---
title: aaaJoin un tooan RedHat Linux VM Azure Active Directory DS | Documents Microsoft
description: Comment toojoin un tooan de machine virtuelle de RedHat Enterprise Linux 7 Azure des services de domaine Active Directory existant.
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
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a><span data-ttu-id="8ddb5-103">Joindre un tooan RedHat Linux VM Azure des services de domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ddb5-103">Join a RedHat Linux VM tooan Azure Active Directory Domain Service</span></span>

<span data-ttu-id="8ddb5-104">Cet article explique comment toojoin un tooan de machine virtuelle Red Hat Enterprise Linux (RHEL) 7 Services de domaine Active Directory (AADDS) d’Azure géré le domaine.</span><span class="sxs-lookup"><span data-stu-id="8ddb5-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="8ddb5-105">spécifications de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="8ddb5-105">hello requirements are:</span></span>

- [<span data-ttu-id="8ddb5-106">un compte Azure</span><span class="sxs-lookup"><span data-stu-id="8ddb5-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="8ddb5-107">des fichiers de clés SSH publiques et privées</span><span class="sxs-lookup"><span data-stu-id="8ddb5-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="8ddb5-108">un contrôleur de domaine Azure Active Directory Domain Services DC</span><span class="sxs-lookup"><span data-stu-id="8ddb5-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="8ddb5-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="8ddb5-109">Quick Commands</span></span>

<span data-ttu-id="8ddb5-110">_Remplacez les exemples par vos propres paramètres._</span><span class="sxs-lookup"><span data-stu-id="8ddb5-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a><span data-ttu-id="8ddb5-111">Basculer le mode de déploiement tooclassic hello cli d’azure</span><span class="sxs-lookup"><span data-stu-id="8ddb5-111">Switch hello azure-cli tooclassic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="8ddb5-112">Rechercher une version et une image de RHEL</span><span class="sxs-lookup"><span data-stu-id="8ddb5-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="8ddb5-113">Créer une machine virtuelle Red Hat Linux</span><span class="sxs-lookup"><span data-stu-id="8ddb5-113">Create a Redhat Linux VM</span></span>

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

### <a name="ssh-toohello-vm"></a><span data-ttu-id="8ddb5-114">SSH toohello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8ddb5-114">SSH toohello VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="8ddb5-115">Mettre à jour des packages YUM</span><span class="sxs-lookup"><span data-stu-id="8ddb5-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="8ddb5-116">Installer les packages requis</span><span class="sxs-lookup"><span data-stu-id="8ddb5-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="8ddb5-117">Maintenant que les packages hello requis sont installés sur une machine virtuelle Linux hello, la tâche suivante hello est toojoin hello machine virtuelle toohello domaine géré.</span><span class="sxs-lookup"><span data-stu-id="8ddb5-117">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

### <a name="discover-hello-aad-domain-services-managed-domain"></a><span data-ttu-id="8ddb5-118">Découverte de domaine géré de Services de domaine AAD hello</span><span class="sxs-lookup"><span data-stu-id="8ddb5-118">Discover hello AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="8ddb5-119">Initialiser Kerberos</span><span class="sxs-lookup"><span data-stu-id="8ddb5-119">Initialize kerberos</span></span>

<span data-ttu-id="8ddb5-120">Veillez à spécifier un utilisateur qui appartient le groupe de toohello « administrateurs de contrôleur de domaine AAD ».</span><span class="sxs-lookup"><span data-stu-id="8ddb5-120">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="8ddb5-121">Seuls ces utilisateurs peuvent joindre le domaine géré des ordinateurs toohello.</span><span class="sxs-lookup"><span data-stu-id="8ddb5-121">Only these users can join computers toohello managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a><span data-ttu-id="8ddb5-122">Joindre le domaine toohello hello</span><span class="sxs-lookup"><span data-stu-id="8ddb5-122">Join hello machine toohello domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a><span data-ttu-id="8ddb5-123">Vérifiez les ordinateur hello sont toohello joint à un domaine</span><span class="sxs-lookup"><span data-stu-id="8ddb5-123">Verify hello machine is joined toohello domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="8ddb5-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ddb5-124">Next Steps</span></span>

* [<span data-ttu-id="8ddb5-125">Infrastructure RHUI (Red Hat Update Infrastructure) pour machines virtuelles Red Hat Enterprise Linux à la demande dans Azure</span><span class="sxs-lookup"><span data-stu-id="8ddb5-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="8ddb5-126">Configuration de Key Vault pour des machines virtuelles dans Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8ddb5-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="8ddb5-127">Déployer et gérer des ordinateurs virtuels à l’aide de modèles Azure Resource Manager et hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="8ddb5-127">Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
