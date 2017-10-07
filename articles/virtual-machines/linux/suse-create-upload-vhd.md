---
title: "aaaCreate et téléchargez un disque dur virtuel de Linux SUSE dans Azure"
description: "En savoir plus toocreate et téléchargez un Azure disque dur virtuel (VHD) qui contient un système d’exploitation SUSE Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Préparation d'une machine virtuelle SLES ou openSUSE pour Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez déjà installé un SUSE ou un openSUSE Linux système d’exploitation tooa disque virtuel. Plusieurs outils existent toocreate les fichiers .vhd, par exemple une solution de virtualisation comme Hyper-V. Pour obtenir des instructions, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="sles--opensuse-installation-notes"></a>Notes d'installation SLES/openSUSE
* Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.
* format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**.  Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande convert-vhd.
* Lors de l’installation de système de Linux hello, il est recommandé que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations). Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un système d’exploitation du disque jamais besoin toobe jointe tooanother machine virtuelle pour le dépannage. La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données, le cas échéant.
* Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello. l’agent de Hello Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.  Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.
* Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.

## <a name="use-suse-studio"></a>Utilisation de SUSE Studio
[SUSE Studio](http://www.susestudio.com) peut facilement créer et gérer vos images SLES et openSUSE pour Azure et Hyper-V. Il s’agit de hello approche pour la personnalisation de vos propres images SLES et openSUSE recommandée.

En tant qu’une autre toobuilding votre propre disque dur virtuel, le SUSE publie également les images BYOS (apportez votre propre abonnement) pour SLES à [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>Préparation de SUSE Linux Enterprise Server 11 SP4
1. Dans le volet central de hello du Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.
2. Cliquez sur **Connect** fenêtre hello de tooopen pour la machine virtuelle de hello.
3. Inscrire votre tooallow de système de SUSE Linux Enterprise il toodownload les mises à jour et les packages d’installation.
4. Système de hello mise à jour avec les derniers correctifs de hello :
   
        # sudo zypper update
5. Installez hello Linux Agent Azure à partir du référentiel SLES hello :
   
        # sudo zypper install WALinuxAgent
6. Vérifiez si waagent est défini trop « on » dans la commande chkconfig et, dans le cas contraire, activez-le pour démarrer automatiquement :
   
        # sudo chkconfig waagent on
7. Vérifiez que le service waagent est en cours d’exécution et, dans le cas contraire, démarrez-le : 
   
        # sudo service waagent start
8. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo ouvrir ce « / boot/grub/menu.lst » dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    Ainsi, tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.
9. Confirmez que fstab /boot/grub/menu.lst et/etc/les deux disques hello de référence à l’aide de son UUID (par uuid) au lieu de l’ID du disque hello (par id). 
   
    Obtention de l’UUID du disque
   
        # ls /dev/disk/by-uuid/
   
    Si /dev/disk/by-id est utilisé, de mettre à jour /boot/grub/menu.lst et/etc/fstab avec la valeur appropriée par uuid de hello
   
    Avant la modification
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    Après la modification
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. Modifier udev tooavoid de règles générant des règles statiques pour hello les interfaces Ethernet. Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. Il est recommandé de fichier de hello tooedit « / etc/sysconfig/réseau/dhcp » et remplacez hello `DHCLIENT_SET_HOSTNAME` paramètre toohello suivant :
    
     DHCLIENT_SET_HOSTNAME="no"
12. Dans « / etc/programmes sudo », commentez ou supprimez les hello lignes suivantes si elles existent :
    
     Valeur par défaut est targetpw # demande hello de mot de passe de l’utilisateur cible de hello c'est-à-dire racine de tous les ALL=(ALL) tous les # avertissement ! N’utilisez cette option qu’avec « Defaults targetpw » !
13. Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.  Cela est généralement hello par défaut.
14. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.
    
    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure. Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée. Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello suivant correctement les paramètres dans /etc/waagent.conf :
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Remarque : définissez cette toowhatever vous en avez besoin toobe.
15. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
16. Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V. Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.

- - -
## <a name="prepare-opensuse-131"></a>Préparation de openSUSE 13.1+
1. Dans le volet central de hello du Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.
2. Cliquez sur **Connect** fenêtre hello de tooopen pour la machine virtuelle de hello.
3. Sur l’interpréteur de commandes hello, exécuter la commande hello '`zypper lr`'. Si cette commande renvoie la sortie similaire toohello suivant, puis les référentiels hello sont configurés comme prévu--aucune ajustements ne sont nécessaires (Notez que les numéros de version peuvent varier) :
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    Si la commande hello ne retourne « Aucun référentiel définies... » puis utilisez hello suivant de commandes tooadd ces référentiels :
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    Vous pouvez ensuite vérifier les référentiels hello ont été ajoutés en exécutant la commande hello '`zypper lr`' à nouveau. Dans le cas où un des référentiels de mise à jour appropriée hello n’est pas activé, activez-le avec la commande suivante :
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. Mise à jour hello noyau toohello version la plus récente :
   
        # sudo zypper up kernel-default
   
    Tooupdate hello système ou avec tous les correctifs les plus récents hello :
   
        # sudo zypper update
5. Installez hello Linux Agent Azure.
   
   # <a name="sudo-zypper-install-walinuxagent"></a>sudo zypper install WALinuxAgent
6. Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure. toodo, ouvrez « / boot/grub/menu.lst » dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :
   
     console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
   Ainsi, tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage. En outre, supprimez hello paramètres suivants à partir de la ligne de démarrage du noyau hello s’ils existent :
   
     libata.atapi_enabled=0 reserve=0x1f0,0x8
7. Il est recommandé de fichier de hello tooedit « / etc/sysconfig/réseau/dhcp » et remplacez hello `DHCLIENT_SET_HOSTNAME` paramètre toohello suivant :
   
     DHCLIENT_SET_HOSTNAME="no"
8. **Important :** dans « / etc/programmes sudo », supprimez ou commentez hello lignes suivantes si elles existent :
   
     Valeur par défaut est targetpw # demande hello de mot de passe de l’utilisateur cible de hello c'est-à-dire racine de tous les ALL=(ALL) tous les # avertissement ! N’utilisez cette option qu’avec « Defaults targetpw » !
9. Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.  Cela est généralement hello par défaut.
10. Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.
    
    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure. Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée. Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello suivant correctement les paramètres dans /etc/waagent.conf :
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Remarque : définissez cette toowhatever vous en avez besoin toobe.
11. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
12. Vérifiez que hello Qu'agent Linux Azure s’exécute au démarrage :
    
        # sudo systemctl enable waagent.service
13. Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V. Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt toouse votre SUSE Linux disque dur virtuel toocreate nouvelles machines virtuelles dans Azure. S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

