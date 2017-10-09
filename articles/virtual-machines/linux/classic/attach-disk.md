---
title: aaaAttach un tooa disque VM Linux dans Azure | Documents Microsoft
description: "En savoir tooattach données tooa Linux VM de disque à l’aide de déploiement classique de hello modéliser et initialiser le disque de hello par conséquent, il est prêt à être utilisé"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>Comment tooAttach un tooa de disque de données Machine virtuelle Linux
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Consultez Comment trop[attacher un disque de données à l’aide du modèle de déploiement du Gestionnaire de ressources hello](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Vous pouvez attacher les disques vides et les disques qui contiennent des données tooyour machines virtuelles Azure. Les deux types de disques sont des fichiers .vhd conservés dans un compte de stockage Azure. Comme avec l’ajout d’un ordinateur Linux de tooa de disque, après avoir attaché le disque de hello vous devez tooinitialize et mettre en forme par conséquent, il est prêt à être utilisé. Cet article explique l’attachement de disques vides et les disques contenant déjà des données tooyour machines virtuelles, ainsi que la manière dont toothen initialiser et formater un nouveau disque.

> [!NOTE]
> Il s’agit d’une meilleure toouse de pratique une ou plusieurs séparés toostore de disques, les données d’un ordinateur virtuel. Lorsque vous créez une machine virtuelle Azure, celle-ci possède un disque de système d'exploitation et un disque temporaire. **N’utilisez pas hello disque temporaire toostore persistants de données.** Hello nom l’indique, il fournit un stockage temporaire uniquement. Il n'offre aucune possibilité de redondance ou de sauvegarde, car il ne réside pas dans le stockage Azure.
> disque temporaire de Hello est généralement gérée par hello Linux Agent Azure et automatiquement monté trop**/mnt/resource** (ou **/mnt** sur Ubuntu images). Sur hello autre part, un disque de données peut être nommé par le noyau Linux de hello quelque chose comme `/dev/sdc`, et vous devez toopartition, mettre en forme et monter cette ressource. Consultez hello [Guide de l’utilisateur l’Agent Linux Azure] [ Agent] pour plus d’informations.
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>Initialisation d’un nouveau disque de données sous Linux
1. SSH tooyour machine virtuelle. Pour plus d’informations, consultez [comment toolog sur l’ordinateur virtuel de tooa exécutant Linux][Logon].
2. Ensuite, vous devez identificateur de l’appareil toofind hello pour tooinitialize de disque de données hello. Il existe deux façons toodo qui :
   
    a) Grep pour les périphériques SCSI Bonjour ouvre une session, comme dans hello de commande suivante :
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    Pour les distributions Ubuntu récent, vous devrez peut-être toouse `sudo grep SCSI /var/log/syslog` car l’enregistrement trop`/var/log/messages` peuvent être désactivés par défaut.
   
    Vous trouverez l’identificateur hello hello dernière du disque de données qui a été ajoutée dans les messages de type hello qui sont affichés.
   
    ![Obtenir les messages de disque hello](./media/attach-disk/scsidisklog.png)
   
    OU
   
    b) hello d’utilisation `lsscsi` toofind de commande des id de périphérique hello. `lsscsi` peuvent être installées par soit `yum install lsscsi` (base de distributions sur Red Hat) ou `apt-get install lsscsi` (base de distributions sur Debian). Vous pouvez trouver de disque de hello recherchée par son *lun* ou **numéro d’unité logique**. Par exemple, hello *lun* pour hello disques vous pouvant facilement visible à partir de `azure vm disk list <virtual-machine>` en tant que :

    ```azurecli
    azure vm disk list myVM
    ```

    sortie de Hello est similaire toohello suivantes :

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    Comparer ces données avec une sortie hello de `lsscsi` pour hello les mêmes exemples de machine virtuelle :
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    dernier numéro de tuple hello dans chaque ligne Hello est hello *lun*. Pour plus d'informations, consultez `man lsscsi` .
3. À l’invite de hello, tapez ce qui suit hello commande toocreate votre appareil :
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. Lorsque vous y êtes invité, tapez  **n**  toocreate une partition.

    ![Créer un appareil](./media/attach-disk/fdisknewpartition.png)

5. Lorsque vous y êtes invité, tapez **p** partition principale pour toomake hello partition hello. Type **1** toomake il hello première partition et tapez indiquez tooaccept hello valeur par défaut cylindre de hello. Sur certains systèmes, il peut afficher les valeurs par défaut hello hello premier et hello dernier secteurs, au lieu de cylindre de hello. Vous pouvez choisir tooaccept ces valeurs par défaut.

    ![Créer une partition](./media/attach-disk/fdisknewpartdetails.png)


6. Type **p** toosee hello plus d’informations sur disque de hello est partitionné.

    ![Répertorier les informations sur le disque](./media/attach-disk/fdiskpartitiondetails.png)


7. Type **w** toowrite les paramètres de hello pour le disque de hello.

    ![Écrire les modifications de disque hello](./media/attach-disk/fdiskwritedisk.png)

