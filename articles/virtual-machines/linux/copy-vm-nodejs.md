---
title: "Créer une copie de votre machine virtuelle Linux à l’aide d’Azure CLI 1.0 | Microsoft Docs"
description: "Découvrez comment créer une copie de votre machine virtuelle Linux Azure à l’aide d’Azure CLI 1.0 dans le modèle de déploiement Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 62ae54f3596c9383cbf3b401fcfdb42ecfdee63c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-the-azure-cli-10"></a><span data-ttu-id="44b14-103">Créer une copie d’une machine virtuelle Linux exécutée sur Azure à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="44b14-103">Create a copy of a Linux virtual machine running on Azure with the Azure CLI 1.0</span></span>
<span data-ttu-id="44b14-104">Cet article vous explique comment créer une copie de votre machine virtuelle Azure exécutant Linux dans le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="44b14-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Resource Manager deployment model.</span></span> <span data-ttu-id="44b14-105">Copiez tout d’abord les disques du système d’exploitation et les disques de données dans un nouveau conteneur, configurez les ressources réseau puis créez la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="44b14-105">First you copy over the operating system and data disks to a new container, then set up the network resources and create the new virtual machine.</span></span>

<span data-ttu-id="44b14-106">Vous pouvez également [charger et créer une machine virtuelle à partir d’une image de disque personnalisée](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="44b14-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="44b14-107">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="44b14-107">CLI versions to complete the task</span></span>
<span data-ttu-id="44b14-108">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="44b14-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="44b14-109">Azure CLI 1.0 : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="44b14-109">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="44b14-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="44b14-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="44b14-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="44b14-111">Before you begin</span></span>
<span data-ttu-id="44b14-112">Assurez-vous de disposer des composants requis suivants avant de commencer la procédure :</span><span class="sxs-lookup"><span data-stu-id="44b14-112">Ensure that you meet the following prerequisites before you start the steps:</span></span>

* <span data-ttu-id="44b14-113">Vous avez téléchargé et installé l [’interface de ligne de commande Azure](../../cli-install-nodejs.md) sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="44b14-113">You have the [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="44b14-114">Vous devez également recueillir quelques informations concernant votre machine virtuelle Linux Azure existante :</span><span class="sxs-lookup"><span data-stu-id="44b14-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="44b14-115">Informations sur la machine virtuelle source</span><span class="sxs-lookup"><span data-stu-id="44b14-115">Source VM information</span></span> | <span data-ttu-id="44b14-116">Comment les obtenir</span><span class="sxs-lookup"><span data-stu-id="44b14-116">Where to get it</span></span> |
| --- | --- |
| <span data-ttu-id="44b14-117">Nom de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="44b14-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="44b14-118">Nom du groupe ressources</span><span class="sxs-lookup"><span data-stu-id="44b14-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="44b14-119">Emplacement</span><span class="sxs-lookup"><span data-stu-id="44b14-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="44b14-120">Nom du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="44b14-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="44b14-121">Nom du conteneur</span><span class="sxs-lookup"><span data-stu-id="44b14-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="44b14-122">Nom du fichier VHD de la machine virtuelle source</span><span class="sxs-lookup"><span data-stu-id="44b14-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="44b14-123">Vous devrez faire certains choix concernant votre nouvelle machine virtuelle :    </span><span class="sxs-lookup"><span data-stu-id="44b14-123">You will need to make some choices about your new VM:    </span></span><br> <span data-ttu-id="44b14-124">-Nom du conteneur    </span><span class="sxs-lookup"><span data-stu-id="44b14-124">-Container name    </span></span><br> <span data-ttu-id="44b14-125">-Nom de la machine virtuelle    </span><span class="sxs-lookup"><span data-stu-id="44b14-125">-VM name    </span></span><br> <span data-ttu-id="44b14-126">-Taille de la machine virtuelle    </span><span class="sxs-lookup"><span data-stu-id="44b14-126">-VM size    </span></span><br> <span data-ttu-id="44b14-127">-Nom du réseau virtuel    </span><span class="sxs-lookup"><span data-stu-id="44b14-127">-vNet name    </span></span><br> <span data-ttu-id="44b14-128">-Nom du sous-réseau    </span><span class="sxs-lookup"><span data-stu-id="44b14-128">-SubNet name    </span></span><br> <span data-ttu-id="44b14-129">-Nom IP    </span><span class="sxs-lookup"><span data-stu-id="44b14-129">-IP Name    </span></span><br> <span data-ttu-id="44b14-130">-nom de la carte réseau</span><span class="sxs-lookup"><span data-stu-id="44b14-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="44b14-131">Se connecter et définir votre abonnement</span><span class="sxs-lookup"><span data-stu-id="44b14-131">Login and set your subscription</span></span>
1. <span data-ttu-id="44b14-132">Connectez-vous à l’interface de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="44b14-132">Login to the CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="44b14-133">Assurez-vous que vous êtes en mode Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="44b14-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="44b14-134">Définissez l'abonnement approprié.</span><span class="sxs-lookup"><span data-stu-id="44b14-134">Set the correct subscription.</span></span> <span data-ttu-id="44b14-135">Vous pouvez utiliser ’azure account list’ pour voir tous vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="44b14-135">You can use 'azure account list' to see all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-the-vm"></a><span data-ttu-id="44b14-136">Arrêtez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="44b14-136">Stop the VM</span></span>
<span data-ttu-id="44b14-137">Arrêtez et libérez la machine virtuelle source.</span><span class="sxs-lookup"><span data-stu-id="44b14-137">Stop and deallocate the source VM.</span></span> <span data-ttu-id="44b14-138">Vous pouvez utiliser ’azure vm list’ pour obtenir une liste de toutes les machines virtuelles de votre abonnement ainsi que les noms de leurs groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="44b14-138">You can use 'azure vm list' to get a list of all of the VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-the-vhd"></a><span data-ttu-id="44b14-139">Copier le disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="44b14-139">Copy the VHD</span></span>
<span data-ttu-id="44b14-140">Vous pouvez copier le disque dur virtuel du stockage source vers le stockage de destination à l’aide de la commande `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="44b14-140">You can copy the VHD from the source storage to the destination using the `azure storage blob copy start`.</span></span> <span data-ttu-id="44b14-141">Dans cet exemple, nous allons copier le disque dur virtuel vers le même compte de stockage, mais dans un autre conteneur.</span><span class="sxs-lookup"><span data-stu-id="44b14-141">In this example, we are going to copy the VHD to the same storage account, but a different container.</span></span>

<span data-ttu-id="44b14-142">Pour copier le disque dur virtuel vers un autre conteneur du même compte de stockage, tapez :</span><span class="sxs-lookup"><span data-stu-id="44b14-142">To copy the VHD to another container in the same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-the-virtual-network-for-your-new-vm"></a><span data-ttu-id="44b14-143">Configurer le réseau virtuel pour votre nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="44b14-143">Set up the virtual network for your new VM</span></span>
<span data-ttu-id="44b14-144">Configurez un réseau virtuel et une carte réseau pour votre nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="44b14-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-the-new-vm"></a><span data-ttu-id="44b14-145">Créer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="44b14-145">Create the new VM</span></span>
<span data-ttu-id="44b14-146">Vous pouvez maintenant créer une machine virtuelle à partir du disque virtuel chargé [en utilisant un modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) ou via la CLI en spécifiant l’URI pointant vers votre disque copié, comme suit :</span><span class="sxs-lookup"><span data-stu-id="44b14-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through the CLI by specifying the URI to your copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="44b14-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="44b14-147">Next steps</span></span>
<span data-ttu-id="44b14-148">Pour plus d’informations sur l’utilisation de l’interface de ligne de commande Azure pour gérer votre nouvelle machine virtuelle, voir [Commandes de l’interface de ligne de commande Azure en mode Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="44b14-148">To learn how to use Azure CLI to manage your new virtual machine, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

