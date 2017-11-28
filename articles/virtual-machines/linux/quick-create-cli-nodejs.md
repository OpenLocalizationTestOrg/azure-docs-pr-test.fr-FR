---
title: "Création d’une machine virtuelle Linux à l’aide d’Azure CLI 1.0 | Microsoft Docs"
description: "Créer une machine virtuelle Linux sur Azure à l’aide de l’interface Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
ms.assetid: facb1115-2b4e-4ef3-9905-330e42beb686
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2016
ms.author: v-livech
ms.openlocfilehash: ec1b34e4f539d2e95bb1f99fca3a6a0ec682ef51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="5b05d-103">Création d'une machine virtuelle Linux à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5b05d-103">Create a Linux VM using the Azure CLI 1.0</span></span>

<span data-ttu-id="5b05d-104">Cet article explique comment déployer rapidement une machine virtuelle Linux sur Azure à l’aide de la commande `azure vm quick-create` dans l’interface de ligne de commande (CLI) Azure.</span><span class="sxs-lookup"><span data-stu-id="5b05d-104">This article shows how to quickly deploy a Linux virtual machine (VM) on Azure by using the `azure vm quick-create` command in the Azure command-line interface (CLI).</span></span> <span data-ttu-id="5b05d-105">La commande `quick-create` déploie une machine virtuelle à l’intérieur d’une infrastructure sécurisée de base que vous pouvez utiliser comme prototype ou pour tester rapidement un concept.</span><span class="sxs-lookup"><span data-stu-id="5b05d-105">The `quick-create` command deploys a VM inside a basic, secure infrastructure that you can use to prototype or test a concept rapidly.</span></span>

