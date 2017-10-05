---
title: "Joindre une machine virtuelle Red Hat Linux à un service de domaine Azure Active Directory | Microsoft Docs"
description: "Découvrez comment joindre une machine virtuelle Red Hat Enterprise Linux 7 à un service de domaine Azure Active Directory."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: 2e46a0f3c9bdbe267d121b4bf62e25d5d411fcc2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="join-a-redhat-linux-vm-to-an-azure-active-directory-domain-service"></a><span data-ttu-id="1260b-103">Joindre une machine virtuelle Red Hat Linux à un service de domaine Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1260b-103">Join a RedHat Linux VM to an Azure Active Directory Domain Service</span></span>

<span data-ttu-id="1260b-104">Cet article explique comment joindre une machine virtuelle Red Hat Enterprise Linux (RHEL) 7 à un domaine géré par Azure Active Directory Domain Services (AADDS).</span><span class="sxs-lookup"><span data-stu-id="1260b-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="1260b-105">Les conditions requises sont :</span><span class="sxs-lookup"><span data-stu-id="1260b-105">The requirements are:</span></span>

- [<span data-ttu-id="1260b-106">un compte Azure</span><span class="sxs-lookup"><span data-stu-id="1260b-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="1260b-107">des fichiers de clés SSH publiques et privées</span><span class="sxs-lookup"><span data-stu-id="1260b-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="1260b-108">un contrôleur de domaine Azure Active Directory Domain Services DC</span><span class="sxs-lookup"><span data-stu-id="1260b-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="1260b-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="1260b-109">Quick Commands</span></span>

<span data-ttu-id="1260b-110">_Remplacez les exemples par vos propres paramètres._</span><span class="sxs-lookup"><span data-stu-id="1260b-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-the-azure-cli-to-classic-deployment-mode"></a><span data-ttu-id="1260b-111">Basculer l’interface de ligne de commande Azure en mode de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="1260b-111">Switch the azure-cli to classic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="1260b-112">Rechercher une version et une image de RHEL</span><span class="sxs-lookup"><span data-stu-id="1260b-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="1260b-113">Créer une machine virtuelle Red Hat Linux</span><span class="sxs-lookup"><span data-stu-id="1260b-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-to-the-vm"></a><span data-ttu-id="1260b-114">Utiliser une clé SSH sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1260b-114">SSH to the VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="1260b-115">Mettre à jour des packages YUM</span><span class="sxs-lookup"><span data-stu-id="1260b-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="1260b-116">Installer les packages requis</span><span class="sxs-lookup"><span data-stu-id="1260b-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="1260b-117">Maintenant que les packages requis sont installés sur la machine virtuelle Linux, la tâche suivante consiste à joindre cette machine virtuelle au domaine géré.</span><span class="sxs-lookup"><span data-stu-id="1260b-117">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

### <a name="discover-the-aad-domain-services-managed-domain"></a><span data-ttu-id="1260b-118">Découvrir le domaine géré par AAD Domain Services</span><span class="sxs-lookup"><span data-stu-id="1260b-118">Discover the AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="1260b-119">Initialiser Kerberos</span><span class="sxs-lookup"><span data-stu-id="1260b-119">Initialize kerberos</span></span>

<span data-ttu-id="1260b-120">Vérifiez que vous spécifiez un utilisateur appartenant au groupe « AAD DC Administrators ».</span><span class="sxs-lookup"><span data-stu-id="1260b-120">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="1260b-121">Seuls ces utilisateurs peuvent joindre des ordinateurs au domaine géré.</span><span class="sxs-lookup"><span data-stu-id="1260b-121">Only these users can join computers to the managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-the-machine-to-the-domain"></a><span data-ttu-id="1260b-122">Joindre la machine au domaine</span><span class="sxs-lookup"><span data-stu-id="1260b-122">Join the machine to the domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-the-machine-is-joined-to-the-domain"></a><span data-ttu-id="1260b-123">Vérifier que la machine est jointe au domaine</span><span class="sxs-lookup"><span data-stu-id="1260b-123">Verify the machine is joined to the domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="1260b-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1260b-124">Next Steps</span></span>

* [<span data-ttu-id="1260b-125">Infrastructure RHUI (Red Hat Update Infrastructure) pour machines virtuelles Red Hat Enterprise Linux à la demande dans Azure</span><span class="sxs-lookup"><span data-stu-id="1260b-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1260b-126">Configuration de Key Vault pour des machines virtuelles dans Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1260b-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1260b-127">Déploiement et gestion de machines virtuelles à l’aide des modèles Azure Resource Manager et de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="1260b-127">Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
