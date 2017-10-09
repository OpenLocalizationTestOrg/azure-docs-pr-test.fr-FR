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
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="66a00-103">Préparation d'une machine virtuelle Linux Ubuntu pour Azure</span><span class="sxs-lookup"><span data-stu-id="66a00-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="66a00-104">Images cloud Ubuntu officielles</span><span class="sxs-lookup"><span data-stu-id="66a00-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="66a00-105">Ubuntu publie désormais des disques durs virtuels Azure officiels téléchargeables depuis l’adresse [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="66a00-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="66a00-106">Si vous devez toobuild votre propre image Ubuntu spécialisé pour Azure, au lieu d’utilisez la procédure manuelle de hello en dessous est recommandée toostart avec ces connus utilisation des disques durs virtuels et personnaliser autant que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="66a00-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="66a00-107">Vous trouverez toujours des dernières versions d’image Hello à hello emplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="66a00-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="66a00-108">Ubuntu 12.04/Precise : [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="66a00-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="66a00-109">Ubuntu 14.04/Trusty : [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="66a00-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="66a00-110">Ubuntu 16.04/Xenial : [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="66a00-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66a00-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="66a00-111">Prerequisites</span></span>
<span data-ttu-id="66a00-112">Cet article suppose que vous avez déjà installé un disque dur virtuel tooa Ubuntu Linux système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="66a00-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="66a00-113">Plusieurs outils existent toocreate les fichiers .vhd, par exemple une solution de virtualisation comme Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="66a00-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="66a00-114">Pour obtenir des instructions, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="66a00-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="66a00-115">**Notes d'installation Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="66a00-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="66a00-116">Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="66a00-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="66a00-117">format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**.</span><span class="sxs-lookup"><span data-stu-id="66a00-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="66a00-118">Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="66a00-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="66a00-119">Lors de l’installation de système de Linux hello, il est recommandé que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations).</span><span class="sxs-lookup"><span data-stu-id="66a00-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="66a00-120">Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un système d’exploitation du disque jamais besoin toobe jointe tooanother machine virtuelle pour le dépannage.</span><span class="sxs-lookup"><span data-stu-id="66a00-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="66a00-121">La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="66a00-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="66a00-122">Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="66a00-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="66a00-123">l’agent de Hello Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.</span><span class="sxs-lookup"><span data-stu-id="66a00-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="66a00-124">Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="66a00-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="66a00-125">Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="66a00-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="66a00-126">Étapes manuelles</span><span class="sxs-lookup"><span data-stu-id="66a00-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="66a00-127">Avant de tenter de toocreate votre propre image Ubuntu personnalisé pour Azure, pensez à l’aide de hello prégénérées et testé des images à partir de [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) à la place.</span><span class="sxs-lookup"><span data-stu-id="66a00-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="66a00-128">Dans le volet central de hello du Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="66a00-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="66a00-129">Cliquez sur **Connect** fenêtre hello de tooopen pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="66a00-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="66a00-130">Remplacez les référentiels actuelle de hello dans les référentiels Azure d’Ubuntu toouse hello image.</span><span class="sxs-lookup"><span data-stu-id="66a00-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="66a00-131">Hello étapes varient légèrement selon la version d’Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="66a00-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="66a00-132">Avant de modifier `/etc/apt/sources.list`, il est recommandé de toomake une sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="66a00-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="66a00-133">Ubuntu 12.04 :</span><span class="sxs-lookup"><span data-stu-id="66a00-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="66a00-134">Ubuntu 14.04 :</span><span class="sxs-lookup"><span data-stu-id="66a00-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="66a00-135">Ubuntu 16.04 :</span><span class="sxs-lookup"><span data-stu-id="66a00-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="66a00-136">Hello images d’Ubuntu Azure sont désormais les suivantes : hello *l’activation du matériel* noyau de (HOUE).</span><span class="sxs-lookup"><span data-stu-id="66a00-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="66a00-137">Mettre à jour du noyau de hello système d’exploitation toohello dernière hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="66a00-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="66a00-138">Ubuntu 12.04 :</span><span class="sxs-lookup"><span data-stu-id="66a00-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="66a00-139">Ubuntu 14.04 :</span><span class="sxs-lookup"><span data-stu-id="66a00-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="66a00-140">Ubuntu 16.04 :</span><span class="sxs-lookup"><span data-stu-id="66a00-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="66a00-141">**Voir aussi :**</span><span class="sxs-lookup"><span data-stu-id="66a00-141">**See also:**</span></span>
    - [<span data-ttu-id="66a00-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="66a00-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="66a00-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="66a00-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="66a00-144">Modifier la ligne de démarrage du noyau hello pour les paramètres de noyau supplémentaires tooinclude Grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="66a00-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="66a00-145">toodo ouvrir ce `/etc/default/grub` dans un éditeur de texte, recherchez variable hello appelée `GRUB_CMDLINE_LINUX_DEFAULT` (ou l’ajouter si nécessaire) et le modifier hello tooinclude paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="66a00-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="66a00-146">Enregistrez ce fichier, puis fermez-le. Exécutez ensuite la commande `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="66a00-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="66a00-147">Ainsi, tous les messages de console sont envoyés toohello premier port série, ce qui peut aider le support technique Azure avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="66a00-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="66a00-148">Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="66a00-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="66a00-149">Cela est généralement hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="66a00-149">This is usually hello default.</span></span>

7. <span data-ttu-id="66a00-150">Installez hello Linux Agent Azure :</span><span class="sxs-lookup"><span data-stu-id="66a00-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="66a00-151">Hello `walinuxagent` package peut supprimer hello `NetworkManager` et `NetworkManager-gnome` des packages, s’ils sont installés.</span><span class="sxs-lookup"><span data-stu-id="66a00-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="66a00-152">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="66a00-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="66a00-153">Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="66a00-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="66a00-154">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="66a00-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66a00-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66a00-155">Next steps</span></span>
<span data-ttu-id="66a00-156">Vous êtes maintenant prêt toouse votre Ubuntu Linux disque dur virtuel toocreate nouvelles machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="66a00-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="66a00-157">S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66a00-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="66a00-158">Références</span><span class="sxs-lookup"><span data-stu-id="66a00-158">References</span></span>
<span data-ttu-id="66a00-159">Noyau HWE (HardWare Enablement) Ubuntu :</span><span class="sxs-lookup"><span data-stu-id="66a00-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="66a00-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="66a00-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="66a00-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="66a00-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