> [!NOTE]
<span data-ttu-id="5b05d-106">Pour créer une machine virtuelle à l’aide d’Azure CLI 2.0, consultez [Créer une machine virtuelle à l’aide de l’interface de ligne de commande (CLI) Azure](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b05d-106">To create a VM using the Azure CLI 2.0, see [Create a VM with the Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="5b05d-107">Vous pouvez également déployer rapidement une machine virtuelle Linux à l’aide du [Portail Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b05d-107">You can also quickly deploy a Linux VM by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="5b05d-108">L’article nécessite des [fichiers de clés SSH publiques et privées](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b05d-108">The article requires an [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="quick-commands"></a><span data-ttu-id="5b05d-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="5b05d-109">Quick commands</span></span>

<span data-ttu-id="5b05d-110">L’exemple suivant montre comment déployer une machine virtuelle CoreOS et comment attacher votre clé SSH (Secure Shell) (vos arguments peuvent être différents) :</span><span class="sxs-lookup"><span data-stu-id="5b05d-110">The following example shows how to deploy a CoreOS VM and attach your Secure Shell (SSH) key (your arguments might be different):</span></span>

```azurecli
azure vm quick-create -M ~/.ssh/id_rsa.pub -Q CoreOS
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="5b05d-111">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="5b05d-111">Detailed walkthrough</span></span>

<span data-ttu-id="5b05d-112">La procédure suivante déploie une machine virtuelle Ubuntu LTS, étape par étape, avec des explications sur le rôle de chaque étape.</span><span class="sxs-lookup"><span data-stu-id="5b05d-112">The following walkthrough has an UbuntuLTS VM being deployed, step by step, with explanations of what each step is doing.</span></span>

## <a name="vm-quick-create-aliases"></a><span data-ttu-id="5b05d-113">Alias de création rapide de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5b05d-113">VM quick-create aliases</span></span>

<span data-ttu-id="5b05d-114">Un moyen rapide de choisir une distribution consiste à utiliser les alias d’interface de ligne de commande Azure mappés sur les distributions de système d’exploitation les plus courantes.</span><span class="sxs-lookup"><span data-stu-id="5b05d-114">A quick way to choose a distribution is to use the Azure CLI aliases mapped to the most common OS distributions.</span></span> <span data-ttu-id="5b05d-115">Le tableau suivant répertorie les alias (à partir de la version 0.10 de l’interface de ligne de commande Azure).</span><span class="sxs-lookup"><span data-stu-id="5b05d-115">The following table lists the aliases (as of Azure CLI version 0.10).</span></span> <span data-ttu-id="5b05d-116">Tous les déploiements qui utilisent `quick-create` par défaut sur les machines virtuelles prises en charge par le stockage SSD, et qui offrent un approvisionnement plus rapide et un accès au disque hautes performances.</span><span class="sxs-lookup"><span data-stu-id="5b05d-116">All deployments that use `quick-create` default to VMs that are backed by solid-state drive (SSD) storage, which offers faster provisioning and high-performance disk access.</span></span> <span data-ttu-id="5b05d-117">(Ces alias représentent une infime partie des distributions disponibles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5b05d-117">(These aliases represent a tiny portion of the available distributions on Azure.</span></span> <span data-ttu-id="5b05d-118">Trouvez d’autres images dans Azure Marketplace en [recherchant une image dans PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [sur le Web](https://azure.microsoft.com/marketplace/virtual-machines/) ou en [chargeant votre image personnalisée](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span><span class="sxs-lookup"><span data-stu-id="5b05d-118">Find more images in the Azure Marketplace by [searching for an image in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [on the web](https://azure.microsoft.com/marketplace/virtual-machines/), or [upload your own custom image](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span></span>

| <span data-ttu-id="5b05d-119">Alias</span><span class="sxs-lookup"><span data-stu-id="5b05d-119">Alias</span></span> | <span data-ttu-id="5b05d-120">Éditeur</span><span class="sxs-lookup"><span data-stu-id="5b05d-120">Publisher</span></span> | <span data-ttu-id="5b05d-121">Offer</span><span class="sxs-lookup"><span data-stu-id="5b05d-121">Offer</span></span> | <span data-ttu-id="5b05d-122">SKU</span><span class="sxs-lookup"><span data-stu-id="5b05d-122">SKU</span></span> | <span data-ttu-id="5b05d-123">Version</span><span class="sxs-lookup"><span data-stu-id="5b05d-123">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="5b05d-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="5b05d-124">CentOS</span></span> |<span data-ttu-id="5b05d-125">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="5b05d-125">OpenLogic</span></span> |<span data-ttu-id="5b05d-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="5b05d-126">CentOS</span></span> |<span data-ttu-id="5b05d-127">7,2</span><span class="sxs-lookup"><span data-stu-id="5b05d-127">7.2</span></span> |<span data-ttu-id="5b05d-128">le plus récent</span><span class="sxs-lookup"><span data-stu-id="5b05d-128">latest</span></span> |
| <span data-ttu-id="5b05d-129">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5b05d-129">CoreOS</span></span> |<span data-ttu-id="5b05d-130">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5b05d-130">CoreOS</span></span> |<span data-ttu-id="5b05d-131">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5b05d-131">CoreOS</span></span> |<span data-ttu-id="5b05d-132">Stable</span><span class="sxs-lookup"><span data-stu-id="5b05d-132">Stable</span></span> |<span data-ttu-id="5b05d-133">le plus récent</span><span class="sxs-lookup"><span data-stu-id="5b05d-133">latest</span></span> |
| <span data-ttu-id="5b05d-134">Debian</span><span class="sxs-lookup"><span data-stu-id="5b05d-134">Debian</span></span> |<span data-ttu-id="5b05d-135">credativ</span><span class="sxs-lookup"><span data-stu-id="5b05d-135">credativ</span></span> |<span data-ttu-id="5b05d-136">Debian</span><span class="sxs-lookup"><span data-stu-id="5b05d-136">Debian</span></span> |<span data-ttu-id="5b05d-137">8</span><span class="sxs-lookup"><span data-stu-id="5b05d-137">8</span></span> |<span data-ttu-id="5b05d-138">le plus récent</span><span class="sxs-lookup"><span data-stu-id="5b05d-138">latest</span></span> |
| <span data-ttu-id="5b05d-139">openSUSE</span><span class="sxs-lookup"><span data-stu-id="5b05d-139">openSUSE</span></span> |<span data-ttu-id="5b05d-140">SUSE</span><span class="sxs-lookup"><span data-stu-id="5b05d-140">SUSE</span></span> |<span data-ttu-id="5b05d-141">openSUSE</span><span class="sxs-lookup"><span data-stu-id="5b05d-141">openSUSE</span></span> |<span data-ttu-id="5b05d-142">13.2</span><span class="sxs-lookup"><span data-stu-id="5b05d-142">13.2</span></span> |<span data-ttu-id="5b05d-143">le plus récent</span><span class="sxs-lookup"><span data-stu-id="5b05d-143">latest</span></span> |
| <span data-ttu-id="5b05d-144">RHEL</span><span class="sxs-lookup"><span data-stu-id="5b05d-144">RHEL</span></span> |<span data-ttu-id="5b05d-145">Red Hat</span><span class="sxs-lookup"><span data-stu-id="5b05d-145">Red Hat</span></span> |<span data-ttu-id="5b05d-146">RHEL</span><span class="sxs-lookup"><span data-stu-id="5b05d-146">RHEL</span></span> |<span data-ttu-id="5b05d-147">7,2</span><span class="sxs-lookup"><span data-stu-id="5b05d-147">7.2</span></span> |<span data-ttu-id="5b05d-148">le plus récent</span><span class="sxs-lookup"><span data-stu-id="5b05d-148">latest</span></span> |
| <span data-ttu-id="5b05d-149">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="5b05d-149">UbuntuLTS</span></span> |<span data-ttu-id="5b05d-150">Canonical</span><span class="sxs-lookup"><span data-stu-id="5b05d-150">Canonical</span></span> |<span data-ttu-id="5b05d-151">Serveur Ubuntu</span><span class="sxs-lookup"><span data-stu-id="5b05d-151">Ubuntu Server</span></span> |<span data-ttu-id="5b05d-152">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="5b05d-152">14.04.4-LTS</span></span> |<span data-ttu-id="5b05d-153">le plus récent</span><span class="sxs-lookup"><span data-stu-id="5b05d-153">latest</span></span> |

<span data-ttu-id="5b05d-154">Les sections suivantes utilisent l’alias `UbuntuLTS` pour l’option **ImageURN** (`-Q`) afin de déployer un serveur Ubuntu 14.04.4 LTS.</span><span class="sxs-lookup"><span data-stu-id="5b05d-154">The following sections use the `UbuntuLTS` alias for the **ImageURN** option (`-Q`) to deploy an Ubuntu 14.04.4 LTS Server.</span></span>

<span data-ttu-id="5b05d-155">Le précédent exemple `quick-create` appelait uniquement l’indicateur `-M` pour identifier la clé publique SSH à charger lors de la désactivation des mots de passe SSH. Par conséquent, vous êtes invité à entrer les arguments suivants :</span><span class="sxs-lookup"><span data-stu-id="5b05d-155">The previous `quick-create` example only called out the `-M` flag to identify the SSH public key to upload while disabling SSH passwords, so you are prompted for the following arguments:</span></span>

* <span data-ttu-id="5b05d-156">nom du groupe de ressources (toute chaîne convient généralement pour votre premier groupe de ressources Azure)</span><span class="sxs-lookup"><span data-stu-id="5b05d-156">resource group name (any string is typically fine for your first Azure resource group)</span></span>
* <span data-ttu-id="5b05d-157">Nom de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5b05d-157">VM name</span></span>
* <span data-ttu-id="5b05d-158">emplacement (`westus` ou `westeurope` sont des valeurs par défaut appropriées)</span><span class="sxs-lookup"><span data-stu-id="5b05d-158">location (`westus` or `westeurope` are good defaults)</span></span>
* <span data-ttu-id="5b05d-159">linux (pour indiquer à Azure le système d’exploitation souhaité)</span><span class="sxs-lookup"><span data-stu-id="5b05d-159">linux (to let Azure know which OS you want)</span></span>
* <span data-ttu-id="5b05d-160">username</span><span class="sxs-lookup"><span data-stu-id="5b05d-160">username</span></span>

<span data-ttu-id="5b05d-161">L’exemple suivant spécifie toutes les valeurs, ainsi aucune autre invite n’est requise.</span><span class="sxs-lookup"><span data-stu-id="5b05d-161">The following example specifies all the values so that no further prompting is required.</span></span> <span data-ttu-id="5b05d-162">Dans la mesure où vous avez un `~/.ssh/id_rsa.pub` en tant que fichier de clé publique au format ssh-rsa, il fonctionne comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b05d-162">So long as you have an `~/.ssh/id_rsa.pub` as a ssh-rsa format public key file, it works as is:</span></span>

```azurecli
azure vm quick-create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --admin-username myAdminUser \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --image-urn UbuntuLTS
```

<span data-ttu-id="5b05d-163">La sortie doit ressembler au bloc de sortie suivant :</span><span class="sxs-lookup"><span data-stu-id="5b05d-163">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command vm quick-create
+ Listing virtual machine sizes available in the location "westus"
+ Looking up the VM "myVM"
info:    Verifying the public key SSH file: /Users/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account cli16330708391032639673
+ Looking up the NIC "examp-westu-1633070839-nic"
info:    An nic with given name "examp-westu-1633070839-nic" not found, creating a new one
+ Looking up the virtual network "examp-westu-1633070839-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "examp-westu-1633070839-vnet" [address prefix: "10.0.0.0/16"] with subnet "examp-westu-1633070839-snet" [address prefix: "10.+.1.0/24"]
+ Looking up the virtual network "examp-westu-1633070839-vnet"
+ Looking up the subnet "examp-westu-1633070839-snet" under the virtual network "examp-westu-1633070839-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "examp-westu-1633070839-pip"
info:    PublicIP with given name "examp-westu-1633070839-pip" not found, creating a new one
+ Creating public ip "examp-westu-1633070839-pip"
+ Looking up the public ip "examp-westu-1633070839-pip"
+ Creating NIC "examp-westu-1633070839-nic"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the storage account clisto1710997031examplev
+ Creating VM "myVM"
+ Looking up the VM "myVM"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the public ip "examp-westu-1633070839-pip"
data:    Id                              :/subscriptions/2<--snip-->d/resourceGroups/exampleResourceGroup/providers/Microsoft.Compute/virtualMachines/exampleVMName
data:    ProvisioningState               :Succeeded
data:    Name                            :exampleVMName
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :Canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :14.04.4-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clic7fadb847357e9cf-os-1473374894359
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli16330708391032639673.blob.core.windows.net/vhds/clic7fadb847357e9cf-os-1473374894359.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM
data:      User Name                     :myAdminUser
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-42-FB
data:          Provisioning State        :Succeeded
data:          Name                      :examp-westu-1633070839-nic
data:          Location                  :westus
data:            Public IP address       :138.91.247.29
data:            FQDN                    :examp-westu-1633070839-pip.westus.cloudapp.azure.com
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://clisto1710997031examplev.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm quick-create command OK
```

## <a name="log-in-to-the-new-vm"></a><span data-ttu-id="5b05d-164">Se connecter à la nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5b05d-164">Log in to the new VM</span></span>
<span data-ttu-id="5b05d-165">Connectez-vous à votre machine virtuelle à l’aide de l’adresse IP publique répertoriée dans la sortie.</span><span class="sxs-lookup"><span data-stu-id="5b05d-165">Log in to your VM by using the public IP address listed in the output.</span></span> <span data-ttu-id="5b05d-166">Vous pouvez également utiliser le nom de domaine complet (FQDN) répertorié :</span><span class="sxs-lookup"><span data-stu-id="5b05d-166">You can also use the fully qualified domain name (FQDN) that's listed:</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub ahmet@138.91.247.29
```

<span data-ttu-id="5b05d-167">Le processus de connexion doit ressembler au bloc de sortie suivant :</span><span class="sxs-lookup"><span data-stu-id="5b05d-167">The login process should look something like the following output block:</span></span>

```bash
Warning: Permanently added '138.91.247.29' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Sep  8 22:50:57 UTC 2016

  System load: 0.63              Memory usage: 2%   Processes:       81
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

myAdminUser@myVM:~$
```

## <a name="next-steps"></a><span data-ttu-id="5b05d-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b05d-168">Next steps</span></span>
<span data-ttu-id="5b05d-169">La commande `azure vm quick-create` permet de déployer rapidement une machine virtuelle pour se connecter à un shell bash et être opérationnel.</span><span class="sxs-lookup"><span data-stu-id="5b05d-169">The `azure vm quick-create` command is the way to quickly deploy a VM so you can log in to a bash shell and get working.</span></span> <span data-ttu-id="5b05d-170">Toutefois, l’utilisation de `vm quick-create` ne vous confère pas un contrôle étendu et ne vous permet pas de créer un environnement plus complexe.</span><span class="sxs-lookup"><span data-stu-id="5b05d-170">However, using `vm quick-create` does not give you extensive control nor does it enable you to create a more complex environment.</span></span>  <span data-ttu-id="5b05d-171">Pour déployer une machine virtuelle Linux personnalisée en fonction de votre infrastructure, lisez l’un des articles ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b05d-171">To deploy a Linux VM that's customized for your infrastructure, you can follow any of these articles:</span></span>

* [<span data-ttu-id="5b05d-172">Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement</span><span class="sxs-lookup"><span data-stu-id="5b05d-172">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="5b05d-173">Création d’une machine virtuelle Linux sécurisée par SSH dans Azure à l’aide de modèles</span><span class="sxs-lookup"><span data-stu-id="5b05d-173">Create an SSH Secured Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="5b05d-174">Vous pouvez également [utiliser le pilote Azure `docker-machine` avec plusieurs commandes pour créer rapidement une machine virtuelle Linux comme hôte docker](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b05d-174">You can also [use the `docker-machine` Azure driver with various commands to quickly create a Linux VM as a docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>