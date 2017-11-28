---
title: "Créer des images de machine virtuelle personnalisées avec l’interface de ligne de commande Azure | Microsoft Docs"
description: "Didacticiel : créez une image de machine virtuelle personnalisée à l’aide de l’interface de ligne de commande Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d32980f05ad17a76793021d0a5355d597974a4e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-the-cli"></a><span data-ttu-id="e87ad-103">Créer une image personnalisée d’une machine virtuelle Azure à l’aide de l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="e87ad-103">Create a custom image of an Azure VM using the CLI</span></span>

<span data-ttu-id="e87ad-104">Les images personnalisées sont comme des images de la Place de marché, sauf que vous les créez vous-même.</span><span class="sxs-lookup"><span data-stu-id="e87ad-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="e87ad-105">Les images personnalisées peuvent être utilisées pour amorcer des configurations comme le préchargement des applications, les configurations d’application et d’autres configurations de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="e87ad-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="e87ad-106">Ce didacticiel explique comment créer votre propre image personnalisée d’une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="e87ad-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="e87ad-107">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="e87ad-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e87ad-108">Annuler le déploiement de machines virtuelles et généraliser des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="e87ad-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="e87ad-109">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="e87ad-109">Create a custom image</span></span>
> * <span data-ttu-id="e87ad-110">Créer une machine virtuelle à partir d’une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="e87ad-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="e87ad-111">Répertorier toutes les images dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="e87ad-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="e87ad-112">Supprimer une image</span><span class="sxs-lookup"><span data-stu-id="e87ad-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e87ad-113">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter l’interface de ligne de commande Azure version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e87ad-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e87ad-114">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="e87ad-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="e87ad-115">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e87ad-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="e87ad-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e87ad-116">Before you begin</span></span>

<span data-ttu-id="e87ad-117">Les étapes ci-dessous expliquent comment prendre une machine virtuelle existante et la transformer en une image personnalisée réutilisable que vous pouvez utiliser pour créer de nouvelles instances de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e87ad-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="e87ad-118">Pour exécuter l’exemple dans ce didacticiel, vous devez disposer d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e87ad-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="e87ad-119">Si nécessaire, cet [exemple de script](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) peut en créer une pour vous.</span><span class="sxs-lookup"><span data-stu-id="e87ad-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="e87ad-120">Au cours du didacticiel, remplacez les noms du groupe de ressources et de la machine virtuelle si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e87ad-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="e87ad-121">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="e87ad-121">Create a custom image</span></span>

<span data-ttu-id="e87ad-122">Pour créer une image de machine virtuelle, vous devez préparer la machine virtuelle en annulant l’approvisionnement, en la libérant et en la marquant comme généralisée.</span><span class="sxs-lookup"><span data-stu-id="e87ad-122">To create an image of a virtual machine, you need to prepare the VM by deprovisioning, deallocating, and then marking the source VM as generalized.</span></span> <span data-ttu-id="e87ad-123">Une fois la machine virtuelle préparée, vous pouvez créer une image.</span><span class="sxs-lookup"><span data-stu-id="e87ad-123">Once the VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-the-vm"></a><span data-ttu-id="e87ad-124">Annuler l’approvisionnement de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e87ad-124">Deprovision the VM</span></span> 

