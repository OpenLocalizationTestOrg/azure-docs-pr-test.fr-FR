---
title: "aaaDifferent manières toocreate un VM Linux dans Azure | Microsoft Azure"
description: "Découvrez les différentes façons de hello toocreate une machine virtuelle de Linux sur Azure, y compris des liens tootools et des didacticiels pour chaque méthode."
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
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a><span data-ttu-id="a58e3-103">Différentes façons toocreate un VM Linux</span><span class="sxs-lookup"><span data-stu-id="a58e3-103">Different ways toocreate a Linux VM</span></span>
<span data-ttu-id="a58e3-104">Vous avez une grande souplesse hello dans Azure toocreate un ordinateur de virtuel (VM) Linux à l’aide des outils et des flux de travail tooyou à l’aise.</span><span class="sxs-lookup"><span data-stu-id="a58e3-104">You have hello flexibility in Azure toocreate a Linux virtual machine (VM) using tools and workflows comfortable tooyou.</span></span> <span data-ttu-id="a58e3-105">Cet article résume ces différences et des exemples pour la création de vos machines virtuelles Linux, y compris hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a58e3-105">This article summarizes these differences and examples for creating your Linux VMs, including hello Azure CLI 2.0.</span></span> <span data-ttu-id="a58e3-106">Vous pouvez également afficher les choix de la création, y compris hello [Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a58e3-106">You can also view creation choices including hello [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="a58e3-107">Hello [Azure CLI 2.0](/cli/azure/install-az-cli2) n’est disponible sur plusieurs plateformes via un package npm, les packages de distribution fournie ou conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="a58e3-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="a58e3-108">Installez hello build la plus appropriée pour votre environnement et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="a58e3-108">Install hello most appropriate build for your environment and log in tooan Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="a58e3-109">Créer une VM Linux avec hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a58e3-109">Create a Linux VM with hello Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="a58e3-110">Avec la commande [az group create](/cli/azure/group#create), créez un groupe de ressources nommé *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="a58e3-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="a58e3-111">Créer une machine virtuelle avec [az vm créer](/cli/azure/vm#create) nommé *myVM* à l’aide de hello dernières *UbuntuLTS* de l’image et générer des clés SSH s’ils n’existent pas déjà dans *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="a58e3-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using hello latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="a58e3-112">Créer une machine virtuelle Linux à l’aide d’un modèle Azure</span><span class="sxs-lookup"><span data-stu-id="a58e3-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="a58e3-113">Hello exemple suivant utilise [créer de déploiement de groupe az](/cli/azure/group/deployment#create) toocreate une machine virtuelle à partir d’un modèle stocké sur GitHub :</span><span class="sxs-lookup"><span data-stu-id="a58e3-113">hello following example uses [az group deployment create](/cli/azure/group/deployment#create) toocreate a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="a58e3-114">Créer une machine virtuelle Linux et personnaliser avec cloud-init</span><span class="sxs-lookup"><span data-stu-id="a58e3-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="a58e3-115">Créer une application hautement disponible et à charge équilibrée sur plusieurs machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="a58e3-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="a58e3-116">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="a58e3-116">Azure portal</span></span>
<span data-ttu-id="a58e3-117">Hello [portail Azure](https://portal.azure.com) vous permet de tooquickly créer une machine virtuelle, car il n’y a rien tooinstall sur votre système.</span><span class="sxs-lookup"><span data-stu-id="a58e3-117">hello [Azure portal](https://portal.azure.com) allows you tooquickly create a VM since there is nothing tooinstall on your system.</span></span> <span data-ttu-id="a58e3-118">Bonjour Azure toocreate portail Bonjour machine virtuelle, utilisez :</span><span class="sxs-lookup"><span data-stu-id="a58e3-118">Use hello Azure portal toocreate hello VM:</span></span>

* [<span data-ttu-id="a58e3-119">Créer une VM Linux à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a58e3-119">Create a Linux VM using hello Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="a58e3-120">Système d'exploitation et choix d'images</span><span class="sxs-lookup"><span data-stu-id="a58e3-120">Operating system and image choices</span></span>
<span data-ttu-id="a58e3-121">Lorsque vous créez une machine virtuelle, vous choisissez une image basée sur hello souhaité toorun de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="a58e3-121">When creating a VM, you choose an image based on hello operating system you want toorun.</span></span> <span data-ttu-id="a58e3-122">Microsoft Azure et ses partenaires proposent de nombreuses images, dont certaines comprennent des applications et des outils préinstallés.</span><span class="sxs-lookup"><span data-stu-id="a58e3-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="a58e3-123">Ou téléchargez un de vos propres images (consultez [hello suivant la section](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="a58e3-123">Or, upload one of your own images (see [hello following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="a58e3-124">Images Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a58e3-124">Azure images</span></span>
<span data-ttu-id="a58e3-125">Hello d’utilisation [image de machine virtuelle az](/cli/azure/vm/image) commandes toosee ce qui est disponible par le serveur de publication, publication de distribution et aux builds.</span><span class="sxs-lookup"><span data-stu-id="a58e3-125">Use hello [az vm image](/cli/azure/vm/image) commands toosee what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="a58e3-126">Répertorier les éditeurs disponibles :</span><span class="sxs-lookup"><span data-stu-id="a58e3-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="a58e3-127">Répertorier les produits disponibles (offres) pour un éditeur donné :</span><span class="sxs-lookup"><span data-stu-id="a58e3-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="a58e3-128">Répertorier les références disponibles (versions distributeur) d’une offre donnée :</span><span class="sxs-lookup"><span data-stu-id="a58e3-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="a58e3-129">Répertorier toutes les images disponibles pour une version donnée :</span><span class="sxs-lookup"><span data-stu-id="a58e3-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="a58e3-130">Pour plus d’exemples sur l’exploration et à l’aide des images disponibles, consultez [naviguer et sélectionnez les images de machine virtuelle Azure avec hello CLI d’Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="a58e3-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with hello Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="a58e3-131">Hello [az vm créer](/cli/azure/vm#create) commande a l’alias que vous pouvez utiliser l’accès tooquickly hello des versions plus courantes et leurs dernières versions.</span><span class="sxs-lookup"><span data-stu-id="a58e3-131">hello [az vm create](/cli/azure/vm#create) command has aliases you can use tooquickly access hello more common distros and their latest releases.</span></span> <span data-ttu-id="a58e3-132">L’alias est souvent plus rapide que la spécification de serveur de publication hello, offre, référence (SKU) et la version chaque fois que vous créez une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="a58e3-132">Using aliases is often quicker than specifying hello publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="a58e3-133">Alias</span><span class="sxs-lookup"><span data-stu-id="a58e3-133">Alias</span></span> | <span data-ttu-id="a58e3-134">Éditeur</span><span class="sxs-lookup"><span data-stu-id="a58e3-134">Publisher</span></span> | <span data-ttu-id="a58e3-135">Offer</span><span class="sxs-lookup"><span data-stu-id="a58e3-135">Offer</span></span> | <span data-ttu-id="a58e3-136">SKU</span><span class="sxs-lookup"><span data-stu-id="a58e3-136">SKU</span></span> | <span data-ttu-id="a58e3-137">Version</span><span class="sxs-lookup"><span data-stu-id="a58e3-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="a58e3-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="a58e3-138">CentOS</span></span> |<span data-ttu-id="a58e3-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="a58e3-139">OpenLogic</span></span> |<span data-ttu-id="a58e3-140">Centos</span><span class="sxs-lookup"><span data-stu-id="a58e3-140">Centos</span></span> |<span data-ttu-id="a58e3-141">7,2</span><span class="sxs-lookup"><span data-stu-id="a58e3-141">7.2</span></span> |<span data-ttu-id="a58e3-142">le plus récent</span><span class="sxs-lookup"><span data-stu-id="a58e3-142">latest</span></span> |
| <span data-ttu-id="a58e3-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a58e3-143">CoreOS</span></span> |<span data-ttu-id="a58e3-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a58e3-144">CoreOS</span></span> |<span data-ttu-id="a58e3-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a58e3-145">CoreOS</span></span> |<span data-ttu-id="a58e3-146">Stable</span><span class="sxs-lookup"><span data-stu-id="a58e3-146">Stable</span></span> |<span data-ttu-id="a58e3-147">le plus récent</span><span class="sxs-lookup"><span data-stu-id="a58e3-147">latest</span></span> |
| <span data-ttu-id="a58e3-148">Debian</span><span class="sxs-lookup"><span data-stu-id="a58e3-148">Debian</span></span> |<span data-ttu-id="a58e3-149">credativ</span><span class="sxs-lookup"><span data-stu-id="a58e3-149">credativ</span></span> |<span data-ttu-id="a58e3-150">Debian</span><span class="sxs-lookup"><span data-stu-id="a58e3-150">Debian</span></span> |<span data-ttu-id="a58e3-151">8</span><span class="sxs-lookup"><span data-stu-id="a58e3-151">8</span></span> |<span data-ttu-id="a58e3-152">le plus récent</span><span class="sxs-lookup"><span data-stu-id="a58e3-152">latest</span></span> |
| <span data-ttu-id="a58e3-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="a58e3-153">openSUSE</span></span> |<span data-ttu-id="a58e3-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="a58e3-154">SUSE</span></span> |<span data-ttu-id="a58e3-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="a58e3-155">openSUSE</span></span> |<span data-ttu-id="a58e3-156">13.2</span><span class="sxs-lookup"><span data-stu-id="a58e3-156">13.2</span></span> |<span data-ttu-id="a58e3-157">le plus récent</span><span class="sxs-lookup"><span data-stu-id="a58e3-157">latest</span></span> |
| <span data-ttu-id="a58e3-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="a58e3-158">RHEL</span></span> |<span data-ttu-id="a58e3-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="a58e3-159">Redhat</span></span> |<span data-ttu-id="a58e3-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="a58e3-160">RHEL</span></span> |<span data-ttu-id="a58e3-161">7,2</span><span class="sxs-lookup"><span data-stu-id="a58e3-161">7.2</span></span> |<span data-ttu-id="a58e3-162">le plus récent</span><span class="sxs-lookup"><span data-stu-id="a58e3-162">latest</span></span> |
| <span data-ttu-id="a58e3-163">SLES</span><span class="sxs-lookup"><span data-stu-id="a58e3-163">SLES</span></span> |<span data-ttu-id="a58e3-164">SLES</span><span class="sxs-lookup"><span data-stu-id="a58e3-164">SLES</span></span> |<span data-ttu-id="a58e3-165">SLES</span><span class="sxs-lookup"><span data-stu-id="a58e3-165">SLES</span></span> |<span data-ttu-id="a58e3-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="a58e3-166">12-SP1</span></span> |<span data-ttu-id="a58e3-167">le plus récent</span><span class="sxs-lookup"><span data-stu-id="a58e3-167">latest</span></span> |
| <span data-ttu-id="a58e3-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="a58e3-168">UbuntuLTS</span></span> |<span data-ttu-id="a58e3-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="a58e3-169">Canonical</span></span> |<span data-ttu-id="a58e3-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="a58e3-170">UbuntuServer</span></span> |<span data-ttu-id="a58e3-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="a58e3-171">14.04.4-LTS</span></span> |<span data-ttu-id="a58e3-172">le plus récent</span><span class="sxs-lookup"><span data-stu-id="a58e3-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="a58e3-173">Utiliser votre propre image</span><span class="sxs-lookup"><span data-stu-id="a58e3-173">Use your own image</span></span>
<span data-ttu-id="a58e3-174">Si vous avez besoin de personnalisations spécifiques, vous pouvez utiliser une image basée sur une machine virtuelle Azure existante, en capturant cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a58e3-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="a58e3-175">Vous pouvez également télécharger une image créée sur site.</span><span class="sxs-lookup"><span data-stu-id="a58e3-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="a58e3-176">Pour plus d’informations sur les versions prises en charge et toouse vos propres images, voir hello suivants articles :</span><span class="sxs-lookup"><span data-stu-id="a58e3-176">For more information on supported distros and how toouse your own images, see hello following articles:</span></span>

* [<span data-ttu-id="a58e3-177">Distributions prises en charge par Azure</span><span class="sxs-lookup"><span data-stu-id="a58e3-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="a58e3-178">Informations concernant les distributions non approuvées</span><span class="sxs-lookup"><span data-stu-id="a58e3-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="a58e3-179">[Comment toocreate une image à partir d’une machine virtuelle Azure existante](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="a58e3-179">[How toocreate an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="a58e3-180">Exemple de démarrage rapide des commandes toocreate une image à partir d’une machine virtuelle Azure existante :</span><span class="sxs-lookup"><span data-stu-id="a58e3-180">Quick-start example commands toocreate an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="a58e3-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a58e3-181">Next steps</span></span>
* <span data-ttu-id="a58e3-182">Créer une VM Linux avec hello [CLI](quick-create-cli.md), à partir de hello [portal](quick-create-portal.md), ou en utilisant un [modèle Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a58e3-182">Create a Linux VM with hello [CLI](quick-create-cli.md), from hello [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="a58e3-183">Après avoir créé une machine virtuelle Linux, [en savoir plus sur les disques et les stockages Azure](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="a58e3-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="a58e3-184">Les étapes trop rapide[réinitialiser un mot de passe ou des clés SSH et gérer des utilisateurs](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a58e3-184">Quick steps too[reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
