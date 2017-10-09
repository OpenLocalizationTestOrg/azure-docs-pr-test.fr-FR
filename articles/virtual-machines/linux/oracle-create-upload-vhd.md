---
title: "aaaCreate et télécharger un disque dur virtuel de Oracle Linux | Documents Microsoft"
description: "En savoir plus toocreate et téléchargez un Azure disque dur virtuel (VHD) qui contient un système d’exploitation de Oracle Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>Préparation d’une machine virtuelle Linux Oracle pour Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez déjà installé un disque dur virtuel tooa Oracle Linux système d’exploitation. Plusieurs outils existent toocreate les fichiers .vhd, par exemple une solution de virtualisation comme Hyper-V. Pour obtenir des instructions, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="oracle-linux-installation-notes"></a>Notes générales d’installation d’Oracle Linux
* Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.
* Le noyau Oracle compatible Red Hat et leur noyau UEK3 (Unbreakable Enterprise Kernel) sont tous les deux pris en charge sur Hyper-V et Azure. Pour de meilleurs résultats, soyez noyau de dernière toohello tooupdate que lors de la préparation de votre disque dur virtuel de Oracle Linux.
* Oracle UEK2 n’est pas prise en charge Hyper-V et sur Azure qu’il n’inclut pas les pilotes hello requis.
* format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**.  Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande convert-vhd.
* Lors de l’installation de système de Linux hello, il est recommandé que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations). Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un système d’exploitation du disque jamais besoin toobe jointe tooanother machine virtuelle pour le dépannage. La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données, le cas échéant.
* NUMA n’est pas pris en charge pour les tailles de machine virtuelle plus grandes en raison du bogue tooa dans les versions de noyau Linux ci-dessous 2.6.37. Ce problème principalement les impacts à l’aide de distributions hello rouge en amont noyau de Hat 2.6.32. Installation manuelle de l’agent Azure Linux de hello (waagent) sera automatiquement désactivée NUMA dans la configuration de GRUB hello pour le noyau Linux de hello. Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.
* Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello. l’agent de Hello Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.  Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.
* Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.
* Vérifiez que hello `Addons` référentiel est activé. Modifier le fichier de hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) et remplacez-la par hello `enabled=0` trop`enabled=1` sous **[ol6_addons]** ou **[ol7_addons]** dans cette fichier.

## <a name="oracle-linux-64"></a>Oracle Linux 6.4+
Vous devez effectuer les étapes de configuration spécifique dans le système d’exploitation hello toorun de machine virtuelle hello dans Azure.

1. Dans le volet central de hello du Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.
2. Cliquez sur **Connect** fenêtre hello de tooopen pour la machine virtuelle de hello.
3. Désinstaller NetworkManager en exécutant hello de commande suivante :
   
        # sudo rpm -e --nodeps NetworkManager
   
    **Remarque :** si le package de hello n’est pas déjà installé, cette commande échoue avec un message d’erreur. Ceci est normal.
4. Créez un fichier nommé **réseau** Bonjour `/etc/sysconfig/` répertoire contenant hello suivant du texte :
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. Créez un fichier nommé **ifcfg-eth0** Bonjour `/etc/sysconfig/network-scripts/` répertoire contenant hello suivant du texte :
   
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
   
        # chkconfig network on
8. Installer python-pyasn1 en exécutant hello de commande suivante :
   
        # sudo yum install python-pyasn1
9. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo ouvrir ce « / boot/grub/menu.lst » dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   Cela garantit également tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage. Cette opération va désactiver NUMA en raison du bogue tooa dans le noyau compatible de Red Hat d’Oracle.
   
   En outre toohello ci-dessus, il est recommandé de trop*supprimer* hello après les paramètres :
   
        rhgb quiet crashkernel=auto
   
   Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.
   
   Hello `crashkernel` option peut être gauche configuré si vous le souhaitez, mais notez que ce paramètre réduit hello de mémoire disponible dans hello VM à 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites hello.
10. Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.  Cela est généralement hello par défaut.
11. Installez hello Linux Agent Azure en exécutant hello commande suivante. version la plus récente Hello est 2.0.15.
    
        # sudo yum install WALinuxAgent
    
    Notez que le lot d’installation hello WALinuxAgent supprimera hello NetworkManager et packages de NetworkManager-gnome si elles n’étaient pas déjà supprimées comme décrit à l’étape 2.
12. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.
    
    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure. Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée. Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello suivant correctement les paramètres dans /etc/waagent.conf :
    
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

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0+
**Modifications dans Oracle Linux 7**

Préparation d’une machine virtuelle de Oracle Linux 7 pour Azure est très similaire tooOracle Linux 6, cependant, il existe plusieurs différences importantes à noter :

* Noyau compatible de hello Red Hat et UEK3 d’Oracle sont pris en charge dans Azure.  noyau de UEK3 Hello est recommandé.
* Hello NetworkManager du package n’est plus en conflit avec l’agent de hello Azure Linux. Ce package est installé par défaut ; nous recommandons de ne pas le supprimer.
* GRUB2 est désormais utilisé comme hello du chargeur de démarrage par défaut, afin de la procédure hello pour la modification des paramètres de noyau a changé (voir ci-dessous).
* XFS est désormais hello par défaut. système de fichiers ext4 Hello peut toujours être utilisé si vous le souhaitez.

**Configuration**

1. Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.
2. Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.
3. Créez un fichier nommé **réseau** Bonjour `/etc/sysconfig/` répertoire contenant hello suivant du texte :
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. Créez un fichier nommé **ifcfg-eth0** Bonjour `/etc/sysconfig/network-scripts/` répertoire contenant hello suivant du texte :
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. Modifier udev tooavoid de règles générant des règles statiques pour hello les interfaces Ethernet. Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. Vérifiez que hello network service démarre au moment du démarrage en cours d’exécution hello de commande suivante :
   
        # sudo chkconfig network on
7. Installer le package de python-pyasn1 de hello en exécutant hello de commande suivante :
   
        # sudo yum install python-pyasn1
8. Exécutez hello suivant actuel yum métadonnées de commande tooclear hello et installer les mises à jour :
   
        # sudo yum clean all
        # sudo yum -y update
9. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo ce Ouvrez « / etc/par défaut/grub » dans un hello éditeur et l’édition de texte `GRUB_CMDLINE_LINUX` paramètre, par exemple :
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Cela garantit également tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage. Il désactive également de nouvelles conventions de nommage OEL 7 hello pour les cartes réseau. En outre toohello ci-dessus, il est recommandé de trop*supprimer* hello après les paramètres :
   
       rhgb quiet crashkernel=auto
   
   Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.
   
   Hello `crashkernel` option peut être gauche configuré si vous le souhaitez, mais notez que ce paramètre réduit hello de mémoire disponible dans hello VM à 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites hello.
10. Une fois que vous avez terminé la modification « / etc/par défaut/grub » par ci-dessus, exécutez hello commande toorebuild hello grub configuration suivante :
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.  Cela est généralement hello par défaut.
12. Installez hello Linux Agent Azure en exécutant hello de commande suivante :
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.
    
    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure. Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée. Après avoir installé hello Linux Agent Azure (voir l’étape précédente de hello), modifier hello suivant correctement les paramètres dans /etc/waagent.conf :
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V. Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt toouse votre Oracle Linux .vhd toocreate nouvelles machines virtuelles dans Azure. S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

