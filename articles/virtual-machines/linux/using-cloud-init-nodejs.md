---
title: "Utilisation de cloud-init pour personnaliser une machine virtuelle Linux lors de la création dans Azure | Microsoft Docs"
description: "Guide pratique d’utilisation de cloud-init pour personnaliser une machine virtuelle Linux lors de la création avec Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: 0b6150bca333188666935b3c9aa02c4b33690db9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation-with-the-azure-cli-10"></a><span data-ttu-id="0bc1e-103">Utiliser cloud-init pour personnaliser une machine virtuelle Linux lors de la création avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0bc1e-103">Use cloud-init to customize a Linux VM during creation with the Azure CLI 1.0</span></span>
<span data-ttu-id="0bc1e-104">Cet article montre comment créer un script cloud-init pour définir le nom d'hôte, mettre à jour les packages installés et gérer les comptes d'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-104">This article shows how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="0bc1e-105">Les scripts cloud-init sont appelés lors de la création de la machine virtuelle à partir de l’interface de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-105">The cloud-init scripts are called during the VM creation from Azure CLI.</span></span>  <span data-ttu-id="0bc1e-106">L’article requiert :</span><span class="sxs-lookup"><span data-stu-id="0bc1e-106">The article requires:</span></span>

* <span data-ttu-id="0bc1e-107">un compte Azure ([obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="0bc1e-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="0bc1e-108">[l’interface de ligne de commande Azure (CLI)](../../cli-install-nodejs.md) connectée à `azure login` ;</span><span class="sxs-lookup"><span data-stu-id="0bc1e-108">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="0bc1e-109">l’interface de ligne de commande (CLI) Azure *doit être en* mode Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-109">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="0bc1e-110">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="0bc1e-110">CLI versions to complete the task</span></span>
<span data-ttu-id="0bc1e-111">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="0bc1e-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="0bc1e-112">[Azure CLI 1.0](#quick-commands) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="0bc1e-112">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0bc1e-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : notre interface Azure CLI nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0bc1e-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="0bc1e-114">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="0bc1e-114">Quick Commands</span></span>
<span data-ttu-id="0bc1e-115">Créez un script cloud-init.txt qui définit le nom d’hôte, met à jour tous les packages et ajoute un utilisateur sudo à Linux.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-115">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

```sh
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```
<span data-ttu-id="0bc1e-116">Créez un groupe de ressources afin d’y lancer des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-116">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="0bc1e-117">Créez une machine virtuelle Linux à configurer au cours de démarrage à l’aide de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-117">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0bc1e-118">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="0bc1e-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="0bc1e-119">Introduction</span><span class="sxs-lookup"><span data-stu-id="0bc1e-119">Introduction</span></span>
<span data-ttu-id="0bc1e-120">Lorsque vous lancez une nouvelle machine virtuelle Linux, vous obtenez une machine virtuelle Linux standard, non personnalisée ni adaptée à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="0bc1e-121">[Cloud-init](https://cloudinit.readthedocs.org) est un moyen classique d'injecter les paramètres d'un script ou d’une configuration dans cette machine virtuelle Linux lorsqu’elle démarre pour la première fois.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="0bc1e-122">Dans Azure, il existe trois façons différentes d’apporter des modifications à une machine virtuelle Linux pendant son déploiement ou son démarrage.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-122">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="0bc1e-123">Injectez des scripts à l’aide de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="0bc1e-124">Injectez des scripts à l’aide de [l’extension Azure VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0bc1e-124">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="0bc1e-125">Un modèle Azure utilisant cloud-init.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="0bc1e-126">Un modèle Azure utilisant [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0bc1e-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0bc1e-127">Pour injecter des scripts à tout moment après le démarrage :</span><span class="sxs-lookup"><span data-stu-id="0bc1e-127">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="0bc1e-128">SSH pour exécuter directement des commandes.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-128">SSH to run commands directly</span></span>
* <span data-ttu-id="0bc1e-129">Injectez des scripts à l’aide de [l’extension Azure VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)de manière impérative ou dans un modèle Azure.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-129">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="0bc1e-130">Des outils de gestion de la configuration tels qu’Ansible, Salt, Chef et Puppet.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="0bc1e-131">l’extension VMAccess exécute un script comme racine de la même manière à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-131">: VMAccess Extension executes a script as root in the same way using SSH can.</span></span>  <span data-ttu-id="0bc1e-132">Cependant, l’utilisation de l’extension de machine virtuelle active plusieurs fonctionnalités qu’Azure offre qui peuvent être utiles selon votre scénario.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-132">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="0bc1e-133">Disponibilité de cloud-init lors de la création d’alias d’images de machine virtuelle Azure :</span><span class="sxs-lookup"><span data-stu-id="0bc1e-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="0bc1e-134">Alias</span><span class="sxs-lookup"><span data-stu-id="0bc1e-134">Alias</span></span> | <span data-ttu-id="0bc1e-135">Éditeur</span><span class="sxs-lookup"><span data-stu-id="0bc1e-135">Publisher</span></span> | <span data-ttu-id="0bc1e-136">Offer</span><span class="sxs-lookup"><span data-stu-id="0bc1e-136">Offer</span></span> | <span data-ttu-id="0bc1e-137">SKU</span><span class="sxs-lookup"><span data-stu-id="0bc1e-137">SKU</span></span> | <span data-ttu-id="0bc1e-138">Version</span><span class="sxs-lookup"><span data-stu-id="0bc1e-138">Version</span></span> | <span data-ttu-id="0bc1e-139">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="0bc1e-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="0bc1e-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="0bc1e-140">CentOS</span></span> |<span data-ttu-id="0bc1e-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="0bc1e-141">OpenLogic</span></span> |<span data-ttu-id="0bc1e-142">Centos</span><span class="sxs-lookup"><span data-stu-id="0bc1e-142">Centos</span></span> |<span data-ttu-id="0bc1e-143">7,2</span><span class="sxs-lookup"><span data-stu-id="0bc1e-143">7.2</span></span> |<span data-ttu-id="0bc1e-144">le plus récent</span><span class="sxs-lookup"><span data-stu-id="0bc1e-144">latest</span></span> |<span data-ttu-id="0bc1e-145">no</span><span class="sxs-lookup"><span data-stu-id="0bc1e-145">no</span></span> |
| <span data-ttu-id="0bc1e-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0bc1e-146">CoreOS</span></span> |<span data-ttu-id="0bc1e-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0bc1e-147">CoreOS</span></span> |<span data-ttu-id="0bc1e-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0bc1e-148">CoreOS</span></span> |<span data-ttu-id="0bc1e-149">Stable</span><span class="sxs-lookup"><span data-stu-id="0bc1e-149">Stable</span></span> |<span data-ttu-id="0bc1e-150">le plus récent</span><span class="sxs-lookup"><span data-stu-id="0bc1e-150">latest</span></span> |<span data-ttu-id="0bc1e-151">yes</span><span class="sxs-lookup"><span data-stu-id="0bc1e-151">yes</span></span> |
| <span data-ttu-id="0bc1e-152">Debian</span><span class="sxs-lookup"><span data-stu-id="0bc1e-152">Debian</span></span> |<span data-ttu-id="0bc1e-153">credativ</span><span class="sxs-lookup"><span data-stu-id="0bc1e-153">credativ</span></span> |<span data-ttu-id="0bc1e-154">Debian</span><span class="sxs-lookup"><span data-stu-id="0bc1e-154">Debian</span></span> |<span data-ttu-id="0bc1e-155">8</span><span class="sxs-lookup"><span data-stu-id="0bc1e-155">8</span></span> |<span data-ttu-id="0bc1e-156">le plus récent</span><span class="sxs-lookup"><span data-stu-id="0bc1e-156">latest</span></span> |<span data-ttu-id="0bc1e-157">no</span><span class="sxs-lookup"><span data-stu-id="0bc1e-157">no</span></span> |
| <span data-ttu-id="0bc1e-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="0bc1e-158">openSUSE</span></span> |<span data-ttu-id="0bc1e-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="0bc1e-159">SUSE</span></span> |<span data-ttu-id="0bc1e-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="0bc1e-160">openSUSE</span></span> |<span data-ttu-id="0bc1e-161">13.2</span><span class="sxs-lookup"><span data-stu-id="0bc1e-161">13.2</span></span> |<span data-ttu-id="0bc1e-162">le plus récent</span><span class="sxs-lookup"><span data-stu-id="0bc1e-162">latest</span></span> |<span data-ttu-id="0bc1e-163">no</span><span class="sxs-lookup"><span data-stu-id="0bc1e-163">no</span></span> |
| <span data-ttu-id="0bc1e-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="0bc1e-164">RHEL</span></span> |<span data-ttu-id="0bc1e-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="0bc1e-165">Redhat</span></span> |<span data-ttu-id="0bc1e-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="0bc1e-166">RHEL</span></span> |<span data-ttu-id="0bc1e-167">7,2</span><span class="sxs-lookup"><span data-stu-id="0bc1e-167">7.2</span></span> |<span data-ttu-id="0bc1e-168">le plus récent</span><span class="sxs-lookup"><span data-stu-id="0bc1e-168">latest</span></span> |<span data-ttu-id="0bc1e-169">no</span><span class="sxs-lookup"><span data-stu-id="0bc1e-169">no</span></span> |
| <span data-ttu-id="0bc1e-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="0bc1e-170">UbuntuLTS</span></span> |<span data-ttu-id="0bc1e-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="0bc1e-171">Canonical</span></span> |<span data-ttu-id="0bc1e-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="0bc1e-172">UbuntuServer</span></span> |<span data-ttu-id="0bc1e-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="0bc1e-173">14.04.4-LTS</span></span> |<span data-ttu-id="0bc1e-174">le plus récent</span><span class="sxs-lookup"><span data-stu-id="0bc1e-174">latest</span></span> |<span data-ttu-id="0bc1e-175">yes</span><span class="sxs-lookup"><span data-stu-id="0bc1e-175">yes</span></span> |

<span data-ttu-id="0bc1e-176">Microsoft collabore avec ses partenaires pour que cloud-init soit inclus et fonctionne dans les images qu’ils fournissent à Azure.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-176">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="adding-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="0bc1e-177">Ajout d'un script cloud-init à la création d’une machine virtuelle avec l’interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="0bc1e-177">Adding a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="0bc1e-178">Pour lancer un script cloud-init lors de la création d'une machine virtuelle dans Azure, spécifiez le fichier cloud-init à l'aide du commutateur d’interface de ligne de commande Azure `--custom-data` .</span><span class="sxs-lookup"><span data-stu-id="0bc1e-178">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="0bc1e-179">Créez un groupe de ressources afin d’y lancer des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-179">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="0bc1e-180">Créez une machine virtuelle Linux à configurer au cours de démarrage à l’aide de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-180">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="0bc1e-181">Création d'un script cloud-init pour définir le nom d'hôte d'une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="0bc1e-181">Creating a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="0bc1e-182">Le nom d’hôte est l’un des paramètres les plus simples et les plus importants pour une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-182">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="0bc1e-183">Nous pouvons facilement définir ce paramètre en utilisant cloud-init avec ce script.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="0bc1e-184">Exemple de script cloud-init nommé `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="0bc1e-185">Lors du démarrage initial de la machine virtuelle, ce script cloud-init définit le nom d'hôte sur `myservername`.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-185">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

<span data-ttu-id="0bc1e-186">Connectez-vous et vérifiez le nom d'hôte de la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-186">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-to-update-linux"></a><span data-ttu-id="0bc1e-187">Création d'un script cloud-init pour mettre à jour Linux</span><span class="sxs-lookup"><span data-stu-id="0bc1e-187">Creating a cloud-init script to update Linux</span></span>
<span data-ttu-id="0bc1e-188">Pour des questions de sécurité, configurez votre machine virtuelle Ubuntu de manière à ce qu’elle se mette à jour au premier démarrage.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-188">For security, you want your Ubuntu VM to update on the first boot.</span></span>  <span data-ttu-id="0bc1e-189">À l'aide de cloud-init, nous pouvons le faire avec le script suivant, en fonction de la distribution Linux que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-189">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="0bc1e-190">Exemple de script cloud-init `cloud_config_apt_upgrade.txt` pour la famille Debian</span><span class="sxs-lookup"><span data-stu-id="0bc1e-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="0bc1e-191">Une fois Linux démarré, tous les packages installés sont mis à jour par le biais d’ `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-191">After Linux has booted, all the installed packages are updated via `apt-get`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="0bc1e-192">Connectez-vous et vérifiez que tous les packages sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-192">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="0bc1e-193">Création d'un script cloud-init pour ajouter un utilisateur à Linux</span><span class="sxs-lookup"><span data-stu-id="0bc1e-193">Creating a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="0bc1e-194">L’une des premières tâches liées à n'importe quelle nouvelle machine virtuelle Linux consiste à ajouter un utilisateur pour vous-même ou à éviter d'utiliser `root`.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-194">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span></span> <span data-ttu-id="0bc1e-195">Les clés SSH sont la meilleure pratique en matière de sécurité et de facilité d’utilisation. Elles sont ajoutées au fichier `~/.ssh/authorized_keys` avec ce script cloud-init.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-195">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="0bc1e-196">Exemple de script cloud-init `cloud_config_add_users.txt` pour la famille Debian</span><span class="sxs-lookup"><span data-stu-id="0bc1e-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="0bc1e-197">Une fois Linux démarré, tous les utilisateurs répertoriés sont créés et ajoutés au groupe sudo.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-197">After Linux has booted, all the listed users are created and added to the sudo group.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="0bc1e-198">Connectez-vous et vérifiez l’utilisateur qui vient d’être créé.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-198">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="0bc1e-199">Sortie</span><span class="sxs-lookup"><span data-stu-id="0bc1e-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="0bc1e-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0bc1e-200">Next Steps</span></span>
<span data-ttu-id="0bc1e-201">Cloud-init est devenu une méthode standard pour modifier votre machine virtuelle Linux au démarrage.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-201">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="0bc1e-202">Azure propose également des extensions de machine virtuelle, ce qui vous permet de modifier votre machine virtuelle Linux au démarrage ou pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-202">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="0bc1e-203">Par exemple, vous pouvez utiliser la VMAccessExtension Azure pour réinitialiser les informations de SSH ou de l’utilisateur pendant l’exécution de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-203">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="0bc1e-204">Avec cloud-init, vous devez effectuer un redémarrage pour réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0bc1e-204">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="0bc1e-205">À propos des extensions et des fonctionnalités des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="0bc1e-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="0bc1e-206">Gérer les utilisateurs, SSH et vérifier ou réparer les disques de machines virtuelles Azure Linux à l'aide de l’extension VMAccess</span><span class="sxs-lookup"><span data-stu-id="0bc1e-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

