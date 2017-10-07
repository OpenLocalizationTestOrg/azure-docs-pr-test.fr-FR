---
title: "aaaUse a Linux résolution des problèmes de la machine virtuelle dans hello portail Azure | Documents Microsoft"
description: "Découvrez comment les problèmes d’ordinateur virtuel Linux tootroubleshoot par connexion hello du système d’exploitation disque tooa récupération machine virtuelle à l’aide de hello portail Azure"
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
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Dépanner une VM Linux en attachant l’ordinateur virtuel de récupération tooa de disque hello du système d’exploitation à l’aide de hello portail Azure
Si votre machine virtuelle de Linux (VM) rencontre une erreur de démarrage ou de disque, vous devrez peut-être tooperform étapes de dépannage sur le disque dur virtuel hello lui-même. Un exemple courant est une entrée non valide dans `/etc/fstab` qui empêche de hello machine virtuelle en mesure de tooboot avec succès. Cet article explique comment toouse hello tooconnect portail Azure votre virtuel dur disque tooanother Linux VM toofix toutes les erreurs, puis recréer votre machine virtuelle d’origine.

## <a name="recovery-process-overview"></a>Vue d’ensemble du processus de récupération
Hello, résolution des problèmes de processus est la suivante :

1. Supprimer hello VM fait de rencontrer des problèmes, en conservant les disques durs virtuels hello.
2. Attacher et monter tooanother de disque dur virtuel hello Linux VM à des fins de dépannage.
3. Se connecter toohello résolution des problèmes de la machine virtuelle. Modifier des fichiers ou d’exécuter des outils toofix problèmes sur les disque dur virtuel d’origine hello.
4. Démontez et détacher le disque dur virtuel de hello de hello, résolution des problèmes de la machine virtuelle.
5. Créer une machine virtuelle à l’aide de hello d’origine disque dur.


## <a name="determine-boot-issues"></a>Identifier les problèmes de démarrage
Examinez les diagnostics de démarrage hello et toodetermine de capture d’écran de machine virtuelle pourquoi votre machine virtuelle n’est pas en mesure de tooboot correctement. Comme exemple courant, citons une entrée non valide dans `/etc/fstab`, ou le disque dur virtuel en cours de suppression ou de déplacement.

Sélectionnez votre machine virtuelle dans le portail de hello et faites défiler vers le bas toohello **prise en charge + dépannage** section. Cliquez sur **diagnostics de démarrage** messages de la console tooview hello diffusées en continu depuis votre machine virtuelle. Révision hello journaux de la console toosee si vous pouvez déterminer pourquoi hello VM rencontre un problème. Hello suivant montre qu'une machine virtuelle est bloqué en mode de maintenance qui nécessite une intervention manuelle :

