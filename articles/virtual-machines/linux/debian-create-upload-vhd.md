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
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="3f6d2-103">Préparer un disque dur virtuel Debian pour Azure</span><span class="sxs-lookup"><span data-stu-id="3f6d2-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="3f6d2-104">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3f6d2-104">Prerequisites</span></span>
<span data-ttu-id="3f6d2-105">Cette section part du principe que vous avez déjà installé un système d’exploitation de Debian Linux à partir d’un fichier .iso téléchargé à partir de hello [site Web Debian](https://www.debian.org/distrib/) tooa un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="3f6d2-106">Toocreate les fichiers .vhd ; il existe plusieurs outils Hyper-V n'est qu’un exemple.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="3f6d2-107">Pour obtenir des instructions à l’aide de Hyper-V, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f6d2-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="3f6d2-108">Notes d'installation</span><span class="sxs-lookup"><span data-stu-id="3f6d2-108">Installation notes</span></span>
* <span data-ttu-id="3f6d2-109">Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="3f6d2-110">nouveau format VHDX de Hello n’est pas pris en charge dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="3f6d2-111">Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello **convert-vhd** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="3f6d2-112">Lors de l’installation de système de Linux hello, il est recommandé que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations).</span><span class="sxs-lookup"><span data-stu-id="3f6d2-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="3f6d2-113">Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un système d’exploitation du disque jamais besoin toobe jointe tooanother machine virtuelle pour le dépannage.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="3f6d2-114">La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="3f6d2-115">Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="3f6d2-116">l’agent de Hello Azure Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="3f6d2-117">Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="3f6d2-118">Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="3f6d2-119">Utilisez Azure-gérer les disques durs virtuels Debian du toocreate</span><span class="sxs-lookup"><span data-stu-id="3f6d2-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="3f6d2-120">Il existe des outils disponibles pour générer des disques durs virtuels Debian pour Azure, par exemple hello [azure-gérer](https://github.com/credativ/azure-manage) à partir de scripts [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="3f6d2-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="3f6d2-121">Il s’agit de hello recommandé approche par rapport à la création d’une image à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="3f6d2-122">Par exemple, toocreate un disque dur virtuel 8 Debian exécuter hello suivant les commandes de gestion azure toodownload (et dépendances) et script d’azure_build_image hello :</span><span class="sxs-lookup"><span data-stu-id="3f6d2-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="3f6d2-123">Préparer manuellement un disque dur virtuel Debian</span><span class="sxs-lookup"><span data-stu-id="3f6d2-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="3f6d2-124">Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="3f6d2-125">Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="3f6d2-126">Commentez la ligne hello pour **deb cdrom** dans `/etc/apt/source.list` si vous configurez hello machine virtuelle par rapport à un fichier ISO.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="3f6d2-127">Modifier hello `/etc/default/grub` et modifiez hello **GRUB_CMDLINE_LINUX** paramètre comme suit les paramètres de noyau supplémentaires tooinclude pour Azure.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="3f6d2-128">Reconstruire les grub hello et exécutez :</span><span class="sxs-lookup"><span data-stu-id="3f6d2-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="3f6d2-129">Ajoutez Azure référentiels too/etc/apt/sources.list de Debian pour Debian 7 ou 8 :</span><span class="sxs-lookup"><span data-stu-id="3f6d2-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="3f6d2-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="3f6d2-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="3f6d2-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="3f6d2-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="3f6d2-132">Installez hello Linux Agent Azure :</span><span class="sxs-lookup"><span data-stu-id="3f6d2-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="3f6d2-133">Pour Debian 7, il est requis toorun hello 3.16 noyau à partir du référentiel de wheezy-backports hello.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="3f6d2-134">Tout d’abord créer un fichier appelé /etc/apt/preferences.d/linux.pref avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="3f6d2-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="3f6d2-135">Puis exécutez « sudo apt-get installer linux-image-amd64 » tooinstall hello nouveau noyau.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="3f6d2-136">Annuler le déploiement d’ordinateur virtuel de hello et préparer pour la mise en service sur Azure et exécutez :</span><span class="sxs-lookup"><span data-stu-id="3f6d2-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="3f6d2-137">Cliquez sur **Action** -> Arrêter dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="3f6d2-138">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f6d2-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f6d2-139">Next steps</span></span>
<span data-ttu-id="3f6d2-140">Vous êtes maintenant prêt toouse votre disque dur Debian toocreate nouvelles machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3f6d2-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="3f6d2-141">S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3f6d2-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

