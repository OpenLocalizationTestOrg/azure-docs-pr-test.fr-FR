---
title: "aaaCreate et télécharger Red Hat Enterprise Linux disque dur virtuel pour une utilisation dans Azure | Documents Microsoft"
description: "En savoir plus toocreate et téléchargez un Azure disque dur virtuel (VHD) qui contient un système d’exploitation Red Hat Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>Préparation d'une machine virtuelle Red Hat pour Azure
Dans cet article, vous allez apprendre comment tooprepare un ordinateur virtuel de Red Hat Enterprise Linux (RHEL) pour une utilisation dans Azure. les versions de Hello de RHEL qui sont abordées dans cet article sont 6.7 + et 7.1. les hyperviseurs Hello de préparation qui sont abordées dans cet article sont virtuels Hyper-V, basée sur le noyau (KVM) et VMware. Pour plus d’informations sur les conditions d’éligibilité pour participer au programme d’accès au Cloud de Red Hat, consultez le [site Web d’accès au cloud de Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) et [Exécution RHEL sous Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>Préparer une machine virtuelle Red Hat à partir du Gestionnaire Hyper-V

### <a name="prerequisites"></a>Composants requis
Cette section part du principe que vous avez déjà obtenu un fichier ISO à partir du site Web de Red Hat hello et installé hello RHEL image tooa disque dur virtuel (VHD). Pour plus d’informations sur la façon toouse Gestionnaire Hyper-V tooinstall une image de système d’exploitation, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](http://technet.microsoft.com/library/hh846766.aspx).

**Notes d'installation de RHEL**

* Azure ne prend pas en charge le format VHDX hello. Azure prend uniquement en charge les VHD fixes. Vous pouvez utiliser le Gestionnaire Hyper-V tooconvert hello disque tooVHD format, ou vous pouvez utiliser les applets de commande convert-vhd hello. Si vous utilisez VirtualBox, sélectionnez **une taille fixe** par opposition toohello par défaut alloué dynamiquement option lorsque vous créez le disque de hello.
* Azure ne prend en charge que les machines virtuelles de la génération 1. Vous pouvez convertir un ordinateur virtuel de génération 1 à partir du format de fichier de disque dur virtuel VHDX toohello et à partir du disque de taille fixe tooa de taille dynamique. Vous ne pouvez pas modifier la génération d’une machine virtuelle. Pour plus d’informations, consultez [Dois-je créer une machine virtuelle de génération 1 ou 2 dans Hyper-V ?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).
* taille maximale Hello est autorisée pour hello disque dur virtuel est de 1 023 go.
* Lorsque vous installez le système d’exploitation de Linux hello, nous vous recommandons d’utiliser les partitions standards plutôt que le Gestionnaire de Volume logique (LVM), qui est souvent hello par défaut pour le nombre d’installations. Cette pratique permet d’éviter les conflits de nom Gestionnaire de volume logique avec les ordinateurs virtuels clonés, en particulier si vous avez besoin de tooattach un système d’exploitation disque tooanother ordinateur virtuel pour le dépannage. La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données.
* La prise en charge du noyau pour le montage de systèmes de fichiers UDF (Universal Disk Format) est requise. Au premier démarrage sur Azure, hello au format UDF support qui est attaché toohello invité passe hello configuration configuration toohello machine virtuelle Linux. Hello Linux Agent Azure doit être en mesure de toomount hello UDF fichier système tooread sa configuration et configurer l’ordinateur virtuel de hello.
* Versions du noyau de Linux hello qui sont antérieures à 2.6.37 ne gèrent pas l’accès mémoire non uniforme (NUMA) sur Hyper-V avec des tailles de machine virtuelle plus importantes. Ce problème principalement les impacts anciennes distributions qui utilisent hello en amont noyau de Red Hat 2.6.32 et a été corrigé dans RHEL 6.6 (noyau-2.6.32-504). Les systèmes qui exécutent des noyaux personnalisés qui sont antérieurs à 2.6.37 ou les noyaux RHEL qui sont antérieurs à 2.6.32-504 doivent définir hello `numa=off` paramètre de démarrage sur la ligne de commande de noyau hello dans grub.conf. Pour plus d’informations, consultez l’article [KB 436883](https://access.redhat.com/solutions/436883) sur Red Hat.
* Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello. Hello Linux Agent peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.  Vous trouverez plus d’informations à ce sujet Bonjour comme suit.
* La taille de tout disque dur virtuel doit être un multiple de 1 Mo.

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>Préparer une machine virtuelle RHEL 6 à partir du Gestionnaire Hyper-V

1. Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.

2. Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.

3. RHEL 6, NetworkManager peut interférer avec l’agent de hello Azure Linux. Désinstaller ce package en exécutant hello de commande suivante :
   
        # sudo rpm -e --nodeps NetworkManager

4. Créer ou modifier hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Déplacer (ou supprimer) hello udev règles tooavoid génération de règles statiques pour l’interface de Ethernet hello. Ces règles entraînent des problèmes lorsque vous clonez une machine virtuelle dans Microsoft Azure ou Hyper-V :

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :

        # sudo chkconfig network on

8. Inscrire votre installation de hello Red Hat abonnement tooenable des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat. Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo cette modification, ouvre `/boot/grub/menu.lst` dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Cela permet également de garantir que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.
    
    En outre, nous recommandons de supprimer hello paramètres suivants :
    
        rhgb quiet crashkernel=auto
    
    Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.  Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez. Notez que ce paramètre réduit hello de mémoire disponible dans l’ordinateur virtuel hello 128 Mo ou plus. Cette configuration peut être problématique sur les machines virtuelles de petite taille.

    >[!Important]
    RHEL 6.5 et versions antérieur doive également définir hello `numa=off` paramètre de noyau. Consultez Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

11. Vérifiez le serveur hello SSH (secure shell) est installé et configuré toostart au moment du démarrage, qui est généralement hello par défaut. Modifiez hello de tooinclude /etc/ssh/sshd_config ligne suivante :

        ClientAliveInterval 180

12. Installez hello Linux Agent Azure en exécutant hello de commande suivante :

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    Package de WALinuxAgent hello lors de l’installation supprime hello NetworkManager et packages de NetworkManager-gnome si elles n’étaient pas déjà supprimées à l’étape 3.

13. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.

    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure. Notez que hello local disque de ressources est un disque temporaire et qu’il doit être vidé lors de la machine virtuelle de hello est annulé. Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifiez hello suivant correctement les paramètres dans /etc/waagent.conf :

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. Annuler l’inscription d’abonnement de hello (si nécessaire) en exécutant hello de commande suivante :

        # sudo subscription-manager unregister

15. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. Cliquez sur **Action** > **Arrêter** dans le Gestionnaire Hyper-V. Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>Préparer une machine virtuelle RHEL 7 à partir du Gestionnaire Hyper-V

1. Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.

2. Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.

3. Créer ou modifier hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :

        # sudo chkconfig network on

6. Inscrire votre installation de hello Red Hat abonnement tooenable des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo cette modification, ouvre `/etc/default/grub` dans un éditeur de texte et l’édition hello `GRUB_CMDLINE_LINUX` paramètre. Par exemple :
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Cela permet également de garantir que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage. Cette configuration désactive également des conventions d’affectation de noms hello nouvelle RHEL 7 pour les cartes réseau. En outre, nous vous recommandons de supprimer hello paramètres suivants :
   
        rhgb quiet crashkernel=auto
   
    Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série. Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez. Notez que ce paramètre réduit hello de mémoire disponible dans la machine virtuelle de hello de 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites.

8. Après avoir effectué édition `/etc/default/grub`, exécutez hello après la commande toorebuild hello grub configuration :

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage, qui est généralement hello par défaut. Modifier `/etc/ssh/sshd_config` hello tooinclude ligne suivante :

        ClientAliveInterval 180

10. package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat. Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. Installez hello Linux Agent Azure en exécutant hello de commande suivante :

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.

    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure. Notez que hello disque de ressources locales est un disque temporaire, et il doit être vidé lorsque l’ordinateur virtuel hello est déprovisionnée. Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Si vous souhaitez abonnement de hello toounregister, exécutez hello de commande suivante :

        # sudo subscription-manager unregister

14. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Cliquez sur **Action** > **Arrêter** dans le Gestionnaire Hyper-V. Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>Préparer une machine virtuelle Red Hat à partir de KVM
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>Préparer une machine virtuelle RHEL 6 à partir de KMV

1. Télécharger l’image KVM hello RHEL 6 à partir du site Web de Red Hat hello.

2. Définissez un mot de passe racine.

    Générer un mot de passe chiffré et copier le résultat de hello de commande hello :

        # openssl passwd -1 changeme

    Définissez un mot de passe racine avec guestfish :
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Modification hello deuxième champ de l’utilisateur racine hello « ! » toohello le mot de passe chiffré.

3. Créer une machine virtuelle dans KVM à partir de l’image de qcow2 hello. Définir le type de disque hello trop**qcow2**et définir le modèle d’appareil hello réseau virtuel interface trop**virtio**. Ensuite, démarrer l’ordinateur virtuel de hello et connectez-vous en tant que racine.

4. Créer ou modifier hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Déplacer (ou supprimer) hello udev règles tooavoid génération de règles statiques pour l’interface de Ethernet hello. Ces règles entraînent des problèmes lorsque vous clonez une machine virtuelle dans Azure ou Hyper-V :

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :

        # chkconfig network on

8. Inscrire votre installation de hello Red Hat abonnement tooenable des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo cette configuration, ouvre `/boot/grub/menu.lst` dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Cela permet également de garantir que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.
    
    En outre, nous vous recommandons de supprimer hello paramètres suivants :
    
        rhgb quiet crashkernel=auto
    
    Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série. Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez. Notez que ce paramètre réduit hello de mémoire disponible dans la machine virtuelle de hello de 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites.

    >[!Important]
    RHEL 6.5 et versions antérieur doive également définir hello `numa=off` paramètre de noyau. Consultez Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

10. Ajoutez tooinitramfs de modules Hyper-V :  

    Modifier `/etc/dracut.conf`et ajoutez hello suivant le contenu :

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Régénérez initramfs :

        # dracut -f -v

11. Désinstallez Cloud-Init :

        # yum remove cloud-init

12. Vérifiez que ce serveur SSH hello est installé et configuré toostart au moment du démarrage :

        # chkconfig sshd on

    Modifiez hello de tooinclude /etc/ssh/sshd_config lignes suivantes :

        PasswordAuthentication yes
        ClientAliveInterval 180

13. package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat. Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. Installez hello Linux Agent Azure en exécutant hello de commande suivante :

        # yum install WALinuxAgent

        # chkconfig waagent on

15. Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure. Notez que hello disque de ressources locales est un disque temporaire, et il doit être vidé lorsque l’ordinateur virtuel hello est déprovisionnée. Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifier hello suivant les paramètres dans **/etc/waagent.conf** correctement :

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Annuler l’inscription d’abonnement de hello (si nécessaire) en exécutant hello de commande suivante :

        # subscription-manager unregister

17. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Arrêter la machine virtuelle hello KVM.

19. Convertir le format VHD toohello hello qcow2 image.

    Tout d’abord convertir le format de tooraw d’image hello :

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    Assurez-vous que la taille hello d’image brute de hello est aligné avec 1 Mo. Sinon, arrondir tooalign de taille hello avec 1 Mo :

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertir hello disque raw tooa disque dur virtuel de taille fixe :

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>Préparer une machine virtuelle RHEL 7 à partir de KMV

1. Télécharger l’image KVM hello de RHEL 7 à partir du site Web de Red Hat hello. Cette procédure utilise RHEL 7 comme exemple de hello.

2. Définissez un mot de passe racine.

    Générer un mot de passe chiffré et copier le résultat de hello de commande hello :

        # openssl passwd -1 changeme

    Définissez un mot de passe racine avec guestfish :

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Modification hello deuxième champ de l’utilisateur racine à partir de « ! » toohello le mot de passe chiffré.

3. Créer une machine virtuelle dans KVM à partir de l’image de qcow2 hello. Définir le type de disque hello trop**qcow2**et définir le modèle d’appareil hello réseau virtuel interface trop**virtio**. Ensuite, démarrer l’ordinateur virtuel de hello et connectez-vous en tant que racine.

4. Créer ou modifier hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :

        # chkconfig network on

7. Inscrire votre installation de tooenable abonnement Red Hat des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo cette configuration, ouvre `/etc/default/grub` dans un éditeur de texte et l’édition hello `GRUB_CMDLINE_LINUX` paramètre. Par exemple :
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Cette commande garantit également que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage. commande Hello désactive également des conventions d’affectation de noms hello nouvelle RHEL 7 pour les cartes réseau. En outre, nous vous recommandons de supprimer hello paramètres suivants :
   
        rhgb quiet crashkernel=auto
   
    Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série. Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez. Notez que ce paramètre réduit hello de mémoire disponible dans la machine virtuelle de hello de 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites.

9. Après avoir effectué édition `/etc/default/grub`, exécutez hello après la commande toorebuild hello grub configuration :

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. Ajoutez des modules de Hyper-V dans initramfs.

    Modifiez `/etc/dracut.conf` en y ajoutant le contenu suivant :

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Régénérez initramfs :

        # dracut -f -v

11. Désinstallez Cloud-Init :

        # yum remove cloud-init

12. Vérifiez que ce serveur SSH hello est installé et configuré toostart au moment du démarrage :

        # systemctl enable sshd

    Modifiez hello de tooinclude /etc/ssh/sshd_config lignes suivantes :

        PasswordAuthentication yes
        ClientAliveInterval 180

13. package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat. Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. Installez hello Linux Agent Azure en exécutant hello de commande suivante :

        # yum install WALinuxAgent

    Activer le service de waagent hello :

        # systemctl enable waagent.service

15. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.

    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure. Notez que hello disque de ressources locales est un disque temporaire, et il doit être vidé lorsque l’ordinateur virtuel hello est déprovisionnée. Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Annuler l’inscription d’abonnement de hello (si nécessaire) en exécutant hello de commande suivante :

        # subscription-manager unregister

17. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Arrêter la machine virtuelle hello KVM.

19. Convertir le format VHD toohello hello qcow2 image.

    Tout d’abord convertir le format de tooraw d’image hello :

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    Assurez-vous que la taille hello d’image brute de hello est aligné avec 1 Mo. Sinon, arrondir tooalign de taille hello avec 1 Mo :

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertir hello disque raw tooa disque dur virtuel de taille fixe :

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>Préparer une machine virtuelle Red Hat à partir de VMware
### <a name="prerequisites"></a>Composants requis
Cette section suppose que vous avez déjà installé une machine virtuelle RHEL dans VMWare. Pour plus d’informations sur la façon dont tooinstall un système d’exploitation dans les environnements VMware, consultez [Guide d’Installation système d’exploitation invité VMware](http://partnerweb.vmware.com/GOSIG/home.html).

* Lorsque vous installez le système d’exploitation de Linux hello, nous vous recommandons d’utiliser les partitions standards au lieu du Gestionnaire de volume logique, qui est souvent hello par défaut pour le nombre d’installations. Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec les ordinateurs virtuels clonés, en particulier si un disque de système d’exploitation a besoin de machine virtuelle de tooanother toobe attaché pour le dépannage. Vous pouvez utiliser les techniques LVM ou RAID sur les disques de données si vous le souhaitez.
* Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello. Vous pouvez configurer hello Linux agent toocreate un fichier d’échange sur le disque de ressources temporaires hello. Vous trouverez plus d’informations à ce sujet dans les étapes de hello qui suivent.
* Lorsque vous créez un disque dur virtuel hello, sélectionnez **disque virtuel de magasin en tant qu’un seul fichier**.

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>Préparer une machine virtuelle RHEL 6 à partir de VMWare
1. RHEL 6, NetworkManager peut interférer avec l’agent de hello Azure Linux. Désinstaller ce package en exécutant hello de commande suivante :
   
        # sudo rpm -e --nodeps NetworkManager

2. Créez un fichier nommé **réseau** hello etc/sysconfig/répertoire contenant hello suivant du texte :

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. Déplacer (ou supprimer) hello udev règles tooavoid génération de règles statiques pour l’interface de Ethernet hello. Ces règles entraînent des problèmes lorsque vous clonez une machine virtuelle dans Azure ou Hyper-V :

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :

        # sudo chkconfig network on

6. Inscrire votre installation de hello Red Hat abonnement tooenable des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat. Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo, ouvrez `/etc/default/grub` dans un éditeur de texte et l’édition hello `GRUB_CMDLINE_LINUX` paramètre. Par exemple :
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   Cela permet également de garantir que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage. En outre, nous vous recommandons de supprimer hello paramètres suivants :
   
        rhgb quiet crashkernel=auto
   
    Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série. Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez. Notez que ce paramètre réduit hello de mémoire disponible dans la machine virtuelle de hello de 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites.

9. Ajoutez tooinitramfs de modules Hyper-V :

    Modifier `/etc/dracut.conf`et ajoutez hello suivant le contenu :

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Régénérez initramfs :

        # dracut -f -v

10. Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage, qui est généralement hello par défaut. Modifier `/etc/ssh/sshd_config` hello tooinclude ligne suivante :

    ClientAliveInterval 180

11. Installez hello Linux Agent Azure en exécutant hello de commande suivante :

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.

    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure. Notez que hello disque de ressources locales est un disque temporaire, et il doit être vidé lorsque l’ordinateur virtuel hello est déprovisionnée. Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Annuler l’inscription d’abonnement de hello (si nécessaire) en exécutant hello de commande suivante :

        # sudo subscription-manager unregister

14. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Arrêt de la machine virtuelle de hello et convertir le fichier .vhd tooa hello VMDK fichier.

    Tout d’abord convertir le format de tooraw d’image hello :

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    Assurez-vous que la taille hello d’image brute de hello est aligné avec 1 Mo. Sinon, arrondir tooalign de taille hello avec 1 Mo :

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertir hello disque raw tooa disque dur virtuel de taille fixe :

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>Préparer une machine virtuelle RHEL 7 à partir de VMWare
1. Créer ou modifier hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :

        # sudo chkconfig network on

4. Inscrire votre installation de hello Red Hat abonnement tooenable des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo cette modification, ouvre `/etc/default/grub` dans un éditeur de texte et l’édition hello `GRUB_CMDLINE_LINUX` paramètre. Par exemple :
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Cette configuration garantit également que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage. Il désactive également de nouvelles conventions de nommage RHEL 7 hello pour les cartes réseau. En outre, nous vous recommandons de supprimer hello paramètres suivants :
   
        rhgb quiet crashkernel=auto
   
    Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série. Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez. Notez que ce paramètre réduit hello de mémoire disponible dans la machine virtuelle de hello de 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites.

6. Après avoir effectué édition `/etc/default/grub`, exécutez hello après la commande toorebuild hello grub configuration :

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. Ajoutez tooinitramfs de modules Hyper-V.

    Modifiez `/etc/dracut.conf`, ajoutez le contenu :

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Régénérez initramfs :

        # dracut -f -v

8. Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage. Ce paramètre est généralement hello par défaut. Modifier `/etc/ssh/sshd_config` hello tooinclude ligne suivante :

        ClientAliveInterval 180

9. package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat. Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. Installez hello Linux Agent Azure en exécutant hello de commande suivante :

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.

    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure. Notez que hello disque de ressources locales est un disque temporaire, et il doit être vidé lorsque l’ordinateur virtuel hello est déprovisionnée. Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. Si vous souhaitez abonnement de hello toounregister, exécutez hello de commande suivante :

        # sudo subscription-manager unregister

13. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. Arrêt de la machine virtuelle de hello et convertir le format de disque dur virtuel du fichier toohello hello VMDK.

    Tout d’abord convertir le format de tooraw d’image hello :

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    Assurez-vous que la taille hello d’image brute de hello est aligné avec 1 Mo. Sinon, arrondir tooalign de taille hello avec 1 Mo :

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Convertir hello disque raw tooa disque dur virtuel de taille fixe :

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>Préparer une machine virtuelle Red Hat à partir d’un fichier ISO grâce à l’utilisation automatique d’un fichier Kickstart
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>Préparer une machine virtuelle RHEL 7 à partir d'un fichier Kickstart

1.  Créer un fichier qui inclut hello suivant le contenu et enregistrer le fichier de hello. Pour plus d’informations sur l’installation de démarrer, consultez hello [Guide d’Installation de démarrer](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. Placez le fichier hello où système d’installation hello peut y accéder.

3. Dans le Gestionnaire Hyper-V, créez une machine virtuelle. Sur hello **connecter un disque dur virtuel** page, sélectionnez **attacher un disque dur virtuel ultérieurement**et terminé hello Assistant Nouvel ordinateur virtuel.

4. Ouvrez les paramètres d’ordinateur virtuel hello :

    a.  Joindre un ordinateur virtuel toohello disque dur virtuel. Assurez-vous que tooselect **Format VHD** et **taille fixe**.

    b.  Attachez l’installation hello lecteur de DVD toohello ISO.

    c.  Définissez hello BIOS tooboot à partir du CD.

5. Démarrer l’ordinateur virtuel de hello. Guide d’installation Bonjour, appuyez sur **onglet** options de démarrage tooconfigure hello.

6. Entrée `inst.ks=<hello location of hello kickstart file>` à fin hello des options de démarrage hello, appuyez sur **entrée**.

7. Attendez que hello installation toofinish. Lorsqu’il est terminé, hello virtual machine s’arrête automatiquement. Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.

## <a name="known-issues"></a>Problèmes connus
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>pilote de Hyper-V de Hello n’a pas pu être inclus dans le disque initiale hello lors de l’utilisation d’un hyperviseur Hyper-V

Dans certains cas, les programmes d’installation de Linux inclut ne peut-être pas les pilotes hello pour Hyper-V dans hello RAM disque initiale (initrd ou initramfs) à moins que Linux détecte qu’il s’exécute dans un environnement Hyper-V.

Lorsque vous utilisez un tooprepare système (c'est-à-dire, Virtualbox, Xen, etc.) de virtualisation différent votre image Linux, vous devrez toorebuild initrd tooensure qui a au moins hello hv_vmbus et les modules de noyau hv_storvsc sont disponibles sur le disque virtuel hello initiale. Il s’agit au moins un problème connu sur les systèmes qui reposent sur la distribution de Red Hat hello en amont.

tooresolve ce problème, ajoutez tooinitramfs de modules Hyper-V et le reconstruire :

Modifier `/etc/dracut.conf`et ajoutez hello suivant le contenu :

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

Régénérez initramfs :

        # dracut -f -v

Pour plus d’informations, consultez les informations de hello sur [reconstruction initramfs](https://access.redhat.com/solutions/1958).

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt toouse votre Red Hat Enterprise Linux disque dur virtuel toocreate nouvelles machines virtuelles dans Azure. S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Pour plus d’informations sur les hyperviseurs hello qui sont certifiés toorun Red Hat Enterprise Linux, consultez [site Web de Red Hat hello](https://access.redhat.com/certified-hypervisors).
