---
title: "aaaCopy un VM Linux à l’aide d’Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toocreate une copie de votre machine virtuelle Linux de Azure à l’aide d’Azure CLI 2.0 et disques gérés."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="1f585-103">Créer une copie de machine virtuelle Linux à l’aide d’Azure CLI 2.0 et de disques gérés</span><span class="sxs-lookup"><span data-stu-id="1f585-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="1f585-104">Cet article vous explique comment toocreate une copie de votre machine virtuelle Azure (VM) en cours d’exécution à l’aide de Linux hello Azure CLI 2.0 et le modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1f585-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Azure CLI 2.0 and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="1f585-105">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f585-105">You can also perform these steps with hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1f585-106">Vous pouvez également [charger et créer une machine virtuelle à partir d’un disque dur virtuel](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f585-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f585-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1f585-107">Prerequisites</span></span>


-   <span data-ttu-id="1f585-108">Installer [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="1f585-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="1f585-109">Se connecter tooan compte Azure avec [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1f585-109">Sign in tooan Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="1f585-110">Avoir un toouse de machine virtuelle Azure en tant que source de hello pour votre copie.</span><span class="sxs-lookup"><span data-stu-id="1f585-110">Have an Azure VM toouse as hello source for your copy.</span></span>

## <a name="step-1-stop-hello-source-vm"></a><span data-ttu-id="1f585-111">Étape 1 : Arrêter l’ordinateur virtuel source de hello</span><span class="sxs-lookup"><span data-stu-id="1f585-111">Step 1: Stop hello source VM</span></span>


<span data-ttu-id="1f585-112">Désallouer la source de hello machine virtuelle à l’aide de [az vm désallouer](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="1f585-112">Deallocate hello source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="1f585-113">exemple Hello désalloue hello ordinateur virtuel nommé **myVM** dans le groupe de ressources hello **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="1f585-113">hello following example deallocates hello VM named **myVM** in hello resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a><span data-ttu-id="1f585-114">Étape 2 : Copier la machine virtuelle de la source hello</span><span class="sxs-lookup"><span data-stu-id="1f585-114">Step 2: Copy hello source VM</span></span>


<span data-ttu-id="1f585-115">toocopy une machine virtuelle, vous créez une copie du disque dur virtuel de sous-jacent hello.</span><span class="sxs-lookup"><span data-stu-id="1f585-115">toocopy a VM, you create a copy of hello underlying virtual hard disk.</span></span> <span data-ttu-id="1f585-116">Ce processus crée un disque dur virtuel spécialisé de disque géré contient hello même configuration et les paramètres de type hello de machine virtuelle source.</span><span class="sxs-lookup"><span data-stu-id="1f585-116">This process creates a specialized VHD as a Managed Disk that contains hello same configuration and settings as hello source VM.</span></span>

<span data-ttu-id="1f585-117">Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f585-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="1f585-118">Chaque nom de machine virtuelle et hello de son disque du système d’exploitation avec [liste d’ordinateurs virtuels az](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="1f585-118">List each VM and hello name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="1f585-119">exemple Hello répertorie tous les ordinateurs virtuels dans le groupe de ressources nommé **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="1f585-119">hello following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="1f585-120">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1f585-120">hello output is similar toohello following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="1f585-121">Copier une disquette hello en créant un nouveau gérés à l’aide du disque [az créer](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="1f585-121">Copy hello disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="1f585-122">Hello exemple suivant crée un disque nommé **myCopiedDisk** hello géré disque nommé **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="1f585-122">hello following example creates a disk named **myCopiedDisk** from hello managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="1f585-123">Vérifiez les disques hello géré désormais dans votre groupe de ressources à l’aide de [liste des disques az](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="1f585-123">Verify hello managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="1f585-124">Hello exemple suivant répertorie les disques hello géré dans le groupe de ressources hello nommé **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="1f585-124">hello following example lists hello managed disks in hello resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="1f585-125">Ignorer trop[« étape 3 : configurer un réseau virtuel «](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="1f585-125">Skip too["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="1f585-126">Étape 3 : Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1f585-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="1f585-127">Hello étapes facultatives suivantes créent un nouveau réseau virtuel, un sous-réseau, une adresse IP publique et une carte réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="1f585-127">hello following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="1f585-128">Si vous copiez une machine virtuelle pour le dépannage à des fins ou des déploiements supplémentaires, vous pouvez toouse une machine virtuelle dans un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="1f585-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want toouse a VM in an existing virtual network.</span></span>

<span data-ttu-id="1f585-129">Si vous souhaitez toocreate une infrastructure de réseau virtuel pour vos machines virtuelles copiés, suivez hello suivant quelques étapes.</span><span class="sxs-lookup"><span data-stu-id="1f585-129">If you want toocreate a virtual network infrastructure for your copied VMs, follow hello next few steps.</span></span> <span data-ttu-id="1f585-130">Si vous ne souhaitez pas toocreate un réseau virtuel, passez trop[étape 4 : créer une machine virtuelle](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="1f585-130">If you don't want toocreate a virtual network, skip too[Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="1f585-131">Créer un réseau virtuel de hello à l’aide de [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="1f585-131">Create hello virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="1f585-132">Hello exemple suivant crée un réseau virtuel nommé **myVnet** et un sous-réseau nommé **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="1f585-132">hello following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="1f585-133">Exécutez la commande [az network public-ip create](/cli/azure/network/public-ip#create) pour créer une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="1f585-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="1f585-134">Hello exemple suivant crée une adresse IP publique nommée **myPublicIP** portant le nom DNS de hello de **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="1f585-134">hello following example creates a public IP named **myPublicIP** with hello DNS name of **mypublicdns**.</span></span> <span data-ttu-id="1f585-135">(nom DNS de hello doit être unique, par conséquent, fournissez un nom unique).</span><span class="sxs-lookup"><span data-stu-id="1f585-135">(hello DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="1f585-136">Créer à l’aide de cartes réseau hello [créer des cartes réseau du réseau az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="1f585-136">Create hello NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="1f585-137">Hello exemple suivant crée une carte réseau nommée **myNic** toothe joint de **mySubnet** sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="1f585-137">hello following example creates a NIC named **myNic** that's attached toothe **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="1f585-138">Étape 4 : Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1f585-138">Step 4: Create a VM</span></span>

<span data-ttu-id="1f585-139">Vous pouvez désormais créer une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="1f585-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="1f585-140">Spécifiez hello copiés toouse disque géré en tant que disque de hello du système d’exploitation (--attacher de disque de système d’exploitation), comme suit :</span><span class="sxs-lookup"><span data-stu-id="1f585-140">Specify hello copied managed disk toouse as hello OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="1f585-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f585-141">Next steps</span></span>

<span data-ttu-id="1f585-142">toolearn comment toouse CLI d’Azure toomanage votre nouvelle machine virtuelle, consultez [les commandes CLI d’Azure pour hello Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="1f585-142">toolearn how toouse Azure CLI toomanage your new VM, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
