---
title: "aaaUse une résolution des problèmes de la machine virtuelle avec hello Azure CLI 1.0 de Linux | Documents Microsoft"
description: "Découvrez comment tootroubleshoot Linux VM émet par connexion hello du système d’exploitation disque tooa récupération machine virtuelle à l’aide de hello Azure CLI 1.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a>Dépanner une VM Linux en attachant l’ordinateur virtuel de récupération tooa de disque hello du système d’exploitation à l’aide de hello Azure CLI 1.0
Si votre machine virtuelle de Linux (VM) rencontre une erreur de démarrage ou de disque, vous devrez peut-être tooperform étapes de dépannage sur le disque dur virtuel hello lui-même. Un exemple courant est une entrée non valide dans `/etc/fstab` qui empêche de hello machine virtuelle en mesure de tooboot avec succès. Cet article explique comment toouse hello Azure CLI 1.0 tooconnect votre virtuel dur disque tooanother Linux VM toofix toutes les erreurs, puis recréer votre machine virtuelle d’origine.


## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#recovery-process-overview) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello


## <a name="recovery-process-overview"></a>Vue d’ensemble du processus de récupération
Hello, résolution des problèmes de processus est la suivante :

1. Supprimer hello VM fait de rencontrer des problèmes, en conservant les disques durs virtuels hello.
2. Attacher et monter tooanother de disque dur virtuel hello Linux VM à des fins de dépannage.
3. Se connecter toohello résolution des problèmes de la machine virtuelle. Modifier des fichiers ou d’exécuter des outils toofix problèmes sur les disque dur virtuel d’origine hello.
4. Démontez et détacher le disque dur virtuel de hello de hello, résolution des problèmes de la machine virtuelle.
5. Créer une machine virtuelle à l’aide de hello d’origine disque dur.

Assurez-vous que vous avez [hello dernière Azure CLI 1.0](../../cli-install-nodejs.md) installé et connecté à l’aide du mode de gestionnaire de ressources :

```azurecli
azure config mode arm
```

Bonjour les exemples suivants, remplacez les noms de paramètres par vos propres valeurs. Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.


## <a name="determine-boot-issues"></a>Identifier les problèmes de démarrage
Examinez toodetermine de sortie série hello pourquoi votre machine virtuelle n’est pas en mesure de tooboot correctement. Un exemple courant est une entrée non valide dans `/etc/fstab`, ou hello sous-jacent de disque dur virtuel est supprimé ou déplacé.

Hello exemple suivant obtient hello série sortie à partir de hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

Passez en revue les toodetermine de sortie série hello pourquoi hello VM échoue tooboot. Si aucune indication n’offre pas de sortie de série hello, vous devrez peut-être tooreview les fichiers de journaux dans `/var/log` une fois que vous avez hello virtuel disque dur connecté tooa résolution des problèmes de la machine virtuelle.


## <a name="view-existing-virtual-hard-disk-details"></a>Afficher les détails du disque dur virtuel existant
Avant de pouvoir joindre votre tooanother de disque dur virtuel machine virtuelle, vous devez nom de hello tooidentify de hello les disque dur virtuel (VHD). 

Hello exemple suivant obtient les informations pour hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

Recherchez `Vhd URI` dans sortie hello hello précédant la commande. Hello tronquée exemple de sortie suivant affiche hello `Vhd URI` sur la dernière ligne de hello :

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a>Supprimer une machine virtuelle existante
Les disques durs virtuels et les machines virtuelles sont deux ressources distinctes dans Azure. Un disque dur virtuel consiste à stocker des hello système d’exploitation, des applications et des configurations. Hello machine virtuelle proprement dite est simplement des métadonnées qui définit la taille de hello ou l’emplacement et fait référence à des ressources, tel qu’un disque dur virtuel ou d’une carte réseau virtuelle (NIC). Chaque disque dur virtuel a un bail attribué lorsqu’il est attaché tooa machine virtuelle. Bien que les disques de données peuvent être attachées et détachées même pendant l’exécution de la machine virtuelle de hello, les disques du système d’exploitation hello ne peut pas être détachée tant que hello ressource d’ordinateur virtuel est supprimé. bail de Hello continue disque hello du système d’exploitation de tooassociate avec une machine virtuelle, même lorsque l’ordinateur virtuel est dans un état arrêté et est libéré.

