---
title: aaaPrepare un disque dur virtuel dans Azure de Debian Linux | Documents Microsoft
description: "Découvrez le fonctionnement des fichiers de toocreate Debian 7 et 8 de disque dur virtuel pour le déploiement dans Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a>Préparer un disque dur virtuel Debian pour Azure
## <a name="prerequisites"></a>Composants requis
Cette section part du principe que vous avez déjà installé un système d’exploitation de Debian Linux à partir d’un fichier .iso téléchargé à partir de hello [site Web Debian](https://www.debian.org/distrib/) tooa un disque dur virtuel. Toocreate les fichiers .vhd ; il existe plusieurs outils Hyper-V n'est qu’un exemple. Pour obtenir des instructions à l’aide de Hyper-V, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](https://technet.microsoft.com/library/hh846766.aspx).

## <a name="installation-notes"></a>Notes d'installation
* Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.
* nouveau format VHDX de Hello n’est pas pris en charge dans Azure. Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello **convert-vhd** applet de commande.
* Lors de l’installation de système de Linux hello, il est recommandé que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations). Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un système d’exploitation du disque jamais besoin toobe jointe tooanother machine virtuelle pour le dépannage. La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données, le cas échéant.
* Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello. l’agent de Hello Azure Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello. Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.
* Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.

## <a name="use-azure-manage-toocreate-debian-vhds"></a>Utilisez Azure-gérer les disques durs virtuels Debian du toocreate
Il existe des outils disponibles pour générer des disques durs virtuels Debian pour Azure, par exemple hello [azure-gérer](https://github.com/credativ/azure-manage) à partir de scripts [credativ](http://www.credativ.com/). Il s’agit de hello recommandé approche par rapport à la création d’une image à partir de zéro. Par exemple, toocreate un disque dur virtuel 8 Debian exécuter hello suivant les commandes de gestion azure toodownload (et dépendances) et script d’azure_build_image hello :

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a>Préparer manuellement un disque dur virtuel Debian
1. Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.
2. Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.
3. Commentez la ligne hello pour **deb cdrom** dans `/etc/apt/source.list` si vous configurez hello machine virtuelle par rapport à un fichier ISO.
4. Modifier hello `/etc/default/grub` et modifiez hello **GRUB_CMDLINE_LINUX** paramètre comme suit les paramètres de noyau supplémentaires tooinclude pour Azure.
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. Reconstruire les grub hello et exécutez :
   
        # sudo update-grub
6. Ajoutez Azure référentiels too/etc/apt/sources.list de Debian pour Debian 7 ou 8 :
   
    **Debian 7.x "Wheezy"**
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    **Debian 8.x "Jessie"**

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. Installez hello Linux Agent Azure :
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. Pour Debian 7, il est requis toorun hello 3.16 noyau à partir du référentiel de wheezy-backports hello. Tout d’abord créer un fichier appelé /etc/apt/preferences.d/linux.pref avec hello suivant le contenu :
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    Puis exécutez « sudo apt-get installer linux-image-amd64 » tooinstall hello nouveau noyau.
3. Annuler le déploiement d’ordinateur virtuel de hello et préparer pour la mise en service sur Azure et exécutez :
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. Cliquez sur **Action** -> Arrêter dans le Gestionnaire Hyper-V. Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt toouse votre disque dur Debian toocreate nouvelles machines virtuelles dans Azure. S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

