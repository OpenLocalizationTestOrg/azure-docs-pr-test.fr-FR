---
title: "Les différentes façons de créer une machine virtuelle Linux | Microsoft Azure"
description: "Découvrez les différentes façons de créer une machine virtuelle Linux sur Azure, avec des liens vers des outils et des didacticiels pour chaque méthode."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: b2f93579eb1c7a69d0dbd1b0ef112aed9b2168c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-linux-vm"></a><span data-ttu-id="35f58-103">Différentes méthodes pour créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="35f58-103">Different ways to create a Linux VM</span></span>
<span data-ttu-id="35f58-104">Dans Azure, vous avez la possibilité de créer une machine virtuelle (VM) Linux à l’aide des outils et des flux de travail qui vous conviennent.</span><span class="sxs-lookup"><span data-stu-id="35f58-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="35f58-105">Cet article résume ces différences et fournit des exemples pour créer vos machines virtuelles Linux, y compris avec Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="35f58-105">This article summarizes these differences and examples for creating your Linux VMs, including the Azure CLI 2.0.</span></span> <span data-ttu-id="35f58-106">Vous trouverez également les options de création à l’aide [d’Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="35f58-106">You can also view creation choices including the [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="35f58-107">[L’interface Azure CLI 2.0](/cli/azure/install-az-cli2) est disponible sur les plateformes via un package npm, des packages fournis par un distributeur ou un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="35f58-107">The [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="35f58-108">Installer la version la plus appropriée pour votre environnement et connectez-vous à un compte Azure à l’aide de [az login](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="35f58-108">Install the most appropriate build for your environment and log in to an Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="35f58-109">Création d’une machine virtuelle Linux avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="35f58-109">Create a Linux VM with the Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="35f58-110">Avec la commande [az group create](/cli/azure/group#create), créez un groupe de ressources nommé *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="35f58-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="35f58-111">Avec la commande [az vm create](/cli/azure/vm#create), créez une machine virtuelle nommée *myVM* à l’aide de la dernière version de l’image *UbuntuLTS* et générez des clés SSH si elles n’existent pas déjà dans *~/.ssh* :</span><span class="sxs-lookup"><span data-stu-id="35f58-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using the latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="35f58-112">Créer une machine virtuelle Linux à l’aide d’un modèle Azure</span><span class="sxs-lookup"><span data-stu-id="35f58-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="35f58-113">L’exemple suivant utilise la commande [az group deployment create](/cli/azure/group/deployment#create) pour créer une machine virtuelle à partir d’un modèle stocké sur GitHub :</span><span class="sxs-lookup"><span data-stu-id="35f58-113">The following example uses [az group deployment create](/cli/azure/group/deployment#create) to create a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="35f58-114">Créer une machine virtuelle Linux et personnaliser avec cloud-init</span><span class="sxs-lookup"><span data-stu-id="35f58-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="35f58-115">Créer une application hautement disponible et à charge équilibrée sur plusieurs machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="35f58-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="35f58-116">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="35f58-116">Azure portal</span></span>
<span data-ttu-id="35f58-117">Le [portail Azure](https://portal.azure.com) vous permet de créer rapidement une machine virtuelle, puisque vous n’avez rien à installer sur votre système.</span><span class="sxs-lookup"><span data-stu-id="35f58-117">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="35f58-118">Utilisez le portail Azure pour créer la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="35f58-118">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="35f58-119">Créer une machine virtuelle Linux à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="35f58-119">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="35f58-120">Système d'exploitation et choix d'images</span><span class="sxs-lookup"><span data-stu-id="35f58-120">Operating system and image choices</span></span>
<span data-ttu-id="35f58-121">Lors de la création d’une machine virtuelle, vous choisissez une image basée sur le système d’exploitation que vous souhaitez exécuter.</span><span class="sxs-lookup"><span data-stu-id="35f58-121">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="35f58-122">Microsoft Azure et ses partenaires proposent de nombreuses images, dont certaines comprennent des applications et des outils préinstallés.</span><span class="sxs-lookup"><span data-stu-id="35f58-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="35f58-123">Sinon, téléchargez l’une de vos propres images (voir [la section ci-dessous](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="35f58-123">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="35f58-124">Images Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="35f58-124">Azure images</span></span>
<span data-ttu-id="35f58-125">Utilisez les commandes [az vm image](/cli/azure/vm/image) pour voir ce qui est disponible par éditeur, version de distributeur et build.</span><span class="sxs-lookup"><span data-stu-id="35f58-125">Use the [az vm image](/cli/azure/vm/image) commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="35f58-126">Répertorier les éditeurs disponibles :</span><span class="sxs-lookup"><span data-stu-id="35f58-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="35f58-127">Répertorier les produits disponibles (offres) pour un éditeur donné :</span><span class="sxs-lookup"><span data-stu-id="35f58-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="35f58-128">Répertorier les références disponibles (versions distributeur) d’une offre donnée :</span><span class="sxs-lookup"><span data-stu-id="35f58-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="35f58-129">Répertorier toutes les images disponibles pour une version donnée :</span><span class="sxs-lookup"><span data-stu-id="35f58-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="35f58-130">Pour obtenir des exemples sur la navigation et l’utilisation d’images disponibles, consultez la page [Sélectionner des images de VM Linux avec l’interface de ligne de commande Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="35f58-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with the Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="35f58-131">La commande [az vm create](/cli/azure/vm#create) dispose d’alias que vous pouvez utiliser pour accéder rapidement aux distributeurs les plus courants et à leurs versions les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="35f58-131">The [az vm create](/cli/azure/vm#create) command has aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="35f58-132">Il est souvent plus rapide d’utiliser des alias que d’avoir à spécifier l’éditeur, l’offre, la référence et la version à chaque fois que vous créez une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="35f58-132">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="35f58-133">Alias</span><span class="sxs-lookup"><span data-stu-id="35f58-133">Alias</span></span> | <span data-ttu-id="35f58-134">Éditeur</span><span class="sxs-lookup"><span data-stu-id="35f58-134">Publisher</span></span> | <span data-ttu-id="35f58-135">Offer</span><span class="sxs-lookup"><span data-stu-id="35f58-135">Offer</span></span> | <span data-ttu-id="35f58-136">SKU</span><span class="sxs-lookup"><span data-stu-id="35f58-136">SKU</span></span> | <span data-ttu-id="35f58-137">Version</span><span class="sxs-lookup"><span data-stu-id="35f58-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="35f58-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="35f58-138">CentOS</span></span> |<span data-ttu-id="35f58-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="35f58-139">OpenLogic</span></span> |<span data-ttu-id="35f58-140">Centos</span><span class="sxs-lookup"><span data-stu-id="35f58-140">Centos</span></span> |<span data-ttu-id="35f58-141">7,2</span><span class="sxs-lookup"><span data-stu-id="35f58-141">7.2</span></span> |<span data-ttu-id="35f58-142">le plus récent</span><span class="sxs-lookup"><span data-stu-id="35f58-142">latest</span></span> |
| <span data-ttu-id="35f58-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="35f58-143">CoreOS</span></span> |<span data-ttu-id="35f58-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="35f58-144">CoreOS</span></span> |<span data-ttu-id="35f58-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="35f58-145">CoreOS</span></span> |<span data-ttu-id="35f58-146">Stable</span><span class="sxs-lookup"><span data-stu-id="35f58-146">Stable</span></span> |<span data-ttu-id="35f58-147">le plus récent</span><span class="sxs-lookup"><span data-stu-id="35f58-147">latest</span></span> |
| <span data-ttu-id="35f58-148">Debian</span><span class="sxs-lookup"><span data-stu-id="35f58-148">Debian</span></span> |<span data-ttu-id="35f58-149">credativ</span><span class="sxs-lookup"><span data-stu-id="35f58-149">credativ</span></span> |<span data-ttu-id="35f58-150">Debian</span><span class="sxs-lookup"><span data-stu-id="35f58-150">Debian</span></span> |<span data-ttu-id="35f58-151">8</span><span class="sxs-lookup"><span data-stu-id="35f58-151">8</span></span> |<span data-ttu-id="35f58-152">le plus récent</span><span class="sxs-lookup"><span data-stu-id="35f58-152">latest</span></span> |
| <span data-ttu-id="35f58-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="35f58-153">openSUSE</span></span> |<span data-ttu-id="35f58-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="35f58-154">SUSE</span></span> |<span data-ttu-id="35f58-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="35f58-155">openSUSE</span></span> |<span data-ttu-id="35f58-156">13.2</span><span class="sxs-lookup"><span data-stu-id="35f58-156">13.2</span></span> |<span data-ttu-id="35f58-157">le plus récent</span><span class="sxs-lookup"><span data-stu-id="35f58-157">latest</span></span> |
| <span data-ttu-id="35f58-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="35f58-158">RHEL</span></span> |<span data-ttu-id="35f58-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="35f58-159">Redhat</span></span> |<span data-ttu-id="35f58-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="35f58-160">RHEL</span></span> |<span data-ttu-id="35f58-161">7,2</span><span class="sxs-lookup"><span data-stu-id="35f58-161">7.2</span></span> |<span data-ttu-id="35f58-162">le plus récent</span><span class="sxs-lookup"><span data-stu-id="35f58-162">latest</span></span> |
| <span data-ttu-id="35f58-163">SLES</span><span class="sxs-lookup"><span data-stu-id="35f58-163">SLES</span></span> |<span data-ttu-id="35f58-164">SLES</span><span class="sxs-lookup"><span data-stu-id="35f58-164">SLES</span></span> |<span data-ttu-id="35f58-165">SLES</span><span class="sxs-lookup"><span data-stu-id="35f58-165">SLES</span></span> |<span data-ttu-id="35f58-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="35f58-166">12-SP1</span></span> |<span data-ttu-id="35f58-167">le plus récent</span><span class="sxs-lookup"><span data-stu-id="35f58-167">latest</span></span> |
| <span data-ttu-id="35f58-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="35f58-168">UbuntuLTS</span></span> |<span data-ttu-id="35f58-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="35f58-169">Canonical</span></span> |<span data-ttu-id="35f58-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="35f58-170">UbuntuServer</span></span> |<span data-ttu-id="35f58-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="35f58-171">14.04.4-LTS</span></span> |<span data-ttu-id="35f58-172">le plus récent</span><span class="sxs-lookup"><span data-stu-id="35f58-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="35f58-173">Utiliser votre propre image</span><span class="sxs-lookup"><span data-stu-id="35f58-173">Use your own image</span></span>
<span data-ttu-id="35f58-174">Si vous avez besoin de personnalisations spécifiques, vous pouvez utiliser une image basée sur une machine virtuelle Azure existante, en capturant cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="35f58-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="35f58-175">Vous pouvez également télécharger une image créée sur site.</span><span class="sxs-lookup"><span data-stu-id="35f58-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="35f58-176">Pour plus d’informations sur les versions prises en charge et comment utiliser vos propres images, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="35f58-176">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="35f58-177">Distributions prises en charge par Azure</span><span class="sxs-lookup"><span data-stu-id="35f58-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="35f58-178">Informations concernant les distributions non approuvées</span><span class="sxs-lookup"><span data-stu-id="35f58-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="35f58-179">[Comment créer une image à partir d’une machine virtuelle Azure existante](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="35f58-179">[How to create an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="35f58-180">Exemples de commandes rapides pour la création d’images à partir d’une machine virtuelle Azure existante :</span><span class="sxs-lookup"><span data-stu-id="35f58-180">Quick-start example commands to create an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="35f58-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="35f58-181">Next steps</span></span>
* <span data-ttu-id="35f58-182">Créez une machine virtuelle Linux avec l’[interface de ligne de commande](quick-create-cli.md), à partir du [portail](quick-create-portal.md) ou à l’aide d’un [modèle Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="35f58-182">Create a Linux VM with the [CLI](quick-create-cli.md), from the [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="35f58-183">Après avoir créé une machine virtuelle Linux, [en savoir plus sur les disques et les stockages Azure](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="35f58-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="35f58-184">Étapes rapides pour [réinitialiser un mot de passe ou des clés SSH et gérer les utilisateurs](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="35f58-184">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
