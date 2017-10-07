---
title: "aaaReset accès tooan machine virtuelle de Azure Linux | Documents Microsoft"
description: "Comment toomanage accès aux utilisateurs et réinitialiser sur l’utilisation de machines virtuelles Linux hello VMAccess Extension et hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a>Gérer les utilisateurs, SSH et vérification ou la réparation des disques sur l’utilisation de machines virtuelles Linux hello VMAccess Extension avec hello Azure CLI 2.0
disque Hello sur votre VM Linux affichant les erreurs. Vous une certaine manière réinitialisez le mot de passe racine hello pour votre VM Linux ou accidentellement votre clé privée SSH. Si cela se produisait dans jours hello de centre de données hello, vous devez toodrive il et puis ouvrez tooget KVM hello sur la console serveur hello. Considérer hello extension VMAccess de Azure en tant que ce commutateur qui vous permet de tooaccess hello console tooreset accès tooLinux ou effectuez une maintenance au niveau du disque.

Cet article vous explique comment toouse hello Azure de le VMAccess Extension toocheck ou réparer un disque, réinitialisez l’accès de l’utilisateur, gérer les comptes d’utilisateur ou réinitialiser la configuration SSH de hello sur Linux. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="ways-toouse-hello-vmaccess-extension"></a>Méthodes toouse hello VMAccess Extension
Il existe deux manières que vous pouvez utiliser hello VMAccess Extension sur vos machines virtuelles Linux :

* Utilisez hello Azure CLI 2.0 et les paramètres de hello requis.
* [Utilisez le JSON brut fichiers ce processus de le VMAccess Extension hello](#use-json-files-and-the-vmaccess-extension) et ensuite agir sur.

Hello suivant l’utilisation d’exemples [utilisateur de machine virtuelle az](/cli/azure/vm/user) commandes. tooperform ces étapes, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

## <a name="reset-ssh-key"></a>Réinitialisation d’une clé SSH
Hello exemple suivant réinitialise la clé SSH hello pour l’utilisateur de hello `azureuser` sur hello ordinateur virtuel nommé `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>Réinitialiser le mot de passe
Hello exemple suivant réinitialise hello de mot de passe pour l’utilisateur de hello `azureuser` sur hello ordinateur virtuel nommé `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>Redémarrer SSH
exemple Hello redémarre démon SSH hello et réinitialise hello des valeurs de toodefault configuration SSH sur un ordinateur virtuel nommé `myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>Créer un utilisateur
Hello exemple suivant crée un utilisateur nommé `myNewUser` à l’aide d’une clé SSH pour l’authentification sur hello ordinateur virtuel nommé `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>Supprimer un utilisateur
Hello exemple suivant supprime un utilisateur nommé `myNewUser` sur hello ordinateur virtuel nommé `myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a>Utiliser des fichiers au format JSON et hello VMAccess Extension
Hello suivant exemples utiliser des fichiers bruts JSON. Utilisez [az vm extension ensemble](/cli/azure/vm/extension#set) toothen appeler vos fichiers JSON. Ces fichiers JSON peuvent également être appelés à partir de modèles Azure. 

### <a name="reset-user-access"></a>Réinitialisation de l’accès utilisateur
Si vous avez perdu l’accès tooroot sur votre VM Linux, vous pouvez lancer une tooreset de script VMAccess clé SSH ou le mot de passe d’un utilisateur.

tooreset hello la clé publique SSH d’un utilisateur, créez un fichier nommé `reset_ssh_key.json` et ajouter des paramètres dans hello suivant le format. Remplacez par vos propres valeurs hello `username` et `ssh_key` paramètres :

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

tooreset un mot de passe utilisateur, créez un fichier nommé `reset_user_password.json` et ajouter des paramètres dans hello suivant le format. Remplacez par vos propres valeurs hello `username` et `password` paramètres :

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a>Redémarrer SSH
toorestart hello démon SSH et réinitialiser les valeurs de toodefault configuration hello SSH, créez un fichier nommé `reset_sshd.json`. Ajoutez hello suivant le contenu :

```json
{
  "reset_ssh": true
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a>Gestion des utilisateurs

toocreate un utilisateur qui utilise une clé SSH pour l’authentification, créez un fichier nommé `create_new_user.json` et ajouter des paramètres dans hello suivant le format. Remplacez par vos propres valeurs hello `username` et `ssh_key` paramètres :

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

toodelete un utilisateur, créez un fichier nommé `delete_user.json` et ajoutez hello suivant le contenu. Remplacez par votre propre valeur pour hello `remove_user` paramètre :

```json
{
  "remove_user":"myNewUser"
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a>Vérifiez ou réparez hello disque
L’utilisation de VMAccess vous pouvez également vérifier et réparer un disque que vous avez ajouté toohello Linux VM.

toocheck, puis hello disquette, créez un fichier nommé `disk_check_repair.json` et ajouter des paramètres dans hello suivant le format. Remplacez par votre propre valeur pour nom hello de `repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

Exécutez le script de VMAccess hello avec :

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a>Étapes suivantes
Mise à jour de Linux à l’aide de hello le VMAccess Extension Azure est une méthode toomake change sur une VM Linux en cours d’exécution. Vous pouvez également utiliser des outils tels que le cloud-init et toomodify de modèles Azure Resource Manager votre VM Linux au démarrage du système.

[Extensions et fonctionnalités de machine virtuelle pour Linux](extensions-features.md)

[Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Lors de la création à l’aide de cloud-init toocustomize un VM Linux](using-cloud-init.md)

