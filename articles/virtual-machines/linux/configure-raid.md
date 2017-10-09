---
title: "aaaConfigure les volumes RAID logiciels sur un ordinateur virtuel exécutant Linux | Documents Microsoft"
description: "Découvrez comment toouse mdadm tooconfigure RAID sur Linux dans Azure."
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a>Configuration d’un RAID logiciel sur Linux
Il est un commun scénario toouse les volumes RAID logiciels sur les ordinateurs virtuels Linux dans Azure toopresent données jointes plusieurs disques comme un périphérique RAID unique. Cela vous pouvez généralement les performances tooimprove utilisé et autoriser pour améliorée débit comparées toousing un seul disque.

## <a name="attaching-data-disks"></a>Disques de données attachés
Deux ou plusieurs disques de données vides sont nécessaire tooconfigure un périphérique RAID.  Hello principal motif de création d’un périphérique RAID est tooimprove les performances de votre disque e/s.  Selon vos besoins d’e/s, vous pouvez choisir les disques tooattach qui sont stockées dans notre stockage Standard, avec des e/s de too500/ps par le stockage sur disque ou notre Premium avec des e/s de too5000/ps par disque. Cet article n’aborde pas de détails sur la façon de tooprovision et attacher une machine virtuelle Linux données disques tooa.  Consultez l’article de Microsoft Azure hello [attacher un disque](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour obtenir des instructions détaillées sur tooattach un vide de données de disque virtuels tooa Linux sur Azure.

## <a name="install-hello-mdadm-utility"></a>Installer l’utilitaire de mdadm hello
* **Ubuntu**
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* **CentOS et Oracle Linux**
```bash
sudo yum install mdadm
```

* **SLES et openSUSE**
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a>Créer des partitions de disque hello
Dans cet exemple, nous créons une partition de disque unique sur /dev/sdc. nouvelle partition de disque Hello sera appelée /dev/sdc1.

1. Démarrer `fdisk` toobegin création de partitions

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. Appuyez sur « n » à toocreate d’invite de commandes hello un  **n** partition de la nouvelle :

    ```bash
    Command (m for help): n
    ```

3. Ensuite, appuyez sur « p » toocreate un **p**rincipal partition :

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. Appuyez sur le numéro de partition '1' tooselect 1 :

    ```bash
    Partition number (1-4): 1
    ```

5. Sélectionnez hello point de départ de la partition hello, ou appuyez sur `<enter>` partition tooaccept hello par défaut tooplace hello au début de hello d’espace disque de hello hello :

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. Sélectionnez la taille de partition hello, par exemple le type '+10G' toocreate une partition de 10 gigaoctets hello. Ou bien, appuyez sur `<enter>` créer une seule partition qui couvre l’intégralité du lecteur hello :

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. Ensuite, modifiez les ID hello et **t**ype de partition hello à partir de la valeur par défaut hello ID '83' (Linux) tooID 'fd' (Linux raid auto) :

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. Enfin, écrire le lecteur de toohello de table de partition hello et quitter fdisk :

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a>Création de disques RAID hello
1. Hello suivant va de l’exemple « bandes » (RAID de niveau 0) trois partitions situées sur trois disques de données distinct (sdc1, sdd1, sde1).  Après l’exécution de cette commande, un nouveau périphérique RAID dénommé **/dev/md127** est créé. Notez également que si ces données disques nous précédemment partie d’un autre tableau RAID obsolète il peut être nécessaire de tooadd hello `--force` paramètre toohello `mdadm` commande :

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. Créer un système de fichiers hello sur un périphérique RAID nouvelle hello
   
    a. **CentOS, Oracle Linux, SLES 12, openSUSE et Ubuntu**

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    b. **SLES 11**

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    c. **SLES 11** : activez boot.md et créez mdadm.conf

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > Un redémarrage peut être nécessaire après avoir apporté ces modifications sur des systèmes SUSE. Cette étape n’est *pas* requise pour SLES 12.
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a>Ajouter hello nouveau fichier système trop/etc/fstab
> [!IMPORTANT]
> Modification incorrecte de fichier/etc/fstab de hello peut entraîner un système non démarrable. En cas de doute, consultez la documentation de la distribution toohello pour plus d’informations sur la façon dont tooproperly modifier ce fichier. Il est également recommandé qu’une sauvegarde de fichier/etc/fstab de hello est créée avant la modification.

1. Créez le point de montage hello souhaité pour votre nouveau système de fichiers, par exemple :

    ```bash
    sudo mkdir /data
    ```
2. Lorsque vous modifiez/etc/fstab, hello **UUID** doit être utilisé tooreference hello système plutôt que hello appareil nom de fichier.  Hello d’utilisation `blkid` hello de toodetermine utilitaire UUID hello nouveau système de fichiers :

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. Ouvrez/etc/fstab dans un éditeur de texte et ajoutez une entrée pour le nouveau système de fichiers hello, par exemple :

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    Ou sur **SLES 11** :

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    Ensuite, enregistrez et fermez /etc/fstab.

4. Tester que hello/etc/fstab entrée est correcte :

    ```bash  
    sudo mount -a
    ```

    Si cette commande renvoie un message d’erreur, vérifiez la syntaxe hello dans le fichier/etc/fstab de hello.
   
    Prochaine exécution hello `mount` système de fichiers de commandes tooensure hello est monté :

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. (Facultatif) Paramètres de démarrage fiables
   
    **Configuration fstab**
   
    Nombre de distributions inclure soit hello `nobootwait` ou `nofail` monter des paramètres qui peuvent être ajoutés à un fichier fstab toohello/etc /. Ces paramètres permettent échecs lors du montage d’un système de fichiers particulier et autoriser hello Linux système toocontinue tooboot même s’il est impossible de tooproperly montage hello RAID. Pour plus d’informations sur ces paramètres, consultez la documentation de la distribution tooyour.
   
    Exemple (Ubuntu) :

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    **Paramètres de démarrage Linux**
   
    Dans toohello ajout au-dessus de paramètres, hello au paramètre de noyau «`bootdegraded=true`» peut autoriser hello système tooboot même si hello RAID est perçu comme endommagé ou détérioré, par exemple, si un lecteur de données est supprimé par inadvertance de la machine virtuelle de hello. Par défaut, cette situation peut également rendre impossible le démarrage du système.
   
    Consultez la documentation de la distribution tooyour sur comment tooproperly modifier les paramètres de noyau. Par exemple, dans de nombreuses distributions (CentOS, Oracle Linux SLES et 11), ces paramètres peuvent être ajoutés manuellement toohello «`/boot/grub/menu.lst`« fichier.  Sur Ubuntu ce paramètre peut être ajouté à toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable sur « / etc/par défaut/grub ».


## <a name="trimunmap-support"></a>Prise en charge de TRIM/UNMAP
Certains noyaux Linux prend en charge TRIM/annuler le mappage operations toodiscard les blocs inutilisés sur le disque de hello. Ces opérations sont principalement dans tooinform standard de stockage Azure qui pages supprimées ne sont plus valides et peuvent être ignorées. Le fait d’ignorer des pages peut vous permettre de réaliser des économies si vous créez des fichiers volumineux, puis les supprimez.

> [!NOTE]
> RAID ne peut pas émettre des commandes de rejet si la taille de segment de hello pour le tableau de hello a la valeur accessible sans que la valeur par défaut de hello (512 Ko). C’est parce que hello annuler le mappage granularité sur hello hôte est également de 512 Ko. Si vous avez modifié le taille de segment du tableau hello par le biais de mdadm `--chunk=` paramètre, puis les demandes/annuler le mappage de découpage peuvent être ignoré par le noyau de hello.

Il existe deux façons tooenable TRIM prend en charge dans votre VM Linux. Comme d’habitude, consultez votre distribution pour hello approche recommandée :

- Hello d’utilisation `discard` monter option dans `/etc/fstab`, par exemple :

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- Dans certains hello cas `discard` option peut avoir des conséquences sur les performances. Vous pouvez également exécuter hello `fstrim` commande manuellement à partir de la ligne de commande hello ou ajoutez-le tooyour crontab toorun régulièrement :

    **Ubuntu**

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    **RHEL/CentOS**
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
