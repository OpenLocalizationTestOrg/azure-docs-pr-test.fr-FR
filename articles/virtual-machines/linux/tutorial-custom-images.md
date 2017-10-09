---
title: "images de machine virtuelle personnalisées aaaCreate avec hello CLI d’Azure | Documents Microsoft"
description: "Didacticiel : créer une image de machine virtuelle personnalisée à l’aide de hello CLI d’Azure."
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
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="c72a7-103">Créer une image personnalisée d’une machine virtuelle de Azure à l’aide de hello CLI</span><span class="sxs-lookup"><span data-stu-id="c72a7-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="c72a7-104">Les images personnalisées sont comme des images de la Place de marché, sauf que vous les créez vous-même.</span><span class="sxs-lookup"><span data-stu-id="c72a7-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="c72a7-105">Images personnalisées peuvent être des configurations toobootstrap utilisés tels que le préchargement des applications, les configurations de l’application et les autres configurations de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="c72a7-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="c72a7-106">Ce didacticiel explique comment créer votre propre image personnalisée d’une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="c72a7-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="c72a7-107">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c72a7-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c72a7-108">Annuler le déploiement de machines virtuelles et généraliser des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="c72a7-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="c72a7-109">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="c72a7-109">Create a custom image</span></span>
> * <span data-ttu-id="c72a7-110">Créer une machine virtuelle à partir d’une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="c72a7-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="c72a7-111">La liste de toutes les images hello dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="c72a7-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="c72a7-112">Supprimer une image</span><span class="sxs-lookup"><span data-stu-id="c72a7-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c72a7-113">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c72a7-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c72a7-114">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c72a7-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c72a7-115">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c72a7-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="c72a7-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c72a7-116">Before you begin</span></span>

<span data-ttu-id="c72a7-117">étapes Hello ci-dessous décrit en détail comment tootake une machine virtuelle existante et les activer dans personnalisé réutilisable de l’image que vous peuvent utiliser toocreate de nouvelles instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c72a7-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="c72a7-118">exemple de hello toocomplete dans ce didacticiel, vous devez disposer d’un ordinateur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="c72a7-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="c72a7-119">Si nécessaire, cet [exemple de script](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) peut en créer une pour vous.</span><span class="sxs-lookup"><span data-stu-id="c72a7-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="c72a7-120">Lorsque le travail didacticiel de hello, remplacez machine virtuelle et groupe de ressources hello noms lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c72a7-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="c72a7-121">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="c72a7-121">Create a custom image</span></span>

<span data-ttu-id="c72a7-122">toocreate une image d’un ordinateur virtuel, vous devez tooprepare hello VM par mise hors service, désallouer, puis marque la source de hello machine virtuelle comme généralisé.</span><span class="sxs-lookup"><span data-stu-id="c72a7-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="c72a7-123">Une fois hello que machine virtuelle a été préparée, vous pouvez créer une image.</span><span class="sxs-lookup"><span data-stu-id="c72a7-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="c72a7-124">Annuler le déploiement hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c72a7-124">Deprovision hello VM</span></span> 

