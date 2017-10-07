---
title: "aaaConfigure Gestionnaire de volume logique sur une machine virtuelle exécutant Linux | Documents Microsoft"
description: "Découvrez comment tooconfigure Gestionnaire de volume logique sur Linux dans Azure."
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a>Configurer LVM sur une machine virtuelle Linux dans Azure
Ce document vous explique comment tooconfigure logique Volume Manager (Gestionnaire de volume logique) dans votre machine virtuelle Azure. Bien qu’il soit possible tooconfigure que gestionnaire de volume logique sur n’importe quel disque attaché toohello virtual machine, par défaut cloud la plupart des images n’aura pas Gestionnaire de volume logique configuré sur hello disque de système d’exploitation. Il s’agit des problèmes de tooprevent avec les groupes de volumes en double si hello disque de système d’exploitation est déjà attaché tooanother VM de hello distribution même type et, par exemple, lors d’un scénario de récupération. Par conséquent, il est recommandé uniquement toouse Gestionnaire de volume logique sur des disques de données hello.

## <a name="linear-vs-striped-logical-volumes"></a>Volumes logiques linéaires et agrégé par bandes
Gestionnaire de volume logique peut être utilisé toocombine un nombre de disques physiques dans un seul volume de stockage. Par défaut Gestionnaire de volume logique crée généralement des volumes logiques linéaires, ce qui signifie que le stockage physique de hello concaténé ensemble. Dans ce cas les opérations de lecture/écriture seront généralement uniquement envoyées tooa seul disque. En revanche, nous pouvons également créer des volumes agrégés par bandes de logiques où les lectures et écritures sont les disques toomultiple distribuée contenues dans le groupe de volumes hello (c'est-à-dire similaire tooRAID0). Pour des performances optimales, qu'il est probable que vous pouvez toostripe vos volumes logiques afin que les lectures et écritures utilisent tous vos disques de données attaché.

Ce document sera décrivent comment toocombine les données de plusieurs disques dans un seul groupe de volumes, puis créez un volume logique. les étapes de Hello ci-dessous sont quelque peu généralisée toowork avec la plupart des distributions. Dans la plupart des hello de cas les utilitaires et les flux de travail pour la gestion du Gestionnaire de volume logique sur Azure n’est pas fondamentalement différentes des autres environnements. Comme d’habitude, veuillez également consulter votre fournisseur Linux pour obtenir la documentation et les meilleures pratiques pour utiliser LVM avec votre distribution spécifique.

## <a name="attaching-data-disks"></a>Disques de données attachés
Un est souhaitable généralement toostart avec deux ou plusieurs disques de données vide lors de l’utilisation du Gestionnaire de volume logique. Selon vos besoins d’e/s, vous pouvez choisir les disques tooattach qui sont stockées dans notre stockage Standard, avec des e/s de too500/ps par le stockage sur disque ou notre Premium avec des e/s de too5000/ps par disque. Cet article ne sera pas entrer dans les détails sur la façon de tooprovision et attacher une machine virtuelle Linux données disques tooa. Consultez l’article de Microsoft Azure hello [attacher un disque](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour obtenir des instructions détaillées sur tooattach un vide de données de disque virtuels tooa Linux sur Azure.

## <a name="install-hello-lvm-utilities"></a>Installez les utilitaires du Gestionnaire de volume logique hello
* **Ubuntu**

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* **RHEL, CentOS &amp; Oracle Linux**

    ```bash   
    sudo yum install lvm2
    ```

* **SLES 12 et openSUSE**

    ```bash   
    sudo zypper install lvm2
    ```

* **SLES 11**

    ```bash   
    sudo zypper install lvm2
    ```

    Sur SLES11 vous devez également modifier `/etc/sysconfig/lvm` et définissez `LVM_ACTIVATED_ON_DISCOVERED` trop « activer » :

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a>Configurer LVM
Dans ce guide, nous supposerons vous avez attaché les trois disques de données, ce qui nous l’appellerons tooas `/dev/sdc`, `/dev/sdd` et `/dev/sde`. Notez qu’il ne peuvent pas toujours être hello mêmes noms de chemin d’accès dans votre machine virtuelle. Vous pouvez exécuter '`sudo fdisk -l`' ou toolist de commande similaires vos disques disponibles.

1. Préparer les volumes physiques hello :

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. Créez un groupe de volumes. Dans cet exemple, nous appelons un groupe de volumes hello `data-vg01`:

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. Créer ou les volumes logiques hello. Hello commande ci-dessous, nous crée un volume logique appelé `data-lv01` toospan hello ensemble groupe de volumes, mais il est également possible toocreate plusieurs volumes logiques dans un groupe de volumes hello.

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. Format du volume logique hello

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > Avec SLES 11, utilisez `-t ext3` plutôt qu’ext4. SLES11 prend uniquement en charge les systèmes de fichiers tooext4 accès en lecture seule.

## <a name="add-hello-new-file-system-tooetcfstab"></a>Ajouter hello nouveau fichier système trop/etc/fstab
> [!IMPORTANT]
> Mal modification hello `/etc/fstab` fichier peut entraîner un système non démarrable. En cas de doute, consultez la documentation de la distribution toohello pour plus d’informations sur la façon dont tooproperly modifier ce fichier. Il est également recommandé d’une sauvegarde de hello `/etc/fstab` fichier est créé avant la modification.

1. Créez le point de montage hello souhaité pour votre nouveau système de fichiers, par exemple :

    ```bash  
    sudo mkdir /data
    ```

2. Recherchez le chemin d’accès du volume logique hello

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. Ouvrez `/etc/fstab` dans un éditeur de texte et ajoutez une entrée pour le nouveau système de fichiers hello, par exemple :

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    Ensuite, enregistrez et fermez `/etc/fstab`.

4. Tester ce hello `/etc/fstab` entrée est correcte :

    ```bash    
    sudo mount -a
    ```

    Si cette commande renvoie un message d’erreur de syntaxe hello dans hello Vérifiez `/etc/fstab` fichier.
   
    Prochaine exécution hello `mount` système de fichiers de commandes tooensure hello est monté :

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. (Facultatif) Paramètres de démarrage fiables dans `/etc/fstab`
   
    Nombre de distributions inclure soit hello `nobootwait` ou `nofail` monter des paramètres qui peuvent être ajoutées toohello `/etc/fstab` fichier. Ces paramètres permettent échecs lors du montage d’un système de fichiers particulier et autoriser hello Linux système toocontinue tooboot même s’il est impossible de tooproperly montage hello RAID. Veuillez consultez la documentation de la distribution tooyour pour plus d’informations sur ces paramètres.
   
    Exemple (Ubuntu) :

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a>Prise en charge de TRIM/UNMAP
Certains noyaux Linux prend en charge TRIM/annuler le mappage operations toodiscard les blocs inutilisés sur le disque de hello. Ces opérations sont principalement dans tooinform standard de stockage Azure qui pages supprimées ne sont plus valides et peuvent être ignorées. Le fait d’ignorer des pages peut vous permettre de réaliser des économies si vous créez des fichiers volumineux, puis les supprimez.

Il existe deux façons tooenable TRIM prend en charge dans votre VM Linux. Comme d’habitude, consultez votre distribution pour hello approche recommandée :

- Hello d’utilisation `discard` monter option dans `/etc/fstab`, par exemple :

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- Dans certains hello cas `discard` option peut avoir des conséquences sur les performances. Vous pouvez également exécuter hello `fstrim` commande manuellement à partir de la ligne de commande hello ou ajoutez-le tooyour crontab toorun régulièrement :

    **Ubuntu**

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    **RHEL/CentOS**

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