Hello première étape toorecover votre machine virtuelle est la ressource d’ordinateur virtuel hello toodelete lui-même. Suppression hello VM laisse hello des disques durs virtuels dans votre compte de stockage. Après hello que machine virtuelle est supprimée, vous attachez hello disque dur virtuel tooanother VM tootroubleshoot et résolvez les erreurs de hello.

Hello suivant supprime de l’exemple hello ordinateur virtuel nommé `myVM` du groupe de ressources hello nommé `myResourceGroup`:

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

Attendez la fin hello VM suppression avant de joindre tooanother de disque dur virtuel hello machine virtuelle. bail Hello sur le disque dur virtuel hello qui associe hello machine virtuelle doit toobe publié avant de pouvoir joindre tooanother de disque dur virtuel hello machine virtuelle.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Attacher tooanother de disque dur virtuel existant machine virtuelle
Pour hello en suivant quelques étapes, vous utilisez un autre ordinateur virtuel à des fins de dépannage. Vous attachez hello toothis de disque dur virtuel existant dépannage toobrowse de machine virtuelle et que vous modifiez le contenu du disque hello. Ce processus vous permet de toocorrect toutes les erreurs de configuration ou examiner des applications supplémentaires ou de système de fichiers journaux, par exemple. Choisissez ou créez une autre machine virtuelle toouse, à des fins de dépannage.

Lorsque vous attachez le disque dur virtuel existant hello, spécifier le disque de toohello URL hello obtenu Bonjour précédent `azure vm show` commande. exemple Hello attache un toohello disque dur virtuel existant, résolution des problèmes d’ordinateur virtuel nommé `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`:

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
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

2. Maintenant détacher le disque dur virtuel de hello à partir de la machine virtuelle de hello. Quittez hello SSH session tooyour résolution des problèmes de la machine virtuelle. Bonjour CLI d’Azure, première hello de liste jointe tooyour de disques de données résolution des problèmes de la machine virtuelle. listes hello disques de données d’exemple Hello attaché toohello ordinateur virtuel nommé `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`:

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    Hello de note `Lun` valeur de votre disque dur virtuel existant. Hello exemple de sortie de commande suivant montre le disque virtuel existant par la hello est attaché à LUN 0 :

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    Détacher le disque de données hello à partir de votre machine virtuelle à l’aide de hello applicable `Lun` valeur :

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a>Créer une machine virtuelle à partir du disque dur d’origine
utilisation d’une machine virtuelle à partir de votre disque dur virtuel d’origine, toocreate [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). modèle JSON réel Hello est à hello lien :

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

modèle de Hello déploie une machine virtuelle dans un réseau virtuel existant, à l’aide de hello URL de disque dur virtuel à partir de hello commande précédemment. exemple Hello déploie groupe de ressources hello modèle toohello nommé `myResourceGroup`:

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

Hello de réponse demande modèle hello comme nom d’ordinateur virtuel (`myDeployedVM` hello selon exemple), type de système d’exploitation (`Linux`) et la taille de machine virtuelle (`Standard_DS1_v2`). Hello `osDiskVhdUri` est hello même que celui précédemment utilisé lors de l’attachement toohello disque dur virtuel existant de hello, résolution des problèmes de la machine virtuelle. Un exemple de sortie de la commande hello et la demande est la suivante :

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a>Réactiver les diagnostics de démarrage

Lorsque vous créez votre machine virtuelle à partir du disque dur virtuel existant hello, les diagnostics de démarrage ne peut pas être automatiquement activés. Hello exemple suivant permet d’extension de diagnostic hello sur hello ordinateur virtuel nommé `myDeployedVM` dans le groupe de ressources hello nommé `myResourceGroup`:

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, consultez [tooan dépanner SSH connexions Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Pour résoudre les problèmes liés à l’accès aux applications exécutées sur votre machine virtuelle, consultez la section [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Linux Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
