---
title: "aaaCreate et téléchargez un disque dur virtuel de Linux Ubuntu dans Azure"
description: "En savoir plus toocreate et téléchargez un Azure disque dur virtuel (VHD) qui contient un système d’exploitation Ubuntu Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>Préparation d'une machine virtuelle Linux Ubuntu pour Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>Images cloud Ubuntu officielles
Ubuntu publie désormais des disques durs virtuels Azure officiels téléchargeables depuis l’adresse [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/). Si vous devez toobuild votre propre image Ubuntu spécialisé pour Azure, au lieu d’utilisez la procédure manuelle de hello en dessous est recommandée toostart avec ces connus utilisation des disques durs virtuels et personnaliser autant que nécessaire. Vous trouverez toujours des dernières versions d’image Hello à hello emplacements suivants :

* Ubuntu 12.04/Precise : [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/Trusty : [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial : [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez déjà installé un disque dur virtuel tooa Ubuntu Linux système d’exploitation. Plusieurs outils existent toocreate les fichiers .vhd, par exemple une solution de virtualisation comme Hyper-V. Pour obtenir des instructions, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](http://technet.microsoft.com/library/hh846766.aspx).

**Notes d'installation Ubuntu**

* Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.
* format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**.  Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande convert-vhd.
* Lors de l’installation de système de Linux hello, il est recommandé que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations). Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un système d’exploitation du disque jamais besoin toobe jointe tooanother machine virtuelle pour le dépannage. La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données, le cas échéant.
* Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello. l’agent de Hello Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.  Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.
* Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.

## <a name="manual-steps"></a>Étapes manuelles
> [!NOTE]
> Avant de tenter de toocreate votre propre image Ubuntu personnalisé pour Azure, pensez à l’aide de hello prégénérées et testé des images à partir de [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) à la place.
> 
> 

1. Dans le volet central de hello du Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.

2. Cliquez sur **Connect** fenêtre hello de tooopen pour la machine virtuelle de hello.

3. Remplacez les référentiels actuelle de hello dans les référentiels Azure d’Ubuntu toouse hello image. Hello étapes varient légèrement selon la version d’Ubuntu hello.
   
    Avant de modifier `/etc/apt/sources.list`, il est recommandé de toomake une sauvegarde :
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12.04 :
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04 :
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04 :
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. Hello images d’Ubuntu Azure sont désormais les suivantes : hello *l’activation du matériel* noyau de (HOUE). Mettre à jour du noyau de hello système d’exploitation toohello dernière hello suivant les commandes en cours d’exécution :

    Ubuntu 12.04 :
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04 :
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04 :
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **Voir aussi :**
    - [https://wiki.ubuntu.com/Kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. Modifier la ligne de démarrage du noyau hello pour les paramètres de noyau supplémentaires tooinclude Grub pour Azure. toodo ouvrir ce `/etc/default/grub` dans un éditeur de texte, recherchez variable hello appelée `GRUB_CMDLINE_LINUX_DEFAULT` (ou l’ajouter si nécessaire) et le modifier hello tooinclude paramètres suivants :
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    Enregistrez ce fichier, puis fermez-le. Exécutez ensuite la commande `sudo update-grub`. Ainsi, tous les messages de console sont envoyés toohello premier port série, ce qui peut aider le support technique Azure avec les problèmes de débogage.

6. Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.  Cela est généralement hello par défaut.

7. Installez hello Linux Agent Azure :
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    Hello `walinuxagent` package peut supprimer hello `NetworkManager` et `NetworkManager-gnome` des packages, s’ils sont installés.

8. Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V. Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt toouse votre Ubuntu Linux disque dur virtuel toocreate nouvelles machines virtuelles dans Azure. S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="references"></a>Références
Noyau HWE (HardWare Enablement) Ubuntu :

* [http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

