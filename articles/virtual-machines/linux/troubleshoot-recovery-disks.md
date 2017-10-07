---
title: "aaaUse une résolution des problèmes de la machine virtuelle avec hello Azure CLI 2.0 de Linux | Documents Microsoft"
description: "Découvrez comment tootroubleshoot Linux VM émet par connexion hello du système d’exploitation disque tooa récupération machine virtuelle à l’aide de hello Azure CLI 2.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a>Dépanner une VM Linux en attachant hello du système d’exploitation disque tooa ordinateur virtuel de récupération avec hello Azure CLI 2.0
Si votre machine virtuelle de Linux (VM) rencontre une erreur de démarrage ou de disque, vous devrez peut-être tooperform étapes de dépannage sur le disque dur virtuel hello lui-même. Un exemple courant est une entrée non valide dans `/etc/fstab` qui empêche de hello machine virtuelle en mesure de tooboot avec succès. Cet article explique comment toouse hello Azure CLI 2.0 tooconnect votre virtuel dur disque tooanother Linux VM toofix toutes les erreurs, puis recréer votre machine virtuelle d’origine. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="recovery-process-overview"></a>Vue d’ensemble du processus de récupération
Hello, résolution des problèmes de processus est la suivante :

1. Supprimer hello VM fait de rencontrer des problèmes, en conservant les disques durs virtuels hello.
2. Attacher et monter tooanother de disque dur virtuel hello Linux VM à des fins de dépannage.
3. Se connecter toohello résolution des problèmes de la machine virtuelle. Modifier des fichiers ou d’exécuter des outils toofix problèmes sur les disque dur virtuel d’origine hello.
4. Démontez et détacher le disque dur virtuel de hello de hello, résolution des problèmes de la machine virtuelle.
5. Créer une machine virtuelle à l’aide de hello d’origine disque dur.

tooperform ces étapes de dépannage vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Bonjour les exemples suivants, remplacez les noms de paramètres par vos propres valeurs. Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.


## <a name="determine-boot-issues"></a>Identifier les problèmes de démarrage
Examinez toodetermine de sortie série hello pourquoi votre machine virtuelle n’est pas en mesure de tooboot correctement. Un exemple courant est une entrée non valide dans `/etc/fstab`, ou hello sous-jacent de disque dur virtuel est supprimé ou déplacé.

