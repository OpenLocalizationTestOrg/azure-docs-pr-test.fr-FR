---
title: aaaUse cloud-init toocustomize un VM Linux | Documents Microsoft
description: "Comment toocustomize du cloud-init toouse a Linux VM lors de la création avec hello Azure CLI 2.0"
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
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a><span data-ttu-id="4da66-103">Utiliser le nuage-init toocustomize un VM Linux lors de la création</span><span class="sxs-lookup"><span data-stu-id="4da66-103">Use cloud-init toocustomize a Linux VM during creation</span></span>
<span data-ttu-id="4da66-104">Cet article vous explique comment toomake un tooset de script cloud-init hello nom d’hôte, mettre à jour les packages installés et gérer des comptes d’utilisateur avec hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="4da66-104">This article shows you how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts with hello Azure CLI 2.0.</span></span> <span data-ttu-id="4da66-105">scripts d’initialisation de cloud Hello sont appelées lorsque vous créez un ordinateur virtuel (VM) à partir de CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="4da66-105">hello cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="4da66-106">Pour une présentation plus détaillée de l’installation d’applications, l’écriture de fichiers de configuration et l’injection de clés à partir de Key Vault, consultez [ce didacticiel](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="4da66-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="4da66-107">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4da66-107">You can also perform these steps with hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="4da66-108">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="4da66-108">Quick commands</span></span>
<span data-ttu-id="4da66-109">Créer un script de init.txt de cloud qui définit le nom d’hôte hello, tous les packages de mises à jour et ajoute un tooLinux d’utilisateur sudo.</span><span class="sxs-lookup"><span data-stu-id="4da66-109">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

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

<span data-ttu-id="4da66-110">Créer un toolaunch de groupe de ressources avec des machines virtuelles dans [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4da66-110">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4da66-111">groupe de ressources hello nommé crée Hello suivant *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="4da66-111">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4da66-112">Créer une VM Linux avec [az vm créer](/cli/azure/vm#create) à l’aide de cloud-init tooconfigure il pendant le démarrage avec hello `--custom-data` paramètre.</span><span class="sxs-lookup"><span data-stu-id="4da66-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot with hello `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="4da66-113">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="4da66-113">Detailed walkthrough</span></span>
<span data-ttu-id="4da66-114">Lorsque vous lancez une nouvelle machine virtuelle Linux, vous obtenez une machine virtuelle Linux standard, non personnalisée ni adaptée à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="4da66-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="4da66-115">[Init-cloud](https://cloudinit.readthedocs.org) est un moyen standard de tooinject paramètres de script ou de configuration dans cette VM Linux comme il démarre hello pour la première fois.</span><span class="sxs-lookup"><span data-stu-id="4da66-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="4da66-116">Sur Azure, il existe différentes manières de modifications toomake sur un VM Linux qu’il est déployé ou démarré.</span><span class="sxs-lookup"><span data-stu-id="4da66-116">On Azure, there are a few different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="4da66-117">Injectez des scripts à l’aide de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="4da66-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="4da66-118">Injection de scripts à l’aide de hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="4da66-118">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="4da66-119">Un modèle Azure utilisant cloud-init.</span><span class="sxs-lookup"><span data-stu-id="4da66-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="4da66-120">Un modèle Azure utilisant [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="4da66-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="4da66-121">scripts de tooinject à tout moment après le démarrage :</span><span class="sxs-lookup"><span data-stu-id="4da66-121">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="4da66-122">Commandes de toorun SSH directement</span><span class="sxs-lookup"><span data-stu-id="4da66-122">SSH toorun commands directly</span></span>
* <span data-ttu-id="4da66-123">Injection de scripts à l’aide de hello Azure [VMAccess Extension](using-vmaccess-extension.md), impérative ou dans un modèle Azure</span><span class="sxs-lookup"><span data-stu-id="4da66-123">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="4da66-124">Des outils de gestion de la configuration tels qu’Ansible, Salt, Chef et Puppet.</span><span class="sxs-lookup"><span data-stu-id="4da66-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="4da66-125">Le VMAccess Extension exécute un script comme racine Bonjour même peut de façon à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="4da66-125">VMAccess Extension executes a script as root in hello same way using SSH can.</span></span> <span data-ttu-id="4da66-126">Toutefois, extension de machine virtuelle hello grâce à plusieurs fonctionnalités que les offres Azure qui peuvent être utile en fonction de votre scénario.</span><span class="sxs-lookup"><span data-stu-id="4da66-126">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="4da66-127">Disponibilité de cloud-init lors de la création d’alias d’images de machine virtuelle Azure :</span><span class="sxs-lookup"><span data-stu-id="4da66-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="4da66-128">Alias</span><span class="sxs-lookup"><span data-stu-id="4da66-128">Alias</span></span> | <span data-ttu-id="4da66-129">Éditeur</span><span class="sxs-lookup"><span data-stu-id="4da66-129">Publisher</span></span> | <span data-ttu-id="4da66-130">Offer</span><span class="sxs-lookup"><span data-stu-id="4da66-130">Offer</span></span> | <span data-ttu-id="4da66-131">SKU</span><span class="sxs-lookup"><span data-stu-id="4da66-131">SKU</span></span> | <span data-ttu-id="4da66-132">Version</span><span class="sxs-lookup"><span data-stu-id="4da66-132">Version</span></span> | <span data-ttu-id="4da66-133">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="4da66-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="4da66-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="4da66-134">CentOS</span></span> |<span data-ttu-id="4da66-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="4da66-135">OpenLogic</span></span> |<span data-ttu-id="4da66-136">Centos</span><span class="sxs-lookup"><span data-stu-id="4da66-136">Centos</span></span> |<span data-ttu-id="4da66-137">7,2</span><span class="sxs-lookup"><span data-stu-id="4da66-137">7.2</span></span> |<span data-ttu-id="4da66-138">le plus récent</span><span class="sxs-lookup"><span data-stu-id="4da66-138">latest</span></span> |<span data-ttu-id="4da66-139">no</span><span class="sxs-lookup"><span data-stu-id="4da66-139">no</span></span> |
| <span data-ttu-id="4da66-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4da66-140">CoreOS</span></span> |<span data-ttu-id="4da66-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4da66-141">CoreOS</span></span> |<span data-ttu-id="4da66-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4da66-142">CoreOS</span></span> |<span data-ttu-id="4da66-143">Stable</span><span class="sxs-lookup"><span data-stu-id="4da66-143">Stable</span></span> |<span data-ttu-id="4da66-144">le plus récent</span><span class="sxs-lookup"><span data-stu-id="4da66-144">latest</span></span> |<span data-ttu-id="4da66-145">yes</span><span class="sxs-lookup"><span data-stu-id="4da66-145">yes</span></span> |
| <span data-ttu-id="4da66-146">Debian</span><span class="sxs-lookup"><span data-stu-id="4da66-146">Debian</span></span> |<span data-ttu-id="4da66-147">credativ</span><span class="sxs-lookup"><span data-stu-id="4da66-147">credativ</span></span> |<span data-ttu-id="4da66-148">Debian</span><span class="sxs-lookup"><span data-stu-id="4da66-148">Debian</span></span> |<span data-ttu-id="4da66-149">8</span><span class="sxs-lookup"><span data-stu-id="4da66-149">8</span></span> |<span data-ttu-id="4da66-150">le plus récent</span><span class="sxs-lookup"><span data-stu-id="4da66-150">latest</span></span> |<span data-ttu-id="4da66-151">no</span><span class="sxs-lookup"><span data-stu-id="4da66-151">no</span></span> |
| <span data-ttu-id="4da66-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="4da66-152">openSUSE</span></span> |<span data-ttu-id="4da66-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="4da66-153">SUSE</span></span> |<span data-ttu-id="4da66-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="4da66-154">openSUSE</span></span> |<span data-ttu-id="4da66-155">13.2</span><span class="sxs-lookup"><span data-stu-id="4da66-155">13.2</span></span> |<span data-ttu-id="4da66-156">le plus récent</span><span class="sxs-lookup"><span data-stu-id="4da66-156">latest</span></span> |<span data-ttu-id="4da66-157">no</span><span class="sxs-lookup"><span data-stu-id="4da66-157">no</span></span> |
| <span data-ttu-id="4da66-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="4da66-158">RHEL</span></span> |<span data-ttu-id="4da66-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="4da66-159">Redhat</span></span> |<span data-ttu-id="4da66-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="4da66-160">RHEL</span></span> |<span data-ttu-id="4da66-161">7,2</span><span class="sxs-lookup"><span data-stu-id="4da66-161">7.2</span></span> |<span data-ttu-id="4da66-162">le plus récent</span><span class="sxs-lookup"><span data-stu-id="4da66-162">latest</span></span> |<span data-ttu-id="4da66-163">no</span><span class="sxs-lookup"><span data-stu-id="4da66-163">no</span></span> |
| <span data-ttu-id="4da66-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="4da66-164">UbuntuLTS</span></span> |<span data-ttu-id="4da66-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="4da66-165">Canonical</span></span> |<span data-ttu-id="4da66-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="4da66-166">UbuntuServer</span></span> |<span data-ttu-id="4da66-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="4da66-167">14.04.4-LTS</span></span> |<span data-ttu-id="4da66-168">le plus récent</span><span class="sxs-lookup"><span data-stu-id="4da66-168">latest</span></span> |<span data-ttu-id="4da66-169">yes</span><span class="sxs-lookup"><span data-stu-id="4da66-169">yes</span></span> |

<span data-ttu-id="4da66-170">Nous sommes utilisation de nos partenaires tooget cloud-init inclus et utilisation dans des images hello qu’ils fournissent des tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4da66-170">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="4da66-171">Ajouter une création d’ordinateurs virtuels cloud-init script toohello avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="4da66-171">Add a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="4da66-172">toolaunch un script d’initialisation de cloud lors de la création d’une machine virtuelle dans Azure, spécifiez le fichier de cloud-init de hello à l’aide de hello CLI d’Azure `--custom-data` basculer.</span><span class="sxs-lookup"><span data-stu-id="4da66-172">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="4da66-173">Créer un toolaunch de groupe de ressources avec des machines virtuelles dans [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4da66-173">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4da66-174">groupe de ressources hello nommé crée Hello suivant *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="4da66-174">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4da66-175">Créer une VM Linux avec [az vm créer](/cli/azure/vm#create) à l’aide de cloud-init tooconfigure il pendant le démarrage.</span><span class="sxs-lookup"><span data-stu-id="4da66-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="4da66-176">Créer un cloud-init script tooset hello nom d’hôte un VM Linux</span><span class="sxs-lookup"><span data-stu-id="4da66-176">Create a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="4da66-177">Un de hello plus simple et des paramètres importants pour n’importe quel VM Linux doit être nom d’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="4da66-177">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="4da66-178">Nous pouvons facilement définir ce paramètre en utilisant cloud-init avec ce script.</span><span class="sxs-lookup"><span data-stu-id="4da66-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="4da66-179">Exemple de script cloud-init nommé `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="4da66-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="4da66-180">Au démarrage initial de hello Hello machine virtuelle, ce script cloud-init définit hello hostname trop*MonNomDeServeur*.</span><span class="sxs-lookup"><span data-stu-id="4da66-180">During hello initial startup of hello VM, this cloud-init script sets hello hostname too*myservername*.</span></span> <span data-ttu-id="4da66-181">Créer une VM Linux avec [az vm créer](/cli/azure/vm#create) à l’aide de cloud-init tooconfigure il pendant le démarrage.</span><span class="sxs-lookup"><span data-stu-id="4da66-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="4da66-182">Connexion et vérifiez le nom d’hôte hello Hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4da66-182">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="4da66-183">Création d’un script cloud-init</span><span class="sxs-lookup"><span data-stu-id="4da66-183">Create a cloud-init script</span></span>
<span data-ttu-id="4da66-184">Pour la sécurité, vous souhaitez que votre tooupdate Ubuntu VM au premier démarrage de hello.</span><span class="sxs-lookup"><span data-stu-id="4da66-184">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span> <span data-ttu-id="4da66-185">À l’aide de cloud-init nous pouvons faire avec hello suivez script, en fonction de distribution de Linux hello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="4da66-185">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="4da66-186">Exemple de script cloud-init `cloud_config_apt_upgrade.txt` pour hello Debian famille</span><span class="sxs-lookup"><span data-stu-id="4da66-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="4da66-187">Une fois que Linux a démarré, tous les packages hello installé sont mis à jour **apt-get**.</span><span class="sxs-lookup"><span data-stu-id="4da66-187">After Linux has booted, all hello installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="4da66-188">Créer une VM Linux avec [az vm créer](/cli/azure/vm#create) à l’aide de cloud-init tooconfigure il pendant le démarrage.</span><span class="sxs-lookup"><span data-stu-id="4da66-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="4da66-189">Connectez-vous et vérifiez que tous les packages sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="4da66-189">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="4da66-190">Créer un tooadd de script cloud-init un tooLinux utilisateur</span><span class="sxs-lookup"><span data-stu-id="4da66-190">Create a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="4da66-191">Une des tâches de premier hello sur n’importe quel VM Linux nouvelle est tooadd un utilisateur pour vous-même ou à l’aide de tooavoid *racine*.</span><span class="sxs-lookup"><span data-stu-id="4da66-191">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using *root*.</span></span> <span data-ttu-id="4da66-192">Clés SSH sont meilleures pratiques pour la sécurité et de facilité d’utilisation et ils sont ajoutés toohello *~/.ssh/authorized_keys* fichier avec ce script init-cloud.</span><span class="sxs-lookup"><span data-stu-id="4da66-192">SSH keys are best practice for security and for usability and they are added toohello *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="4da66-193">Exemple de script cloud-init `cloud_config_add_users.txt` pour la famille Debian</span><span class="sxs-lookup"><span data-stu-id="4da66-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="4da66-194">Une fois que Linux a démarré, tous les utilisateurs de hello répertorié sont un groupe de sudo toohello créé et ajouté.</span><span class="sxs-lookup"><span data-stu-id="4da66-194">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span> <span data-ttu-id="4da66-195">Créer une VM Linux avec [az vm créer](/cli/azure/vm#create) à l’aide de cloud-init tooconfigure il pendant le démarrage.</span><span class="sxs-lookup"><span data-stu-id="4da66-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="4da66-196">Connexion et vérifier l’utilisateur de hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="4da66-196">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="4da66-197">Sortie</span><span class="sxs-lookup"><span data-stu-id="4da66-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="4da66-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4da66-198">Next steps</span></span>
<span data-ttu-id="4da66-199">Init-cloud devient un moyen standard toomodify votre VM Linux au démarrage du système.</span><span class="sxs-lookup"><span data-stu-id="4da66-199">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="4da66-200">Azure a également les extensions de machine virtuelle, ce qui vous toomodify votre LinuxVM au démarrage ou pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="4da66-200">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="4da66-201">Par exemple, vous pouvez utiliser hello Azure VMAccessExtension tooreset SSH ou les informations de l’utilisateur pendant l’exécution de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4da66-201">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="4da66-202">Avec cloud-init, vous aurez besoin d’un mot de passe de redémarrage tooreset hello.</span><span class="sxs-lookup"><span data-stu-id="4da66-202">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="4da66-203">À propos des extensions et des fonctionnalités des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="4da66-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="4da66-204">Gérer les utilisateurs, SSH et vérification ou de réparation des disques sur les machines virtuelles Azure Linux à l’aide de bienvenue de le VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="4da66-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md)
