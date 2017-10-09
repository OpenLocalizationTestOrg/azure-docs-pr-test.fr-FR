---
title: "aaaCreate et télécharger un VHD Linux CentOS base dans Azure"
description: "En savoir plus toocreate et téléchargez un Azure disque dur virtuel (VHD) qui contient un système d’exploitation Linux basée sur CentOS."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>Préparation d'une machine virtuelle CentOS pour Azure
* [Préparation d’une machine virtuelle CentOS 6.x pour Azure](#centos-6x)
* [Préparation d’une machine virtuelle CentOS 7.0+ pour Azure](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez déjà installé un CentOS (ou dérivé similaire) Linux système d’exploitation tooa disque virtuel. Plusieurs outils existent toocreate les fichiers .vhd, par exemple une solution de virtualisation comme Hyper-V. Pour obtenir des instructions, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](http://technet.microsoft.com/library/hh846766.aspx).

**Notes d'installation CentOS**

* Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.
* format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**.  Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande convert-vhd. Si vous utilisez VirtualBox, cela signifie en sélectionnant **une taille fixe** en tant qu’et non par défaut de toohello allouée dynamiquement lors de la création du disque de hello.
* Lorsque vous installez le système de Linux hello *recommandé* que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations). Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un disque du système d’exploitation a besoin toobe jointe tooanother VM identiques pour le dépannage. La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données.
* La prise en charge du noyau pour le montage de systèmes de fichiers UDF est requise. Au premier démarrage sur Azure hello mise en service de configuration est passée toohello Linux VM via un support au format UDF qui est attaché toohello invité. l’agent Azure Linux de Hello doit être en mesure de toomount hello UDF fichier système tooread sa configuration et configurer hello machine virtuelle.
* Les versions du noyau Linux antérieures à la version 2.6.37 ne prennent pas en charge NUMA sur Hyper-V avec des machines virtuelles de taille supérieure. Ce problème principalement les impacts de distributions antérieures à l’aide de hello en amont noyau de Red Hat 2.6.32 et a été corrigé dans RHEL 6.6 (noyau-2.6.32-504). Systèmes en cours d’exécution personnalisées noyaux antérieures à 2.6.37 ou les noyaux basée sur RHEL plus anciens que 2.6.32-504 doit définir hello paramètre démarrage `numa=off` sur noyau hello de ligne de commande dans grub.conf. Pour plus d’informations, consultez l’article [KB 436883](https://access.redhat.com/solutions/436883) sur Red Hat.
* Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello. l’agent de Hello Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.  Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.
* Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.

## <a name="centos-6x"></a>CentOS 6.x

1. Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.

2. Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.

3. CentOS 6, NetworkManager peut interférer avec l’agent de hello Azure Linux. Désinstaller ce package en exécutant hello de commande suivante :
   
        # sudo rpm -e --nodeps NetworkManager

4. Créer ou modifier le fichier de hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Créer ou modifier le fichier de hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Modifier udev tooavoid de règles générant des règles statiques pour hello les interfaces Ethernet. Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Vérifiez que hello network service démarre au moment du démarrage en cours d’exécution hello de commande suivante :
   
        # sudo chkconfig network on

8. Si vous souhaitez que les miroirs OpenLogic toouse hello qui sont hébergés dans hello centres de données Azure, puis remplacez hello `/etc/yum.repos.d/CentOS-Base.repo` fichier avec hello suivant référentiels.  Cette action ajoutera également hello **[openlogic]** référentiel qui inclut les packages supplémentaires, telles que l’agent de hello Azure Linux :

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    Hello reste de ce guide suppose que vous utilisez au moins hello `[openlogic]` référentiel, qui sera utilisé tooinstall hello Azure Linux agent ci-dessous.


9. Ajoutez hello suivant ligne too/etc/yum.conf :
    
        http_caching=packages

10. Exécutez hello suivant commande tooclear hello yum mise à jour et les métadonnées hello système actuel avec les derniers packages de hello :
    
        # yum clean all

    Sauf si vous créez une image pour une version antérieure de CentOS, il est recommandé de tooupdate que tous hello packages toohello dernière :

        # sudo yum -y update

    Un redémarrage peut être nécessaire après avoir exécuté cette commande.

11. (Facultatif) Installer des pilotes hello pour hello Services d’intégration Linux (LIS).
   
    >[!IMPORTANT]
    étape de Hello est **requis** pour CentOS 6.3 et antérieures et facultatives pour les versions ultérieures.

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    Ou bien, vous pouvez suivre les instructions d’installation manuelle hello sur hello [page de téléchargement LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM sur votre machine virtuelle.
 
12. Installez hello Linux Agent Azure et les dépendances :
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    package de WALinuxAgent hello supprimera hello NetworkManager et packages de NetworkManager-gnome si elles n’étaient pas déjà supprimées comme décrit à l’étape 3.


13. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo, ouvrez `/boot/grub/menu.lst` dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Cela garantit également tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.
    
    En outre toohello ci-dessus, il est recommandé de trop*supprimer* hello après les paramètres :
    
        rhgb quiet crashkernel=auto
    
    Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.  Hello `crashkernel` option peut être gauche configuré si vous le souhaitez, mais notez que ce paramètre réduit hello de mémoire disponible dans hello VM à 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites hello.

    >[!Important]
    CentOS 6.5 et versions antérieures doivent également définir des paramètres de noyau hello `numa=off`. Consultez Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

14. Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.  Cela est généralement hello par défaut.

15. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.
    
    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure. Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée. Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V. Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.


- - -
## <a name="centos-70"></a>CentOS 7.0+
**Modifications dans CentOS 7 (et les distributions dérivées)**

Préparation d’un ordinateur virtuel de CentOS 7 pour Azure est très similaire tooCentOS 6, cependant, il existe plusieurs différences importantes à noter :

* Hello NetworkManager du package n’est plus en conflit avec l’agent de hello Azure Linux. Ce package est installé par défaut ; nous recommandons de ne pas le supprimer.
* GRUB2 est désormais utilisé comme hello du chargeur de démarrage par défaut, afin de la procédure hello pour la modification des paramètres de noyau a changé (voir ci-dessous).
* XFS est désormais hello par défaut. système de fichiers ext4 Hello peut toujours être utilisé si vous le souhaitez.

**Configuration**

1. Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.

2. Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.

3. Créer ou modifier le fichier de hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Créer ou modifier le fichier de hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Modifier udev tooavoid de règles générant des règles statiques pour hello les interfaces Ethernet. Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. Si vous souhaitez que les miroirs OpenLogic toouse hello qui sont hébergés dans hello centres de données Azure, puis remplacez hello `/etc/yum.repos.d/CentOS-Base.repo` fichier avec hello suivant référentiels.  Cette action ajoutera également hello **[openlogic]** référentiel qui inclut des packages pour l’agent de hello Azure Linux :
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    Hello reste de ce guide suppose que vous utilisez au moins hello `[openlogic]` référentiel, qui sera utilisé tooinstall hello Azure Linux agent ci-dessous.

7. Exécutez hello suivant actuel yum métadonnées de commande tooclear hello et installer les mises à jour :
   
        # sudo yum clean all

    Sauf si vous créez une image pour une version antérieure de CentOS, il est recommandé de tooupdate que tous hello packages toohello dernière :

        # sudo yum -y update

    Un redémarrage peut être nécessaire après avoir exécuté cette commande.

8. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo, ouvrez `/etc/default/grub` un Bonjour éditeur et l’édition de texte `GRUB_CMDLINE_LINUX` paramètre, par exemple :
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Cela garantit également tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage. Il désactive également de nouvelles conventions de nommage CentOS 7 hello pour les cartes réseau. En outre toohello ci-dessus, il est recommandé de trop*supprimer* hello après les paramètres :
   
        rhgb quiet crashkernel=auto
   
    Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série. Hello `crashkernel` option peut être gauche configuré si vous le souhaitez, mais notez que ce paramètre réduit hello de mémoire disponible dans hello VM à 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites hello.

9. Une fois que vous avez terminé édition `/etc/default/grub` par ci-dessus, exécutez hello commande toorebuild hello grub configuration suivante :
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. Si la création d’image de système hello **VMWare, VirtualBox ou KVM :** Vérifiez que les pilotes hello Hyper-V sont inclus dans hello initramfs :
   
   Modifiez `/etc/dracut.conf`, ajoutez le contenu :
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   Reconstruire hello initramfs :
   
        # sudo dracut –f -v

11. Installez hello Linux Agent Azure et les dépendances :

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.
   
   Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure. Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée. Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V. Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt toouse votre CentOS Linux disque dur virtuel toocreate nouvelles machines virtuelles dans Azure. S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

