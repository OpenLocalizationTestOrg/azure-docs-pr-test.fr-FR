---
title: "aaaUse une application Windows de résolution des problèmes de la machine virtuelle dans hello portail Azure | Documents Microsoft"
description: "Découvrez comment les problèmes d’ordinateur virtuel Windows tootroubleshoot dans Azure par connexion hello du système d’exploitation disque tooa récupération machine virtuelle à l’aide de hello portail Azure"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Résoudre les problèmes d’une machine virtuelle Windows en attachant l’ordinateur virtuel de récupération tooa de disque hello du système d’exploitation à l’aide de hello portail Azure
Si votre machine virtuelle de Windows (VM) dans Azure rencontre une erreur de démarrage ou de disque, vous devrez peut-être tooperform étapes de dépannage sur le disque dur virtuel hello lui-même. Un exemple courant est une mise à jour de l’application qui a échoué empêche hello machine virtuelle en mesure de tooboot avec succès. Cet article explique comment toouse hello tooconnect portail Azure votre virtuel dur disque tooanother machine virtuelle Windows toofix toutes les erreurs, puis recréer votre machine virtuelle d’origine.

## <a name="recovery-process-overview"></a>Vue d’ensemble du processus de récupération
Hello, résolution des problèmes de processus est la suivante :

1. Supprimer hello VM fait de rencontrer des problèmes, en conservant les disques durs virtuels hello.
2. Attacher et monter un disque dur virtuel de hello tooanother machine virtuelle Windows à des fins de dépannage.
3. Se connecter toohello résolution des problèmes de la machine virtuelle. Modifier des fichiers ou d’exécuter des outils toofix problèmes sur les disque dur virtuel d’origine hello.
4. Démontez et détacher le disque dur virtuel de hello de hello, résolution des problèmes de la machine virtuelle.
5. Créer une machine virtuelle à l’aide de hello d’origine disque dur.


## <a name="determine-boot-issues"></a>Identifier les problèmes de démarrage
toodetermine pourquoi votre machine virtuelle n’est pas en mesure de tooboot correctement, examinez les diagnostics de démarrage hello capture d’écran de la machine virtuelle. Comme exemple courant, citons l’échec de mise à jour d’une application ou un disque dur virtuel en cours de suppression ou de déplacement.

Sélectionnez votre machine virtuelle dans le portail de hello et faites défiler vers le bas toohello **prise en charge + dépannage** section. Cliquez sur **diagnostics de démarrage** tooview capture d’écran de hello. Notez les messages d’erreur spécifiques ou les codes d’erreur toohelp déterminer pourquoi hello VM rencontre un problème. Hello suivant montre une machine virtuelle en attente sur l’arrêt des services :

![Affichage des journaux de console des diagnostics de démarrage de la machine virtuelle](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

Vous pouvez également cliquer sur **capture d’écran de** toodownload une capture de capture d’écran de la machine virtuelle hello.


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

1. Ouvrez un tooyour de connexion Bureau à distance machine virtuelle. Sélectionnez votre machine virtuelle dans le portail de hello et cliquez sur **connexion**. Téléchargez et ouvrez le fichier de connexion RDP hello. Entrez vos informations d’identification toolog dans tooyour machine virtuelle comme suit :

    ![Connectez-vous à tooyour machine virtuelle en utilisant Bureau à distance](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. Ouvrez le **Gestionnaire de serveur**, puis sélectionnez **Services de fichiers et de stockage**. 

    ![Sélection de Services de fichiers et de stockage dans le Gestionnaire de serveur](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. disque de données Hello est automatiquement détecté et attaché. toosee une liste de hello disques connectés, sélectionnez **disques**. Vous pouvez sélectionner votre disque tooview volume de données, y compris la lettre de lecteur hello. Hello exemple affiche hello disque de données attaché et à l’aide de **F:**:

    ![Disque attaché et informations sur le volume dans le Gestionnaire de serveur](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Résoudre des problèmes sur le disque dur virtuel d’origine
Avec hello disque dur virtuel existant monté, vous pouvez désormais effectuer une maintenance et dépannage en fonction des besoins. Une fois que vous avez corrige les problèmes de hello, poursuivez hello comme suit.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Démonter et dissocier le disque dur virtuel d’origine
Une fois les erreurs résolues, détachez hello disque dur virtuel existant à partir de votre machine virtuelle de résolution des problèmes. Vous ne pouvez pas utiliser votre disque dur virtuel avec n’importe quel autre machine virtuelle jusqu'à ce que le bail hello attachement toohello de disque dur virtuel hello résolution des problèmes de la machine virtuelle est libéré.

1. À partir de tooyour de session RDP hello machine virtuelle, ouvrez **le Gestionnaire de serveur**, puis sélectionnez **File and Storage Services**:

    ![Sélection de Services de fichiers et de stockage dans le Gestionnaire de serveur](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. Sélectionnez **Disques**, puis sélectionnez votre disque de données. Cliquez avec le bouton droit sur votre disque de données et sélectionnez **Mettre hors connexion** :

    ![Définir le disque de données hello comme étant hors connexion dans le Gestionnaire de serveur](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. Maintenant détacher le disque dur virtuel de hello à partir de la machine virtuelle de hello. Sélectionnez votre machine virtuelle hello portail Azure, cliquez sur **disques**. Sélectionnez votre disque dur virtuel existant, puis cliquez **Dissocier** :

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
Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, consultez [tooan des connexions RDP de résoudre les problèmes Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Pour résoudre les problèmes liés à l’accès aux applications exécutées sur votre machine virtuelle, consultez [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Pour plus d’informations sur l’utilisation de Resource Manager, consultez la page [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).