<span data-ttu-id="e87ad-125">L’annulation de l’approvisionnement généralise la machine virtuelle en supprimant les informations spécifiques à la machine.</span><span class="sxs-lookup"><span data-stu-id="e87ad-125">Deprovisioning generalizes the VM by removing machine-specific information.</span></span> <span data-ttu-id="e87ad-126">Cette généralisation permet de déployer plusieurs machines virtuelles à partir d’une image unique.</span><span class="sxs-lookup"><span data-stu-id="e87ad-126">This generalization makes it possible to deploy many VMs from a single image.</span></span> <span data-ttu-id="e87ad-127">Au cours de l’annulation de l’approvisionnement, le nom d’hôte est réinitialisé sur *localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="e87ad-127">During deprovisioning, the host name is reset to *localhost.localdomain*.</span></span> <span data-ttu-id="e87ad-128">Les clés d’hôte SSH, les configurations de serveur de noms, le mot de passe racine et les baux DHCP mis en cache sont également supprimés.</span><span class="sxs-lookup"><span data-stu-id="e87ad-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="e87ad-129">Pour annuler l’approvisionnement de la machine virtuelle, utilisez l’agent de machine virtuelle Azure (waagent).</span><span class="sxs-lookup"><span data-stu-id="e87ad-129">To deprovision the VM, use the Azure VM agent (waagent).</span></span> <span data-ttu-id="e87ad-130">L’agent de machine virtuelle Azure est installé sur la machine virtuelle et gère l’approvisionnement et l’interaction avec le contrôleur de structure Azure.</span><span class="sxs-lookup"><span data-stu-id="e87ad-130">The Azure VM agent is installed on the VM and manages provisioning and interacting with the Azure Fabric Controller.</span></span> <span data-ttu-id="e87ad-131">Pour plus d’informations, consultez le [Guide d’utilisateur de l’agent Linux Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e87ad-131">For more information, see the [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="e87ad-132">Connectez-vous à votre machine virtuelle à l’aide du protocole SSH et exécutez la commande pour annuler l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e87ad-132">Connect to your VM using SSH and run the command to deprovision the VM.</span></span> <span data-ttu-id="e87ad-133">Avec l’argument `+user`, le dernier compte d’utilisateur approvisionné et les données associées sont également supprimés.</span><span class="sxs-lookup"><span data-stu-id="e87ad-133">With the `+user` argument, the last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="e87ad-134">Remplacez l’exemple d’adresse IP par l’adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e87ad-134">Replace the example IP address with the public IP address of your VM.</span></span>

<span data-ttu-id="e87ad-135">Utilisez une clé SSH sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e87ad-135">SSH to the VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="e87ad-136">Annulez l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e87ad-136">Deprovision the VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="e87ad-137">Fermez la session SSH.</span><span class="sxs-lookup"><span data-stu-id="e87ad-137">Close the SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="e87ad-138">Libérer la machine virtuelle et la marquer comme généralisée</span><span class="sxs-lookup"><span data-stu-id="e87ad-138">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="e87ad-139">Pour créer une image, la machine virtuelle doit être libérée.</span><span class="sxs-lookup"><span data-stu-id="e87ad-139">To create an image, the VM needs to be deallocated.</span></span> <span data-ttu-id="e87ad-140">Libérez la machine virtuelle à l’aide de [az vm deallocate](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="e87ad-140">Deallocate the VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e87ad-141">Enfin, définissez l’état de la machine virtuelle comme généralisé avec [az vm generalize](/cli//azure/vm#generalize) afin que la plateforme Azure sache que la machine virtuelle a été généralisée.</span><span class="sxs-lookup"><span data-stu-id="e87ad-141">Finally, set the state of the VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so the Azure platform knows the VM has been generalized.</span></span> <span data-ttu-id="e87ad-142">Vous pouvez uniquement créer une image à partir d’une machine virtuelle généralisée.</span><span class="sxs-lookup"><span data-stu-id="e87ad-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-the-image"></a><span data-ttu-id="e87ad-143">Création de l’image</span><span class="sxs-lookup"><span data-stu-id="e87ad-143">Create the image</span></span>

<span data-ttu-id="e87ad-144">Créez à présent une image de la machine virtuelle à l’aide de [az image create](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="e87ad-144">Now you can create an image of the VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="e87ad-145">L’exemple suivant crée une image nommée *myimage* à partir d’une machine virtuelle nommée *myimage*.</span><span class="sxs-lookup"><span data-stu-id="e87ad-145">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="e87ad-146">Créer des machines virtuelles à partir de l’image</span><span class="sxs-lookup"><span data-stu-id="e87ad-146">Create VMs from the image</span></span>

<span data-ttu-id="e87ad-147">Maintenant que vous avez une image, vous pouvez créer une ou plusieurs nouvelles machines virtuelles à partir de l’image à l’aide de [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e87ad-147">Now that you have an image, you can create one or more new VMs from the image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e87ad-148">L’exemple suivant crée une machine virtuelle nommée *myVMfromImage* à partir de l’image nommée *myImage*.</span><span class="sxs-lookup"><span data-stu-id="e87ad-148">The following example creates a VM named *myVMfromImage* from the image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="e87ad-149">Gestion d’image</span><span class="sxs-lookup"><span data-stu-id="e87ad-149">Image management</span></span> 

<span data-ttu-id="e87ad-150">Voici quelques exemples de tâches de gestion d’image courantes et comment les exécuter à l’aide d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e87ad-150">Here are some examples of common image management tasks and how to complete them using the Azure CLI.</span></span>

<span data-ttu-id="e87ad-151">Répertoriez toutes les images par nom dans un format de tableau.</span><span class="sxs-lookup"><span data-stu-id="e87ad-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="e87ad-152">Supprimez une image.</span><span class="sxs-lookup"><span data-stu-id="e87ad-152">Delete an image.</span></span> <span data-ttu-id="e87ad-153">Cet exemple supprime l’image nommée *myOldImage* à partir du groupe *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="e87ad-153">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="e87ad-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e87ad-154">Next steps</span></span>

<span data-ttu-id="e87ad-155">Ce didacticiel vous montré comment créer une image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e87ad-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="e87ad-156">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="e87ad-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e87ad-157">Annuler le déploiement de machines virtuelles et généraliser des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="e87ad-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="e87ad-158">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="e87ad-158">Create a custom image</span></span>
> * <span data-ttu-id="e87ad-159">Créer une machine virtuelle à partir d’une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="e87ad-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="e87ad-160">Répertorier toutes les images dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="e87ad-160">List all the images in your subscription</span></span>
> * <span data-ttu-id="e87ad-161">Supprimer une image</span><span class="sxs-lookup"><span data-stu-id="e87ad-161">Delete an image</span></span>

<span data-ttu-id="e87ad-162">Pour découvrir les machines virtuelles hautement disponibles, passez au didacticiel suivant.</span><span class="sxs-lookup"><span data-stu-id="e87ad-162">Advance to the next tutorial to learn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="e87ad-163">[How to use availability sets](tutorial-availability-sets.md) (Comment utiliser des groupes à haute disponibilité).</span><span class="sxs-lookup"><span data-stu-id="e87ad-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