<span data-ttu-id="c72a7-125">Annulation de généralise hello machine virtuelle en supprimant les informations spécifiques à l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c72a7-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="c72a7-126">Cette généralisation rend possible toodeploy de machines virtuelles à partir d’une seule image.</span><span class="sxs-lookup"><span data-stu-id="c72a7-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="c72a7-127">Au cours de la mise hors service, le nom d’hôte hello est réinitialisé trop*localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="c72a7-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="c72a7-128">Les clés d’hôte SSH, les configurations de serveur de noms, le mot de passe racine et les baux DHCP mis en cache sont également supprimés.</span><span class="sxs-lookup"><span data-stu-id="c72a7-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="c72a7-129">toodeprovision hello machine virtuelle, utilisez l’agent de machine virtuelle Azure hello (waagent).</span><span class="sxs-lookup"><span data-stu-id="c72a7-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="c72a7-130">l’agent de machine virtuelle Azure Hello est installé sur la machine virtuelle de hello et gère la configuration et l’utilisation de hello contrôleur de structure Azure.</span><span class="sxs-lookup"><span data-stu-id="c72a7-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="c72a7-131">Pour plus d’informations, consultez hello [guide de l’utilisateur Linux Agent Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c72a7-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="c72a7-132">Se connecter tooyour machine virtuelle à l’aide de SSH et exécution Bonjour commande toodeprovision Bonjour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c72a7-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="c72a7-133">Avec hello `+user` argument, dernier compte d’utilisateur configuré hello et toutes les données associées sont également supprimées.</span><span class="sxs-lookup"><span data-stu-id="c72a7-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="c72a7-134">Remplacez l’exemple d’adresse IP hello avec hello adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c72a7-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="c72a7-135">SSH toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c72a7-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="c72a7-136">Annuler le déploiement hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c72a7-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="c72a7-137">Fermez la session SSH hello.</span><span class="sxs-lookup"><span data-stu-id="c72a7-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="c72a7-138">Désallouer et marquer hello machine virtuelle comme généralisé</span><span class="sxs-lookup"><span data-stu-id="c72a7-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="c72a7-139">toocreate une image, hello machine virtuelle doit toobe désallouée.</span><span class="sxs-lookup"><span data-stu-id="c72a7-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="c72a7-140">Désallouer hello machine virtuelle en utilisant [az vm désallouer](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="c72a7-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="c72a7-141">Enfin, définissez état hello Hello machine virtuelle comme généralisée avec [az vm généraliser](/cli//azure/vm#generalize) afin que hello plateforme Azure sache hello machine virtuelle a été généralisé.</span><span class="sxs-lookup"><span data-stu-id="c72a7-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="c72a7-142">Vous pouvez uniquement créer une image à partir d’une machine virtuelle généralisée.</span><span class="sxs-lookup"><span data-stu-id="c72a7-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="c72a7-143">Création d’image de hello</span><span class="sxs-lookup"><span data-stu-id="c72a7-143">Create hello image</span></span>

<span data-ttu-id="c72a7-144">Vous pouvez désormais créer une image de machine virtuelle de hello à l’aide de [az image création](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="c72a7-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="c72a7-145">Hello exemple suivant crée une image nommée *myImage* à partir d’un ordinateur virtuel nommé *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c72a7-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="c72a7-146">Créer des ordinateurs virtuels à partir de l’image de hello</span><span class="sxs-lookup"><span data-stu-id="c72a7-146">Create VMs from hello image</span></span>

<span data-ttu-id="c72a7-147">Maintenant que vous disposez d’une image, vous pouvez créer un ou plusieurs nouveaux ordinateurs virtuels à partir de l’image de hello à l’aide [az vm créer](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c72a7-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c72a7-148">Hello exemple suivant crée un ordinateur virtuel nommé *myVMfromImage* à partir de l’image hello nommée *myImage*.</span><span class="sxs-lookup"><span data-stu-id="c72a7-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="c72a7-149">Gestion d’image</span><span class="sxs-lookup"><span data-stu-id="c72a7-149">Image management</span></span> 

<span data-ttu-id="c72a7-150">Voici quelques exemples de tâches de gestion d’image courantes et comment toocomplete les à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="c72a7-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="c72a7-151">Répertoriez toutes les images par nom dans un format de tableau.</span><span class="sxs-lookup"><span data-stu-id="c72a7-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="c72a7-152">Supprimez une image.</span><span class="sxs-lookup"><span data-stu-id="c72a7-152">Delete an image.</span></span> <span data-ttu-id="c72a7-153">Cet exemple supprime hello image nommée *myOldImage* de hello *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="c72a7-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c72a7-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c72a7-154">Next steps</span></span>

<span data-ttu-id="c72a7-155">Ce didacticiel vous montré comment créer une image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c72a7-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="c72a7-156">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c72a7-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c72a7-157">Annuler le déploiement de machines virtuelles et généraliser des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="c72a7-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="c72a7-158">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="c72a7-158">Create a custom image</span></span>
> * <span data-ttu-id="c72a7-159">Créer une machine virtuelle à partir d’une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="c72a7-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="c72a7-160">La liste de toutes les images hello dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="c72a7-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="c72a7-161">Supprimer une image</span><span class="sxs-lookup"><span data-stu-id="c72a7-161">Delete an image</span></span>

<span data-ttu-id="c72a7-162">Avance toohello toolearn de didacticiel suivant sur les ordinateurs virtuels hautement disponibles.</span><span class="sxs-lookup"><span data-stu-id="c72a7-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="c72a7-163">[How to use availability sets](tutorial-availability-sets.md) (Comment utiliser des groupes à haute disponibilité).</span><span class="sxs-lookup"><span data-stu-id="c72a7-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