8. Maintenant, vous pouvez créer des système de fichiers hello sur la nouvelle partition de hello. Ajouter l’ID de périphérique hello partition numéro toohello (Bonjour exemple `/dev/sdc1`). Hello exemple suivant crée une partition ext4 sur /dev/sdc1 :
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Créer le système de fichiers](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > Les systèmes SUSE Linux Enterprise 11 ne prennent en charge que l’accès en lecture seule aux systèmes de fichiers ext4. Pour ces systèmes, il est recommandé de tooformat hello nouveau système de fichiers comme ext3 plutôt qu’ext4.

9. Effectuez un répertoire toomount hello nouveau système de fichiers, comme suit :
   
    ```bash
    sudo mkdir /datadrive
    ```

10. Enfin, vous pouvez monter le lecteur de hello, comme suit :
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    Hello disque de données est maintenant prêt toouse comme **/datadrive**.
   
    ![Créer hello active et montage hello le disque](./media/attach-disk/mkdirandmount.png)

11. Ajoutez hello nouveau lecteur trop/etc/fstab :
   
    lecteur de hello tooensure est remontée automatiquement après qu’un redémarrage, qu'il doit être ajouté le fichier/etc/fstab de toohello. En outre, il est recommandé que hello UUID (universellement Unique IDentifier) est utilisé dans/etc/fstab toorefer toohello lecteur plutôt que simplement hello nom de périphérique (par exemple, /dev/sdc1). À l’aide de hello UUID évite hello incorrect disque monté tooa emplacement donné si hello du système d’exploitation détecte une erreur disque pendant le démarrage et les disques de données restants en étant celles reçoivent un ID de périphérique. toofind hello UUID du nouveau lecteur de hello, vous pouvez utiliser hello **blkid** utilitaire :
   
    ```bash
    sudo -i blkid
    ```
   
    sortie de Hello semble similaire toohello l’exemple suivant :
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > Mal modification hello **/etc/fstab** fichier peut entraîner un système non démarrable. En cas de doute, consultez la documentation de la distribution toohello pour plus d’informations sur la façon dont tooproperly modifier ce fichier. Il est également recommandé qu’une sauvegarde de fichier/etc/fstab de hello est créée avant la modification.

    Ensuite, ouvrez hello **/etc/fstab** fichier dans un éditeur de texte :

    ```bash
    sudo vi /etc/fstab
    ```

    Dans cet exemple, nous utilisons valeur UUID de hello pour hello nouvelle **/dev/sdc1** périphérique qui a été créé dans les étapes précédentes hello et point de montage hello **/datadrive**. Ajouter hello suivant la fin ligne toohello Hello **/etc/fstab** fichier :

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    Ou, sur les systèmes basés sur SuSE Linux, vous devrez peut-être toouse un format légèrement différent :

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > Hello `nofail` option garantit que hello machine virtuelle démarre, même si le système de fichiers hello est endommagé ou disque de hello n’existe pas au moment du démarrage. Sans cette option, vous pouvez rencontrer le problème comme décrit dans [ne peut pas SSH tooLinux machine virtuelle en raison d’erreurs de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).

    Vous pouvez maintenant tester que le système de fichiers hello est monté correctement par le démontage et de réinstaller le système de fichiers hello, c'est-à-dire à l’aide de point de montage exemple hello `/datadrive` créé Bonjour étapes précédemment :

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    Si hello `mount` commande génère une erreur, vérifiez hello fichier/etc/fstab pour la syntaxe correcte. Si des disques de données ou partitions supplémentaires sont créés, ajoutez-les séparément au fichier /etc/fstab.

    Que les données du lecteur hello accessible en écriture à l’aide de cette commande :

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > Suppression par la suite d’un disque de données sans avoir à modifier fstab pourrait hello VM toofail tooboot. Si cela se produit fréquemment, la plupart des distributions fournissent soit hello `nofail` et/ou `nobootwait` fstab options qui permettent un tooboot système même en cas de disque de hello toomount au moment du démarrage. Pour plus d’informations sur ces paramètres, consultez la documentation de votre distribution.

### <a name="trimunmap-support-for-linux-in-azure"></a>Prise en charge de TRIM/UNMAP pour Linux dans Azure
Certains noyaux Linux prend en charge TRIM/annuler le mappage operations toodiscard les blocs inutilisés sur le disque de hello. Ces opérations sont principalement dans tooinform standard de stockage Azure qui pages supprimées ne sont plus valides et peuvent être ignorées. Le fait d’ignorer des pages peut vous permettre de réaliser des économies si vous créez des fichiers volumineux, puis les supprimez.

Il existe deux façons tooenable TRIM prend en charge dans votre VM Linux. Comme d’habitude, consultez votre distribution pour hello approche recommandée :

* Hello d’utilisation `discard` monter option dans `/etc/fstab`, par exemple :

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* Dans certains hello cas `discard` option peut avoir des conséquences sur les performances. Vous pouvez également exécuter hello `fstrim` commande manuellement à partir de la ligne de commande hello ou ajoutez-le tooyour crontab toorun régulièrement :
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Résolution des problèmes
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez en savoir plus sur l’utilisation de votre VM Linux Bonjour suivant des articles :

* [Comment toolog sur l’ordinateur virtuel de tooa exécutant Linux][Logon]
* [Comment toodetach un disque à partir d’une machine virtuelle Linux](detach-disk.md)
* [À l’aide de hello CLI d’Azure avec le modèle de déploiement classique de hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Configurer RAID sur une machine virtuelle Linux dans Azure](../configure-raid.md)
* [Configurer LVM sur une machine virtuelle Linux dans Azure](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