Obtenir les journaux de démarrage hello avec [az vm diagnostics de démarrage get-démarrage-log](/cli/azure/vm/boot-diagnostics#get-boot-log). Hello exemple suivant obtient hello série sortie à partir de hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

Passez en revue les toodetermine de sortie série hello pourquoi hello VM échoue tooboot. Si aucune indication n’offre pas de sortie de série hello, vous devrez peut-être tooreview les fichiers de journaux dans `/var/log` une fois que vous avez hello virtuel disque dur connecté tooa résolution des problèmes de la machine virtuelle.


## <a name="view-existing-virtual-hard-disk-details"></a>Afficher les détails du disque dur virtuel existant
Avant de pouvoir joindre votre disque dur virtuel (VHD) de tooanother machine virtuelle, vous devez tooidentify hello URI de disque de système d’exploitation hello. 

Pour afficher des informations sur votre machine virtuelle, utilisez la commande [az vm show](/cli/azure/vm#show). Hello d’utilisation `--query` le disque du système d’exploitation de toohello URI indicateur tooextract hello. exemple Hello Obtient des informations de disque pour hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

Hello URI est trop similaire**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.

## <a name="delete-existing-vm"></a>Supprimer une machine virtuelle existante
Les disques durs virtuels et les machines virtuelles sont deux ressources distinctes dans Azure. Un disque dur virtuel consiste à stocker des hello système d’exploitation, des applications et des configurations. Hello machine virtuelle proprement dite est simplement des métadonnées qui définit la taille de hello ou l’emplacement et fait référence à des ressources, tel qu’un disque dur virtuel ou d’une carte réseau virtuelle (NIC). Chaque disque dur virtuel a un bail attribué lorsqu’il est attaché tooa machine virtuelle. Bien que les disques de données peuvent être attachées et détachées même pendant l’exécution de la machine virtuelle de hello, les disques du système d’exploitation hello ne peut pas être détachée tant que hello ressource d’ordinateur virtuel est supprimé. bail de Hello continue disque hello du système d’exploitation de tooassociate avec une machine virtuelle, même lorsque l’ordinateur virtuel est dans un état arrêté et est libéré.

Hello première étape toorecover votre machine virtuelle est la ressource d’ordinateur virtuel hello toodelete lui-même. Suppression hello VM laisse hello des disques durs virtuels dans votre compte de stockage. Après hello que machine virtuelle est supprimée, vous attachez hello disque dur virtuel tooanother VM tootroubleshoot et résolvez les erreurs de hello.

Supprimer hello machine virtuelle avec [az vm supprimer](/cli/azure/vm#delete). Hello suivant supprime de l’exemple hello ordinateur virtuel nommé `myVM` du groupe de ressources hello nommé `myResourceGroup`:

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

Attendez la fin hello VM suppression avant de joindre tooanother de disque dur virtuel hello machine virtuelle. bail Hello sur le disque dur virtuel hello qui associe hello machine virtuelle doit toobe publié avant de pouvoir joindre tooanother de disque dur virtuel hello machine virtuelle.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Attacher tooanother de disque dur virtuel existant machine virtuelle
Pour hello en suivant quelques étapes, vous utilisez un autre ordinateur virtuel à des fins de dépannage. Vous attachez hello toothis de disque dur virtuel existant dépannage toobrowse de machine virtuelle et que vous modifiez le contenu du disque hello. Ce processus vous permet de toocorrect toutes les erreurs de configuration ou examiner des applications supplémentaires ou de système de fichiers journaux, par exemple. Choisissez ou créez une autre machine virtuelle toouse, à des fins de dépannage.

Attacher hello disque dur virtuel existant avec [az non managée-disque de machine virtuelle attacher](/cli/azure/vm/unmanaged-disk#attach). Lorsque vous attachez le disque dur virtuel existant hello, spécifiez le disque de toohello hello URI obtenu Bonjour précédent `az vm show` commande. exemple Hello attache un toohello disque dur virtuel existant, résolution des problèmes d’ordinateur virtuel nommé `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>Monter le disque de données attaché hello

> [!NOTE]
> Hello exemples suivants décrivent les étapes hello requis sur un VM Ubuntu. Si vous utilisez un autre distributeur Linux, telles que Red Hat Enterprise Linux ou SUSE, hello emplacements des fichiers journaux et `mount` commandes peuvent être légèrement différentes. Consultez la documentation du toohello pour votre distribution spécifique pour les modifications appropriées de hello dans les commandes.

1. SSH tooyour de résolution des problèmes de la machine virtuelle en utilisant les informations d’identification appropriées hello. Si ce disque est hello première données disque attaché tooyour résolution des problèmes de la machine virtuelle, hello disque est probablement connecté trop`/dev/sdc`. Utilisez `dmseg` tooview les disques attachés :

    ```bash
    dmesg | grep SCSI
    ```

    Hello la sortie est similaire toohello l’exemple suivant :

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    Bonjour précédent exemple, disque de hello du système d’exploitation est à `/dev/sda` et le disque temporaire hello fournie pour chaque ordinateur virtuel est à `/dev/sdb`. Si vous possédiez plusieurs disques de données, ils doivent se trouver au niveau de `/dev/sdd`, `/dev/sde`, etc.

2. Créer un répertoire toomount votre disque dur virtuel existant. Hello exemple suivant crée un répertoire nommé `troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. Si vous avez plusieurs partitions sur votre disque dur virtuel existant, montez la partition de hello requis. exemple Hello monte première partition principale hello à `/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > Il est recommandé toomount des disques de données sur des machines virtuelles à l’aide d’Azure hello identificateur unique universel (UUID) du disque dur virtuel de hello. Pour ce scénario de dépannage court, le disque dur virtuel hello montage à l’aide de hello UUID n’est pas nécessaire. Toutefois, en fonctionnement normal, Édition `/etc/fstab` à l’aide du nom de périphérique plutôt que UUID peut entraîner des disques durs virtuels toomount hello tooboot toofail de machine virtuelle.


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Résoudre des problèmes sur le disque dur virtuel d’origine
Avec hello disque dur virtuel existant monté, vous pouvez désormais effectuer une maintenance et dépannage en fonction des besoins. Une fois que vous avez corrige les problèmes de hello, poursuivez hello comme suit.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Démonter et dissocier le disque dur virtuel d’origine
Une fois les erreurs résolues, vous démontez et détachez un disque dur virtuel existant hello à partir de votre machine virtuelle de résolution des problèmes. Vous ne pouvez pas utiliser votre disque dur virtuel avec n’importe quel autre machine virtuelle jusqu'à ce que le bail hello attachement toohello de disque dur virtuel hello résolution des problèmes de la machine virtuelle est libéré.

1. À partir de hello tooyour de session SSH résolution des problèmes d’ordinateur virtuel, démontez le disque dur virtuel existant hello. Modifiez d’abord en dehors du répertoire parent de hello pour votre point de montage :

    ```bash
    cd /
    ```

    Démonter le disque dur virtuel existant hello maintenant. exemple Hello démonte périphérique hello sur `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Maintenant détacher le disque dur virtuel de hello à partir de la machine virtuelle de hello. Quittez hello SSH session tooyour résolution des problèmes de la machine virtuelle. Hello de liste jointe tooyour de disques de données résolution des problèmes de la machine virtuelle avec [liste de disque non managée de machine virtuelle az](/cli/azure/vm/unmanaged-disk#list). listes hello disques de données d’exemple Hello attaché toohello ordinateur virtuel nommé `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`:

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    Notez le nom hello pour votre disque dur virtuel existant. Par exemple, le nom hello d’un disque avec hello URI de **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** est **myVHD**. 

    Détacher le disque de données hello à partir de votre machine virtuelle [az non managée-disque de machine virtuelle détacher](/cli/azure/vm/unmanaged-disk#detach). exemple Hello détache disque hello nommé `myVHD` de hello ordinateur virtuel nommé `myVMRecovery` Bonjour `myResourceGroup` groupe de ressources :

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a>Créer une machine virtuelle à partir du disque dur d’origine
utilisation d’une machine virtuelle à partir de votre disque dur virtuel d’origine, toocreate [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). modèle JSON réel Hello est à hello lien :

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

modèle Hello déploie une machine virtuelle à l’aide de hello URI VHD à partir de hello commande précédemment. Déployer le modèle hello avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create). Fournir hello URI tooyour disque dur virtuel d’origine, puis spécifiez les type hello du système d’exploitation, la taille de machine virtuelle et nom d’ordinateur virtuel comme suit :

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a>Réactiver les diagnostics de démarrage
Lorsque vous créez votre machine virtuelle à partir du disque dur virtuel existant hello, les diagnostics de démarrage ne peut pas être automatiquement activés. Activez les diagnostics de démarrage avec la commande [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable). Hello exemple suivant permet d’extension de diagnostic hello sur hello ordinateur virtuel nommé `myDeployedVM` dans le groupe de ressources hello nommé `myResourceGroup`:

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, consultez [tooan dépanner SSH connexions Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Pour résoudre les problèmes liés à l’accès aux applications exécutées sur votre machine virtuelle, consultez la section [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Linux Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
