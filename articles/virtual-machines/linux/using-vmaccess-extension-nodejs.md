---
title: "accès aaaReset sur l’utilisation de machines virtuelles de Azure Linux hello VMAccess Extension | Documents Microsoft"
description: "Réinitialisez l’accès sur les ordinateurs virtuels Linux de Azure à l’aide de hello VMAccess Extension."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>Gérer les utilisateurs, SSH et vérification ou de disquettes de réparation sur les machines virtuelles Azure Linux à l’aide de bienvenue de le VMAccess Extension avec hello Azure CLI 1.0
Cet article vous explique comment toouse hello Azure VMAcesss Extension toocheck ou réparer un disque, réinitialisez l’accès de l’utilisateur, gérer les comptes d’utilisateur ou réinitialiser la configuration de SSHD hello sur Linux. article de Hello nécessite :

* un compte Azure ([obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/)).
* Hello [CLI d’Azure](../../cli-install-nodejs.md) connecté `azure login`.
* Hello CLI d’Azure *doit se trouver dans* mode Azure Resource Manager `azure config mode arm`.


## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#quick-commands)– notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello


## <a name="quick-commands"></a>Commandes rapides
Il existe deux façons toouse VMAccess sur vos machines virtuelles Linux :

* À l’aide de hello Azure CLI 1.0 et hello les paramètres requis.
* À l’aide de fichiers JSON bruts que VMAccess traite et exploite.

Section de commande rapide hello, nous allons toouse hello Azure CLI 1.0 `azure vm reset-access` (méthode). Bonjour des exemples de commandes suivante, remplacez les valeurs de hello qui contiennent « exemple » avec des valeurs hello à partir de votre propre environnement.

## <a name="create-a-resource-group-and-linux-vm"></a>Création d'un groupe de ressources et d’une machine virtuelle Linux
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>Création d’une machine virtuelle Debian
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a>Réinitialisation du mot de passe racine
mot de passe tooreset hello racine :

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>Réinitialisation de la clé SSH
tooreset hello code SSH d’un utilisateur non racine :

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>Créer un utilisateur
toocreate un utilisateur :

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>Supprimer un utilisateur
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>Réinitialiser SSHD
configuration de SSHD tooreset hello :

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>Procédure pas à pas
### <a name="vmaccess-defined"></a>VMAccess défini :
disque Hello sur votre VM Linux affichant les erreurs. Vous une certaine manière réinitialisez le mot de passe racine hello pour votre VM Linux ou accidentellement votre clé privée SSH. Si cela se produisait dans jours hello de centre de données hello, vous devez toodrive il et puis ouvrez tooget KVM hello sur la console serveur hello. Considérer hello extension VMAccess de Azure en tant que ce commutateur qui vous permet de tooaccess hello console tooreset accès tooLinux ou effectuez une maintenance au niveau du disque.

Pour hello plus procédure pas à pas, nous allons la forme longue de hello toouse de VMAccess, qui utilise des fichiers bruts JSON.  Ces fichiers JSON VMAccess peuvent également être appelés à partir de modèles Azure.

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>À l’aide de VMAccess toocheck ou la réparation du disque hello d’un VM Linux
L’utilisation de VMAccess vous pouvez effectuer un fsck s’exécutent sur le disque hello sous votre VM Linux.  Vous pouvez également effectuer une vérification de disque et une réparation de disque à l’aide d’un VMAccess.

toocheck, puis sur Réparer hello disque utiliser ce script VMAccess :

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>À l’aide de VMAccess tooreset utilisateur accès tooLinux
Si vous avez perdu l’accès tooroot sur votre VM Linux, vous pouvez lancer un VMAccess script tooreset hello mot de passe racine.

mot de passe tooreset hello racine, utilisez ce script VMAccess :

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

la clé SSH hello tooreset d’un utilisateur non racine, utilisez ce script VMAccess :

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>À l’aide de comptes d’utilisateur toomanage VMAccess sur Linux
VMAccess est un script Python qui peut être des utilisateurs toomanage utilisés sur votre Linux VM sans connexion et à l’aide du compte de racine sudo ou hello.

toocreate un utilisateur, utilisez ce script VMAccess :

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete un utilisateur, utilisez ce script VMAccess :

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>À l’aide de la configuration de VMAccess tooreset hello SSHD
Si vous effectuez la configuration de modifications toohello SSHD de machines virtuelles Linux et la connexion SSH hello fermer avant de vérifier les modifications de hello, vous ne puissent pas SSH'ing dans.  VMAccess peut être utilisé tooreset hello SSHD configuration arrière tooa bonne configuration sans être connecté en via SSH.

configuration de SSHD hello tooreset utiliser ce script de VMAccess :

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>Étapes suivantes
Mise à jour de Linux à l’aide des Extensions de VMAccess Azure est une méthode toomake change sur une VM Linux en cours d’exécution.  Vous pouvez également utiliser des outils tels qu’init de cloud et les modèles Azure toomodify votre VM Linux au démarrage du système.

[À propos des extensions et des fonctionnalités des machines virtuelles](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Lors de la création à l’aide de cloud-init toocustomize un VM Linux](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

