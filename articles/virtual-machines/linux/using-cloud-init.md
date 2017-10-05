---
title: Utiliser cloud-init pour personnaliser une machine virtuelle Linux | Microsoft Docs
description: "Guide pratique d’utilisation de cloud-init pour personnaliser une machine virtuelle Linux lors de la création avec Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="dd141-103">Utiliser cloud-init pour personnaliser une machine virtuelle Linux lors de la création</span><span class="sxs-lookup"><span data-stu-id="dd141-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="dd141-104">Cet article vous montre comment créer un script cloud-init pour définir le nom d’hôte, mettre à jour les packages installés et gérer les comptes d’utilisateur avec Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="dd141-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span> <span data-ttu-id="dd141-105">Les scripts cloud-init sont appelés lorsque vous créez une machine virtuelle à partir de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="dd141-105">The cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="dd141-106">Pour une présentation plus détaillée de l’installation d’applications, l’écriture de fichiers de configuration et l’injection de clés à partir de Key Vault, consultez [ce didacticiel](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="dd141-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="dd141-107">Vous pouvez également effectuer ces étapes à l’aide [d’Azure CLI 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="dd141-107">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="dd141-108">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="dd141-108">Quick commands</span></span>
<span data-ttu-id="dd141-109">Créez un script cloud-init.txt qui définit le nom d’hôte, met à jour tous les packages et ajoute un utilisateur sudo à Linux.</span><span class="sxs-lookup"><span data-stu-id="dd141-109">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

```yaml
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

<span data-ttu-id="dd141-110">Créez un groupe de ressources pour y lancer des machines virtuelles avec [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="dd141-110">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="dd141-111">L’exemple suivant permet de créer le groupe de ressources nommé *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="dd141-111">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="dd141-112">Créez une machine virtuelle Linux à configurer au cours de démarrage avec [az vm create](/cli/azure/vm#create) à l’aide de cloud-init avec le paramètre `--custom-data`.</span><span class="sxs-lookup"><span data-stu-id="dd141-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot with the `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="dd141-113">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="dd141-113">Detailed walkthrough</span></span>
<span data-ttu-id="dd141-114">Lorsque vous lancez une nouvelle machine virtuelle Linux, vous obtenez une machine virtuelle Linux standard, non personnalisée ni adaptée à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="dd141-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="dd141-115">[Cloud-init](https://cloudinit.readthedocs.org) est un moyen classique d'injecter les paramètres d'un script ou d’une configuration dans cette machine virtuelle Linux lorsqu’elle démarre pour la première fois.</span><span class="sxs-lookup"><span data-stu-id="dd141-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="dd141-116">Dans Azure, il existe plusieurs façons différentes d’apporter des modifications à une machine virtuelle Linux pendant son déploiement ou son démarrage.</span><span class="sxs-lookup"><span data-stu-id="dd141-116">On Azure, there are a few different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="dd141-117">Injectez des scripts à l’aide de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="dd141-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="dd141-118">Injectez des scripts à l’aide de [l’extension Azure VMAccess](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="dd141-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="dd141-119">Un modèle Azure utilisant cloud-init.</span><span class="sxs-lookup"><span data-stu-id="dd141-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="dd141-120">Un modèle Azure utilisant [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="dd141-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="dd141-121">Pour injecter des scripts à tout moment après le démarrage :</span><span class="sxs-lookup"><span data-stu-id="dd141-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="dd141-122">SSH pour exécuter directement des commandes.</span><span class="sxs-lookup"><span data-stu-id="dd141-122">SSH to run commands directly</span></span>
* <span data-ttu-id="dd141-123">Injectez des scripts à l’aide de [l’extension Azure VMAccess](using-vmaccess-extension.md)de manière impérative ou dans un modèle Azure.</span><span class="sxs-lookup"><span data-stu-id="dd141-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="dd141-124">Des outils de gestion de la configuration tels qu’Ansible, Salt, Chef et Puppet.</span><span class="sxs-lookup"><span data-stu-id="dd141-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="dd141-125">L’extension VMAccess exécute un script comme racine de la même manière à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="dd141-125">VMAccess Extension executes a script as root in the same way using SSH can.</span></span> <span data-ttu-id="dd141-126">Cependant, l’utilisation de l’extension de machine virtuelle active plusieurs fonctionnalités qu’Azure offre qui peuvent être utiles selon votre scénario.</span><span class="sxs-lookup"><span data-stu-id="dd141-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="dd141-127">Disponibilité de cloud-init lors de la création d’alias d’images de machine virtuelle Azure :</span><span class="sxs-lookup"><span data-stu-id="dd141-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="dd141-128">Alias</span><span class="sxs-lookup"><span data-stu-id="dd141-128">Alias</span></span> | <span data-ttu-id="dd141-129">Éditeur</span><span class="sxs-lookup"><span data-stu-id="dd141-129">Publisher</span></span> | <span data-ttu-id="dd141-130">Offer</span><span class="sxs-lookup"><span data-stu-id="dd141-130">Offer</span></span> | <span data-ttu-id="dd141-131">SKU</span><span class="sxs-lookup"><span data-stu-id="dd141-131">SKU</span></span> | <span data-ttu-id="dd141-132">Version</span><span class="sxs-lookup"><span data-stu-id="dd141-132">Version</span></span> | <span data-ttu-id="dd141-133">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="dd141-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd141-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="dd141-134">CentOS</span></span> |<span data-ttu-id="dd141-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="dd141-135">OpenLogic</span></span> |<span data-ttu-id="dd141-136">Centos</span><span class="sxs-lookup"><span data-stu-id="dd141-136">Centos</span></span> |<span data-ttu-id="dd141-137">7,2</span><span class="sxs-lookup"><span data-stu-id="dd141-137">7.2</span></span> |<span data-ttu-id="dd141-138">le plus récent</span><span class="sxs-lookup"><span data-stu-id="dd141-138">latest</span></span> |<span data-ttu-id="dd141-139">no</span><span class="sxs-lookup"><span data-stu-id="dd141-139">no</span></span> |
| <span data-ttu-id="dd141-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="dd141-140">CoreOS</span></span> |<span data-ttu-id="dd141-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="dd141-141">CoreOS</span></span> |<span data-ttu-id="dd141-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="dd141-142">CoreOS</span></span> |<span data-ttu-id="dd141-143">Stable</span><span class="sxs-lookup"><span data-stu-id="dd141-143">Stable</span></span> |<span data-ttu-id="dd141-144">le plus récent</span><span class="sxs-lookup"><span data-stu-id="dd141-144">latest</span></span> |<span data-ttu-id="dd141-145">yes</span><span class="sxs-lookup"><span data-stu-id="dd141-145">yes</span></span> |
| <span data-ttu-id="dd141-146">Debian</span><span class="sxs-lookup"><span data-stu-id="dd141-146">Debian</span></span> |<span data-ttu-id="dd141-147">credativ</span><span class="sxs-lookup"><span data-stu-id="dd141-147">credativ</span></span> |<span data-ttu-id="dd141-148">Debian</span><span class="sxs-lookup"><span data-stu-id="dd141-148">Debian</span></span> |<span data-ttu-id="dd141-149">8</span><span class="sxs-lookup"><span data-stu-id="dd141-149">8</span></span> |<span data-ttu-id="dd141-150">le plus récent</span><span class="sxs-lookup"><span data-stu-id="dd141-150">latest</span></span> |<span data-ttu-id="dd141-151">no</span><span class="sxs-lookup"><span data-stu-id="dd141-151">no</span></span> |
| <span data-ttu-id="dd141-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="dd141-152">openSUSE</span></span> |<span data-ttu-id="dd141-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="dd141-153">SUSE</span></span> |<span data-ttu-id="dd141-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="dd141-154">openSUSE</span></span> |<span data-ttu-id="dd141-155">13.2</span><span class="sxs-lookup"><span data-stu-id="dd141-155">13.2</span></span> |<span data-ttu-id="dd141-156">le plus récent</span><span class="sxs-lookup"><span data-stu-id="dd141-156">latest</span></span> |<span data-ttu-id="dd141-157">no</span><span class="sxs-lookup"><span data-stu-id="dd141-157">no</span></span> |
| <span data-ttu-id="dd141-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="dd141-158">RHEL</span></span> |<span data-ttu-id="dd141-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="dd141-159">Redhat</span></span> |<span data-ttu-id="dd141-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="dd141-160">RHEL</span></span> |<span data-ttu-id="dd141-161">7,2</span><span class="sxs-lookup"><span data-stu-id="dd141-161">7.2</span></span> |<span data-ttu-id="dd141-162">le plus récent</span><span class="sxs-lookup"><span data-stu-id="dd141-162">latest</span></span> |<span data-ttu-id="dd141-163">no</span><span class="sxs-lookup"><span data-stu-id="dd141-163">no</span></span> |
| <span data-ttu-id="dd141-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="dd141-164">UbuntuLTS</span></span> |<span data-ttu-id="dd141-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="dd141-165">Canonical</span></span> |<span data-ttu-id="dd141-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="dd141-166">UbuntuServer</span></span> |<span data-ttu-id="dd141-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="dd141-167">14.04.4-LTS</span></span> |<span data-ttu-id="dd141-168">le plus récent</span><span class="sxs-lookup"><span data-stu-id="dd141-168">latest</span></span> |<span data-ttu-id="dd141-169">Oui</span><span class="sxs-lookup"><span data-stu-id="dd141-169">yes</span></span> |

<span data-ttu-id="dd141-170">Nous collaborons avec nos partenaires pour que cloud-init soit inclus et fonctionne dans les images qu’ils fournissent à Azure.</span><span class="sxs-lookup"><span data-stu-id="dd141-170">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="dd141-171">Ajouter un script cloud-init à la création d’une machine virtuelle avec l’interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="dd141-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="dd141-172">Pour lancer un script cloud-init lors de la création d'une machine virtuelle dans Azure, spécifiez le fichier cloud-init à l'aide du commutateur d’interface de ligne de commande Azure `--custom-data` .</span><span class="sxs-lookup"><span data-stu-id="dd141-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="dd141-173">Créez un groupe de ressources pour y lancer des machines virtuelles avec [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="dd141-173">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="dd141-174">L’exemple suivant permet de créer le groupe de ressources nommé *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="dd141-174">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="dd141-175">Créez une machine virtuelle Linux à configurer au cours de démarrage avec [az vm create](/cli/azure/vm#create) à l’aide de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="dd141-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="dd141-176">Créer un script cloud-init pour définir le nom d’hôte d’une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="dd141-176">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="dd141-177">Le nom d’hôte est l’un des paramètres les plus simples et les plus importants pour une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="dd141-177">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="dd141-178">Nous pouvons facilement définir ce paramètre en utilisant cloud-init avec ce script.</span><span class="sxs-lookup"><span data-stu-id="dd141-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="dd141-179">Exemple de script cloud-init nommé `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="dd141-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="dd141-180">Lors du démarrage initial de la machine virtuelle, ce script cloud-init définit le nom d'hôte sur *myservername*.</span><span class="sxs-lookup"><span data-stu-id="dd141-180">During the initial startup of the VM, this cloud-init script sets the hostname to *myservername*.</span></span> <span data-ttu-id="dd141-181">Créez une machine virtuelle Linux à configurer au cours de démarrage avec [az vm create](/cli/azure/vm#create) à l’aide de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="dd141-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="dd141-182">Connectez-vous et vérifiez le nom d'hôte de la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dd141-182">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="dd141-183">Création d’un script cloud-init</span><span class="sxs-lookup"><span data-stu-id="dd141-183">Create a cloud-init script</span></span>
<span data-ttu-id="dd141-184">Pour des questions de sécurité, configurez votre machine virtuelle Ubuntu de manière à ce qu’elle se mette à jour au premier démarrage.</span><span class="sxs-lookup"><span data-stu-id="dd141-184">For security, you want your Ubuntu VM to update on the first boot.</span></span> <span data-ttu-id="dd141-185">À l'aide de cloud-init, nous pouvons le faire avec le script suivant, en fonction de la distribution Linux que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="dd141-185">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="dd141-186">Exemple de script cloud-init `cloud_config_apt_upgrade.txt` pour la famille Debian</span><span class="sxs-lookup"><span data-stu-id="dd141-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="dd141-187">Une fois Linux démarré, tous les packages installés sont mis à jour par le biais d’**apt-get**.</span><span class="sxs-lookup"><span data-stu-id="dd141-187">After Linux has booted, all the installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="dd141-188">Créez une machine virtuelle Linux à configurer au cours de démarrage avec [az vm create](/cli/azure/vm#create) à l’aide de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="dd141-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="dd141-189">Connectez-vous et vérifiez que tous les packages sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="dd141-189">Login and verify all packages are updated.</span></span>

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

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="dd141-190">Créer un script cloud-init pour ajouter un utilisateur à Linux</span><span class="sxs-lookup"><span data-stu-id="dd141-190">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="dd141-191">L’une des premières tâches liées à n'importe quelle nouvelle machine virtuelle Linux consiste à ajouter un utilisateur pour vous-même ou à éviter d'utiliser *root*.</span><span class="sxs-lookup"><span data-stu-id="dd141-191">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using *root*.</span></span> <span data-ttu-id="dd141-192">Les clés SSH sont la meilleure pratique en matière de sécurité et de facilité d’utilisation. Elles sont ajoutées au fichier *~/.ssh/authorized_keys* avec ce script cloud-init.</span><span class="sxs-lookup"><span data-stu-id="dd141-192">SSH keys are best practice for security and for usability and they are added to the *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="dd141-193">Exemple de script cloud-init `cloud_config_add_users.txt` pour la famille Debian</span><span class="sxs-lookup"><span data-stu-id="dd141-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="dd141-194">Une fois Linux démarré, tous les utilisateurs répertoriés sont créés et ajoutés au groupe sudo.</span><span class="sxs-lookup"><span data-stu-id="dd141-194">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="dd141-195">Créez une machine virtuelle Linux à configurer au cours de démarrage avec [az vm create](/cli/azure/vm#create) à l’aide de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="dd141-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="dd141-196">Connectez-vous et vérifiez l’utilisateur qui vient d’être créé.</span><span class="sxs-lookup"><span data-stu-id="dd141-196">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="dd141-197">Sortie</span><span class="sxs-lookup"><span data-stu-id="dd141-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="dd141-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dd141-198">Next steps</span></span>
<span data-ttu-id="dd141-199">Cloud-init est devenu une méthode standard pour modifier votre machine virtuelle Linux au démarrage.</span><span class="sxs-lookup"><span data-stu-id="dd141-199">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="dd141-200">Azure propose également des extensions de machine virtuelle, ce qui vous permet de modifier votre machine virtuelle Linux au démarrage ou pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="dd141-200">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="dd141-201">Par exemple, vous pouvez utiliser la VMAccessExtension Azure pour réinitialiser les informations de SSH ou de l’utilisateur pendant l’exécution de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dd141-201">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="dd141-202">Avec cloud-init, vous devez effectuer un redémarrage pour réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="dd141-202">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="dd141-203">À propos des extensions et des fonctionnalités des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="dd141-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="dd141-204">Gérer les utilisateurs, SSH et vérifier ou réparer les disques de machines virtuelles Azure Linux à l'aide de l’extension VMAccess</span><span class="sxs-lookup"><span data-stu-id="dd141-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md)