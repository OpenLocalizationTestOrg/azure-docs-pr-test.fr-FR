---
title: "Différentes façons de créer une machine virtuelle Linux avec Azure CLI 1.0 | Microsoft Docs"
description: "Découvrez les différentes façons de créer une machine virtuelle Linux sur Azure, avec des liens vers des outils et des didacticiels pour chaque méthode."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="f80c8-103">Les différentes méthodes de création d’une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="f80c8-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="f80c8-104">Dans Azure, vous avez la possibilité de créer une machine virtuelle (VM) Linux à l’aide des outils et des flux de travail qui vous conviennent.</span><span class="sxs-lookup"><span data-stu-id="f80c8-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="f80c8-105">Cet article résume ces différences et fournit des exemples pour créer vos machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="f80c8-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="f80c8-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f80c8-106">Azure CLI</span></span>
<span data-ttu-id="f80c8-107">Vous pouvez créer des machines virtuelles dans Azure à l’aide d’une des versions suivantes de CLI :</span><span class="sxs-lookup"><span data-stu-id="f80c8-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="f80c8-108">Azure CLI 1.0 : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="f80c8-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f80c8-109">[Azure CLI 2.0](../windows/creation-choices.md) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f80c8-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="f80c8-110">L’interface de ligne de commande Azure 1.0 est disponible sur les plateformes via un package npm, des packages fournis par un distributeur ou un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="f80c8-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="f80c8-111">Vous pouvez en savoir plus sur [la manière d’installer et de configurer l’interface de ligne de commande Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f80c8-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="f80c8-112">Les didacticiels suivants fournissent des exemples d’utilisation de l’interface de commande Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="f80c8-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="f80c8-113">Lisez chaque article pour en savoir plus sur les commandes de démarrage rapide de l’interface de ligne de commande indiquées :</span><span class="sxs-lookup"><span data-stu-id="f80c8-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="f80c8-114">Créer une machine virtuelle Linux à partir de l’interface CLI Azure pour le développement et le test</span><span class="sxs-lookup"><span data-stu-id="f80c8-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md)
  
  * <span data-ttu-id="f80c8-115">L’exemple suivant crée une VM CoreOS à l’aide d’une clé publique nommée *azure_id_rsa.pub* :</span><span class="sxs-lookup"><span data-stu-id="f80c8-115">The following example creates a CoreOS VM using a public key named *azure_id_rsa.pub*:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="f80c8-116">Create a secured Linux VM using an Azure template (Créer une machine virtuelle Linux sécurisée à l’aide d’un modèle Azure)</span><span class="sxs-lookup"><span data-stu-id="f80c8-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="f80c8-117">L’exemple suivant crée une machine virtuelle à l’aide d’un modèle stocké sur GitHub :</span><span class="sxs-lookup"><span data-stu-id="f80c8-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="f80c8-118">Création d’un environnement Linux complet à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f80c8-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md)
  
  * <span data-ttu-id="f80c8-119">Inclut la création d’un équilibrage de charge et de plusieurs machines virtuelles dans un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="f80c8-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="f80c8-120">Ajouter un disque à une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="f80c8-120">Add a disk to a Linux VM</span></span>](add-disk.md)
  
  * <span data-ttu-id="f80c8-121">L’exemple suivant ajoute un disque de *5* Go à une machine virtuelle existante nommée *myVM* :</span><span class="sxs-lookup"><span data-stu-id="f80c8-121">The following example adds a *5* Gb disk to an existing VM named *myVM*:</span></span>
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="f80c8-122">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f80c8-122">Azure portal</span></span>
<span data-ttu-id="f80c8-123">Le [portail Azure](https://portal.azure.com) vous permet de créer rapidement une machine virtuelle, puisque vous n’avez rien à installer sur votre système.</span><span class="sxs-lookup"><span data-stu-id="f80c8-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="f80c8-124">Utilisez le portail Azure pour créer la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="f80c8-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="f80c8-125">Créer une machine virtuelle Linux à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="f80c8-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="f80c8-126">Système d'exploitation et choix d'images</span><span class="sxs-lookup"><span data-stu-id="f80c8-126">Operating system and image choices</span></span>
<span data-ttu-id="f80c8-127">Lors de la création d’une machine virtuelle, vous choisissez une image basée sur le système d’exploitation que vous souhaitez exécuter.</span><span class="sxs-lookup"><span data-stu-id="f80c8-127">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="f80c8-128">Microsoft Azure et ses partenaires proposent de nombreuses images, dont certaines comprennent des applications et des outils préinstallés.</span><span class="sxs-lookup"><span data-stu-id="f80c8-128">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="f80c8-129">Sinon, téléchargez l’une de vos propres images (voir [la section ci-dessous](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="f80c8-129">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="f80c8-130">Images Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f80c8-130">Azure images</span></span>
<span data-ttu-id="f80c8-131">Utilises les commandes de l’interface de ligne de commande `azure vm image` pour voir ce qui est disponible par éditeur, version de distributeur et build.</span><span class="sxs-lookup"><span data-stu-id="f80c8-131">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="f80c8-132">Procédez comme suit pour répertorier les éditeurs disponibles :</span><span class="sxs-lookup"><span data-stu-id="f80c8-132">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location eastus
```

<span data-ttu-id="f80c8-133">Procédez comme suit pour répertorier les produits disponibles (offres) pour un éditeur donné :</span><span class="sxs-lookup"><span data-stu-id="f80c8-133">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

<span data-ttu-id="f80c8-134">Procédez comme suit pour répertorier les références disponibles (versions distributeur) d’une offre donnée :</span><span class="sxs-lookup"><span data-stu-id="f80c8-134">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="f80c8-135">Procédez comme suit pour répertorier toutes les images disponibles pour une version donnée :</span><span class="sxs-lookup"><span data-stu-id="f80c8-135">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="f80c8-136">Les commandes `azure vm quick-create` et `azure vm create` disposent d’alias que vous pouvez utiliser pour accéder rapidement aux distributeurs les plus courants et à leurs versions les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="f80c8-136">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="f80c8-137">Il est souvent plus rapide d’utiliser des alias que d’avoir à spécifier l’éditeur, l’offre, la référence et la version à chaque fois que vous créez une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="f80c8-137">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="f80c8-138">Alias</span><span class="sxs-lookup"><span data-stu-id="f80c8-138">Alias</span></span> | <span data-ttu-id="f80c8-139">Éditeur</span><span class="sxs-lookup"><span data-stu-id="f80c8-139">Publisher</span></span> | <span data-ttu-id="f80c8-140">Offer</span><span class="sxs-lookup"><span data-stu-id="f80c8-140">Offer</span></span> | <span data-ttu-id="f80c8-141">SKU</span><span class="sxs-lookup"><span data-stu-id="f80c8-141">SKU</span></span> | <span data-ttu-id="f80c8-142">Version</span><span class="sxs-lookup"><span data-stu-id="f80c8-142">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="f80c8-143">CentOS</span><span class="sxs-lookup"><span data-stu-id="f80c8-143">CentOS</span></span> |<span data-ttu-id="f80c8-144">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="f80c8-144">OpenLogic</span></span> |<span data-ttu-id="f80c8-145">Centos</span><span class="sxs-lookup"><span data-stu-id="f80c8-145">Centos</span></span> |<span data-ttu-id="f80c8-146">7,2</span><span class="sxs-lookup"><span data-stu-id="f80c8-146">7.2</span></span> |<span data-ttu-id="f80c8-147">le plus récent</span><span class="sxs-lookup"><span data-stu-id="f80c8-147">latest</span></span> |
| <span data-ttu-id="f80c8-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f80c8-148">CoreOS</span></span> |<span data-ttu-id="f80c8-149">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f80c8-149">CoreOS</span></span> |<span data-ttu-id="f80c8-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f80c8-150">CoreOS</span></span> |<span data-ttu-id="f80c8-151">Stable</span><span class="sxs-lookup"><span data-stu-id="f80c8-151">Stable</span></span> |<span data-ttu-id="f80c8-152">le plus récent</span><span class="sxs-lookup"><span data-stu-id="f80c8-152">latest</span></span> |
| <span data-ttu-id="f80c8-153">Debian</span><span class="sxs-lookup"><span data-stu-id="f80c8-153">Debian</span></span> |<span data-ttu-id="f80c8-154">credativ</span><span class="sxs-lookup"><span data-stu-id="f80c8-154">credativ</span></span> |<span data-ttu-id="f80c8-155">Debian</span><span class="sxs-lookup"><span data-stu-id="f80c8-155">Debian</span></span> |<span data-ttu-id="f80c8-156">8</span><span class="sxs-lookup"><span data-stu-id="f80c8-156">8</span></span> |<span data-ttu-id="f80c8-157">le plus récent</span><span class="sxs-lookup"><span data-stu-id="f80c8-157">latest</span></span> |
| <span data-ttu-id="f80c8-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="f80c8-158">openSUSE</span></span> |<span data-ttu-id="f80c8-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="f80c8-159">SUSE</span></span> |<span data-ttu-id="f80c8-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="f80c8-160">openSUSE</span></span> |<span data-ttu-id="f80c8-161">13.2</span><span class="sxs-lookup"><span data-stu-id="f80c8-161">13.2</span></span> |<span data-ttu-id="f80c8-162">le plus récent</span><span class="sxs-lookup"><span data-stu-id="f80c8-162">latest</span></span> |
| <span data-ttu-id="f80c8-163">RHEL</span><span class="sxs-lookup"><span data-stu-id="f80c8-163">RHEL</span></span> |<span data-ttu-id="f80c8-164">Redhat</span><span class="sxs-lookup"><span data-stu-id="f80c8-164">Redhat</span></span> |<span data-ttu-id="f80c8-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="f80c8-165">RHEL</span></span> |<span data-ttu-id="f80c8-166">7,2</span><span class="sxs-lookup"><span data-stu-id="f80c8-166">7.2</span></span> |<span data-ttu-id="f80c8-167">le plus récent</span><span class="sxs-lookup"><span data-stu-id="f80c8-167">latest</span></span> |
| <span data-ttu-id="f80c8-168">SLES</span><span class="sxs-lookup"><span data-stu-id="f80c8-168">SLES</span></span> |<span data-ttu-id="f80c8-169">SLES</span><span class="sxs-lookup"><span data-stu-id="f80c8-169">SLES</span></span> |<span data-ttu-id="f80c8-170">SLES</span><span class="sxs-lookup"><span data-stu-id="f80c8-170">SLES</span></span> |<span data-ttu-id="f80c8-171">12-SP1</span><span class="sxs-lookup"><span data-stu-id="f80c8-171">12-SP1</span></span> |<span data-ttu-id="f80c8-172">le plus récent</span><span class="sxs-lookup"><span data-stu-id="f80c8-172">latest</span></span> |
| <span data-ttu-id="f80c8-173">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="f80c8-173">UbuntuLTS</span></span> |<span data-ttu-id="f80c8-174">Canonical</span><span class="sxs-lookup"><span data-stu-id="f80c8-174">Canonical</span></span> |<span data-ttu-id="f80c8-175">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="f80c8-175">UbuntuServer</span></span> |<span data-ttu-id="f80c8-176">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="f80c8-176">14.04.4-LTS</span></span> |<span data-ttu-id="f80c8-177">le plus récent</span><span class="sxs-lookup"><span data-stu-id="f80c8-177">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="f80c8-178">Utiliser votre propre image</span><span class="sxs-lookup"><span data-stu-id="f80c8-178">Use your own image</span></span>
<span data-ttu-id="f80c8-179">Si vous avez besoin de personnalisations spécifiques, vous pouvez utiliser une image basée sur une machine virtuelle Azure existante, en *capturant* cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f80c8-179">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="f80c8-180">Vous pouvez également télécharger une image créée sur site.</span><span class="sxs-lookup"><span data-stu-id="f80c8-180">You can also upload an image created on-premises.</span></span> <span data-ttu-id="f80c8-181">Pour plus d’informations sur les versions prises en charge et comment utiliser vos propres images, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="f80c8-181">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="f80c8-182">Distributions prises en charge par Azure</span><span class="sxs-lookup"><span data-stu-id="f80c8-182">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="f80c8-183">Informations concernant les distributions non approuvées</span><span class="sxs-lookup"><span data-stu-id="f80c8-183">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* [<span data-ttu-id="f80c8-184">Chargement et création d’une machine virtuelle Linux à partir d’une image de disque personnalisée</span><span class="sxs-lookup"><span data-stu-id="f80c8-184">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md)
* <span data-ttu-id="f80c8-185">[Comment capturer une machine virtuelle Linux pour utiliser un modèle de gestionnaire de ressources](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="f80c8-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md).</span></span>
  
  * <span data-ttu-id="f80c8-186">Exemples de commandes rapides pour la capture d’une machine virtuelle existante :</span><span class="sxs-lookup"><span data-stu-id="f80c8-186">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="f80c8-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f80c8-187">Next steps</span></span>
* <span data-ttu-id="f80c8-188">Créez une machine virtuelle Linux à partir du [portail](quick-create-portal.md), avec l’[interface de ligne de commande](quick-create-cli.md) ou à l’aide d’un [modèle Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f80c8-188">Create a Linux VM from the [portal](quick-create-portal.md), with the [CLI](quick-create-cli.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="f80c8-189">Après avoir créé une machine virtuelle Linux, [ajoutez un disque de données](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="f80c8-189">After creating a Linux VM, [add a data disk](add-disk.md).</span></span>
* <span data-ttu-id="f80c8-190">Étapes rapides pour [réinitialiser un mot de passe ou des clés SSH et gérer les utilisateurs](using-vmaccess-extension.md)</span><span class="sxs-lookup"><span data-stu-id="f80c8-190">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md)</span></span>