![Affichage des journaux de console des diagnostics de démarrage de la machine virtuelle](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

Vous pouvez également cliquer sur **capture d’écran de** haut hello de hello démarrage diagnostics journal toodownload une capture de capture d’écran de la machine virtuelle hello.


## <a name="view-existing-virtual-hard-disk-details"></a>Afficher les détails du disque dur virtuel existant
Avant de pouvoir joindre votre tooanother de disque dur virtuel machine virtuelle, vous devez nom de hello tooidentify de hello les disque dur virtuel (VHD). 

Sélectionnez votre groupe de ressources à partir du portail de hello, puis sélectionnez votre compte de stockage. Cliquez sur **BLOB**, comme dans hello l’exemple suivant :

![Sélectionner les blobs de stockage](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

En général, vous avez un conteneur nommé **vhds** qui stocke vos disques durs virtuels. Sélectionnez le conteneur de hello tooview une liste de disques durs virtuels. Nom de hello Remarque de votre disque dur virtuel (hello préfixe est généralement hello nom de votre machine virtuelle) :

![Identifier le disque dur virtuel dans un conteneur de stockage](./media/troubleshoot-recovery-disks-portal/storage-container.png)

Sélectionnez votre disque dur virtuel existant à partir de la liste de hello et copier l’URL de hello pour une utilisation dans hello comme suit :

![Copier l’URL du disque dur virtuel existant](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a>Supprimer une machine virtuelle existante
Les disques durs virtuels et les machines virtuelles sont deux ressources distinctes dans Azure. Un disque dur virtuel consiste à stocker des hello système d’exploitation, des applications et des configurations. Hello machine virtuelle proprement dite est simplement des métadonnées qui définit la taille de hello ou l’emplacement et fait référence à des ressources, tel qu’un disque dur virtuel ou d’une carte réseau virtuelle (NIC). Chaque disque dur virtuel a un bail attribué lorsqu’il est attaché tooa machine virtuelle. Bien que les disques de données peuvent être attachées et détachées même pendant l’exécution de la machine virtuelle de hello, les disques du système d’exploitation hello ne peut pas être détachée tant que hello ressource d’ordinateur virtuel est supprimé. bail de Hello continue disque hello du système d’exploitation de tooassociate avec une machine virtuelle, même lorsque l’ordinateur virtuel est dans un état arrêté et est libéré.

Hello première étape toorecover votre machine virtuelle est la ressource d’ordinateur virtuel hello toodelete lui-même. Suppression hello VM laisse hello des disques durs virtuels dans votre compte de stockage. Après hello que machine virtuelle est supprimée, vous attachez hello disque dur virtuel tooanother VM tootroubleshoot et résolvez les erreurs de hello.

Sélectionnez votre machine virtuelle dans le portail de hello, puis cliquez sur **supprimer**:

![Capture d’écran de diagnostics de démarrage de machine virtuelle présentant une erreur de démarrage](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

Attendez la fin hello VM suppression avant de joindre tooanother de disque dur virtuel hello machine virtuelle. bail Hello sur le disque dur virtuel hello qui associe hello machine virtuelle doit toobe publié avant de pouvoir joindre tooanother de disque dur virtuel hello machine virtuelle.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Attacher tooanother de disque dur virtuel existant machine virtuelle
Pour hello en suivant quelques étapes, vous utilisez un autre ordinateur virtuel à des fins de dépannage. Vous attachez hello toothis de disque dur virtuel existant toobrowse en mesure de machine virtuelle toobe de résolution des problèmes et que vous modifiez le contenu du disque hello. Ce processus vous permet de toocorrect toutes les erreurs de configuration ou examiner des applications supplémentaires ou de système de fichiers journaux, par exemple. Choisissez ou créez une autre machine virtuelle toouse, à des fins de dépannage.

1. Sélectionnez votre groupe de ressources à partir du portail de hello, puis sélectionnez votre machine virtuelle de résolution des problèmes. Sélectionnez **Disques**, puis cliquez sur **Attacher existant** :

    ![Attacher un disque existant dans le portail de hello](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. tooselect votre disque dur virtuel existant, cliquez sur **fichier de disque dur virtuel**:

    ![Rechercher le disque dur virtuel existant](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. Sélectionnez votre compte de stockage et votre conteneur, puis cliquez sur votre disque dur virtuel existant. Cliquez sur hello **sélectionnez** bouton tooconfirm votre choix :

    ![Sélectionner votre disque dur virtuel existant](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. Cliquez sur votre disque dur virtuel sélectionné maintenant, **OK** tooattach hello disque dur virtuel existant :

    ![Confirmer l’attachement du disque dur virtuel existant](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. Après quelques secondes, hello **disques** répertorie pour votre machine virtuelle votre disque dur virtuel existant connecté en tant qu’un disque de données :

    ![Disque dur virtuel existant attaché en tant que disque de données](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a>Monter le disque de données attaché hello

> [!NOTE]
> Hello exemples suivants décrivent les étapes hello requis sur un VM Ubuntu. Si vous utilisez un autre distributeur Linux, telles que Red Hat Enterprise Linux ou SUSE, hello emplacements des fichiers journaux et `mount` commandes peuvent être légèrement différentes. Consultez la documentation du toohello pour votre distribution spécifique pour les modifications appropriées de hello dans les commandes.

1. SSH tooyour de résolution des problèmes de la machine virtuelle en utilisant les informations d’identification appropriées hello. Si ce disque est hello première données disque attaché tooyour résolution des problèmes de la machine virtuelle, il est probablement connecté trop`/dev/sdc`. Utilisez `dmseg` toolist les disques attachés :

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
Une fois les erreurs résolues, détachez hello disque dur virtuel existant à partir de votre machine virtuelle de résolution des problèmes. Vous ne pouvez pas utiliser votre disque dur virtuel avec n’importe quel autre machine virtuelle jusqu'à ce que le bail hello attachement toohello de disque dur virtuel hello résolution des problèmes de la machine virtuelle est libéré.

1. À partir de hello tooyour de session SSH résolution des problèmes d’ordinateur virtuel, démontez le disque dur virtuel existant hello. Modifiez d’abord en dehors du répertoire parent de hello pour votre point de montage :

    ```bash
    cd /
    ```

    Démonter le disque dur virtuel existant hello maintenant. exemple Hello démonte périphérique hello sur `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Maintenant détacher le disque dur virtuel de hello à partir de la machine virtuelle de hello. Sélectionnez votre machine virtuelle dans le portail de hello et cliquez sur **disques**. Sélectionnez votre disque dur virtuel existant, puis cliquez **Dissocier** :

    ![Dissocier le disque dur virtuel existant](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    Attendez que hello machine virtuelle a été correctement détaché disque de données hello avant de continuer.

## <a name="create-vm-from-original-hard-disk"></a>Créer une machine virtuelle à partir du disque dur d’origine
utilisation d’une machine virtuelle à partir de votre disque dur virtuel d’origine, toocreate [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). modèle de Hello déploie une machine virtuelle dans un réseau virtuel existant, à l’aide de hello URL de disque dur virtuel à partir de hello commande précédemment. Cliquez sur hello **déployer tooAzure** bouton comme suit :

![Déployer la machine virtuelle du modèle à partir de GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

modèle de Hello chargée hello portail Azure pour le déploiement. Entrez les noms de hello pour votre nouvelle machine virtuelle et les ressources Azure existantes et collez hello URL tooyour disque dur virtuel existant. déploiement de hello toobegin, cliquez sur **achat**:

![Déployer une machine virtuelle à partir d’un modèle](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>Réactiver les diagnostics de démarrage
Lorsque vous créez votre machine virtuelle à partir du disque dur virtuel existant hello, les diagnostics de démarrage ne peut pas être automatiquement activés. toocheck hello état des diagnostics de démarrage et l’activer si nécessaire, sélectionnez votre machine virtuelle dans le portail de hello. Sous **Surveillance**, cliquez sur **Paramètres de diagnostic**. Vérifiez l’état de hello est **sur**, et hello coche ensuite trop**diagnostics de démarrage** est sélectionnée. Si vous apportez des modifications, cliquez sur **Enregistrer** :

![Mettre à jour les paramètres des diagnostics de démarrage](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, consultez [tooan dépanner SSH connexions Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Pour résoudre les problèmes liés à l’accès aux applications exécutées sur votre machine virtuelle, consultez la section [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Linux Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Pour plus d’informations sur l’utilisation de Resource Manager, consultez la page [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
