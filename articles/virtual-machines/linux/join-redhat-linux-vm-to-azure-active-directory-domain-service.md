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
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a>Joindre un tooan RedHat Linux VM Azure des services de domaine Active Directory

Cet article explique comment toojoin un tooan de machine virtuelle Red Hat Enterprise Linux (RHEL) 7 Services de domaine Active Directory (AADDS) d’Azure géré le domaine.  spécifications de Hello sont :

- [un compte Azure](https://azure.microsoft.com/pricing/free-trial/)

- [des fichiers de clés SSH publiques et privées](mac-create-ssh-keys.md)

- [un contrôleur de domaine Azure Active Directory Domain Services DC](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Commandes rapides

_Remplacez les exemples par vos propres paramètres._

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a>Basculer le mode de déploiement tooclassic hello cli d’azure

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>Rechercher une version et une image de RHEL

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Créer une machine virtuelle Red Hat Linux

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

### <a name="ssh-toohello-vm"></a>SSH toohello machine virtuelle

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>Mettre à jour des packages YUM

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>Installer les packages requis

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

Maintenant que les packages hello requis sont installés sur une machine virtuelle Linux hello, la tâche suivante hello est toojoin hello machine virtuelle toohello domaine géré.

### <a name="discover-hello-aad-domain-services-managed-domain"></a>Découverte de domaine géré de Services de domaine AAD hello

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>Initialiser Kerberos

Veillez à spécifier un utilisateur qui appartient le groupe de toohello « administrateurs de contrôleur de domaine AAD ». Seuls ces utilisateurs peuvent joindre le domaine géré des ordinateurs toohello.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a>Joindre le domaine toohello hello

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a>Vérifiez les ordinateur hello sont toohello joint à un domaine

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>Étapes suivantes

* [Infrastructure RHUI (Red Hat Update Infrastructure) pour machines virtuelles Red Hat Enterprise Linux à la demande dans Azure](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Configuration de Key Vault pour des machines virtuelles dans Azure Resource Manager](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Déployer et gérer des ordinateurs virtuels à l’aide de modèles Azure Resource Manager et hello CLI d’Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
