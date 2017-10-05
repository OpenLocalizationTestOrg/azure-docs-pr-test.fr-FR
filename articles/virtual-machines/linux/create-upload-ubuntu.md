---
title: "Création et téléchargement d'un disque dur virtuel Linux Ubuntu dans Azure"
description: "Apprenez à créer et à charger un disque dur virtuel (VHD) Azure contenant un système d'exploitation Linux Ubuntu."
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
ms.openlocfilehash: 4496b34ff88ca1e08cc74788ae09d787d4399eaf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="36fc0-103">Préparation d'une machine virtuelle Linux Ubuntu pour Azure</span><span class="sxs-lookup"><span data-stu-id="36fc0-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="36fc0-104">Images cloud Ubuntu officielles</span><span class="sxs-lookup"><span data-stu-id="36fc0-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="36fc0-105">Ubuntu publie désormais des disques durs virtuels Azure officiels téléchargeables depuis l’adresse [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="36fc0-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="36fc0-106">Si vous avez besoin de créer votre propre image Ubuntu spécialisée pour Azure, plutôt que d’utiliser la procédure manuelle ci-après, nous vous recommandons de démarrer avec ces disques durs virtuels opérationnels connus et de les personnaliser selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="36fc0-106">If you need to build your own specialized Ubuntu image for Azure, rather than use the manual procedure below it is recommended to start with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="36fc0-107">Les dernières versions de l’image se trouvent toujours aux emplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="36fc0-107">The latest image releases can always be found at the following locations:</span></span>

* <span data-ttu-id="36fc0-108">Ubuntu 12.04/Precise : [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="36fc0-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="36fc0-109">Ubuntu 14.04/Trusty : [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="36fc0-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="36fc0-110">Ubuntu 16.04/Xenial : [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="36fc0-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36fc0-111">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="36fc0-111">Prerequisites</span></span>
<span data-ttu-id="36fc0-112">Cet article suppose que vous avez déjà installé un système d'exploitation Linux Ubuntu dans un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="36fc0-112">This article assumes that you have already installed an Ubuntu Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="36fc0-113">Il existe de multiples outils dédiés à la création de fichiers .vhd, comme la solution de virtualisation Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="36fc0-113">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="36fc0-114">Pour obtenir des instructions, consultez la page [Installation du rôle Hyper-V et configuration d'une machine virtuelle](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="36fc0-114">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="36fc0-115">**Notes d'installation Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="36fc0-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="36fc0-116">Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="36fc0-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="36fc0-117">Azure ne prend pas en charge le format VHDX, seulement le **VHD fixe**.</span><span class="sxs-lookup"><span data-stu-id="36fc0-117">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="36fc0-118">Vous pouvez convertir le disque au format VHD à l'aide de Hyper-V Manager ou de l’applet de commande convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="36fc0-118">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="36fc0-119">Lors de l’installation du système Linux, il est recommandé d’utiliser les partitions standard plutôt que LVM (qui est souvent le choix par défaut pour de nombreuses installations).</span><span class="sxs-lookup"><span data-stu-id="36fc0-119">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="36fc0-120">Ceci permettra d'éviter les conflits de noms avec des machines virtuelles clonées, notamment si un disque de système d'exploitation doit être relié à une autre machine virtuelle pour la dépanner.</span><span class="sxs-lookup"><span data-stu-id="36fc0-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="36fc0-121">La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="36fc0-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="36fc0-122">Ne configurez pas une partition d'échange sur le disque du système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="36fc0-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="36fc0-123">L'agent Linux est configurable pour créer un fichier d'échange sur le disque de ressources temporaire.</span><span class="sxs-lookup"><span data-stu-id="36fc0-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="36fc0-124">Les étapes ci-dessous fournissent plus d'informations à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="36fc0-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="36fc0-125">La taille des disques durs virtuels doit être un multiple de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="36fc0-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="36fc0-126">Étapes manuelles</span><span class="sxs-lookup"><span data-stu-id="36fc0-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="36fc0-127">Avant d’essayer de créer votre propre image Ubuntu personnalisée pour Azure, envisagez d’utiliser les images préconçues et testées disponibles à l’adresse [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) .</span><span class="sxs-lookup"><span data-stu-id="36fc0-127">Before attempting to create your own custom Ubuntu image for Azure, please consider using the pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="36fc0-128">Dans le panneau central de Hyper-V Manager, sélectionnez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="36fc0-128">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="36fc0-129">Cliquez sur **Connect** pour ouvrir la fenêtre de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="36fc0-129">Click **Connect** to open the window for the virtual machine.</span></span>

3. <span data-ttu-id="36fc0-130">Remplacez les référentiels actuels dans l'image par les référentiels Azure Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="36fc0-130">Replace the current repositories in the image to use Ubuntu's Azure repos.</span></span> <span data-ttu-id="36fc0-131">Les étapes varient légèrement selon la version d'Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="36fc0-131">The steps vary slightly depending on the Ubuntu version.</span></span>
   
    <span data-ttu-id="36fc0-132">Avant de modifier `/etc/apt/sources.list`, il est recommandé d’effectuer une sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="36fc0-132">Before editing `/etc/apt/sources.list`, it is recommended to make a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="36fc0-133">Ubuntu 12.04 :</span><span class="sxs-lookup"><span data-stu-id="36fc0-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="36fc0-134">Ubuntu 14.04 :</span><span class="sxs-lookup"><span data-stu-id="36fc0-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="36fc0-135">Ubuntu 16.04 :</span><span class="sxs-lookup"><span data-stu-id="36fc0-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="36fc0-136">Les images Ubuntu Azure suivent désormais le noyau *HWE* (HardWare Enablement).</span><span class="sxs-lookup"><span data-stu-id="36fc0-136">The Ubuntu Azure images are now following the *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="36fc0-137">Exécutez les commandes suivantes pour mettre à jour le système d’exploitation avec le dernier noyau :</span><span class="sxs-lookup"><span data-stu-id="36fc0-137">Update the operating system to the latest kernel by running the following commands:</span></span>

    <span data-ttu-id="36fc0-138">Ubuntu 12.04 :</span><span class="sxs-lookup"><span data-stu-id="36fc0-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="36fc0-139">Ubuntu 14.04 :</span><span class="sxs-lookup"><span data-stu-id="36fc0-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="36fc0-140">Ubuntu 16.04 :</span><span class="sxs-lookup"><span data-stu-id="36fc0-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="36fc0-141">**Voir aussi :**</span><span class="sxs-lookup"><span data-stu-id="36fc0-141">**See also:**</span></span>
    - [<span data-ttu-id="36fc0-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="36fc0-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="36fc0-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="36fc0-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="36fc0-144">Modifiez la ligne de démarrage du noyau afin que Grub y inclue les paramètres de noyau supplémentaires pour Azure.</span><span class="sxs-lookup"><span data-stu-id="36fc0-144">Modify the kernel boot line for Grub to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="36fc0-145">Pour cela, ouvrez le fichier `/etc/default/grub` dans un éditeur de texte. Recherchez la variable nommée `GRUB_CMDLINE_LINUX_DEFAULT` (ou ajoutez-la le cas échéant) et modifiez-la pour inclure les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="36fc0-145">To do this open `/etc/default/grub` in a text editor, find the variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it to include the following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="36fc0-146">Enregistrez ce fichier, puis fermez-le. Exécutez ensuite la commande `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="36fc0-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="36fc0-147">Ce permet d'assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour l'assistance technique d'Azure.</span><span class="sxs-lookup"><span data-stu-id="36fc0-147">This will ensure all console messages are sent to the first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="36fc0-148">Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu.</span><span class="sxs-lookup"><span data-stu-id="36fc0-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="36fc0-149">C'est généralement le cas par défaut.</span><span class="sxs-lookup"><span data-stu-id="36fc0-149">This is usually the default.</span></span>

7. <span data-ttu-id="36fc0-150">Installez l'agent Linux Azure :</span><span class="sxs-lookup"><span data-stu-id="36fc0-150">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="36fc0-151">Le package `walinuxagent` peut entraîner la suppression des packages `NetworkManager` et `NetworkManager-gnome` (s’ils sont installés).</span><span class="sxs-lookup"><span data-stu-id="36fc0-151">The `walinuxagent` package may remove the `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="36fc0-152">Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :</span><span class="sxs-lookup"><span data-stu-id="36fc0-152">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="36fc0-153">Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="36fc0-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="36fc0-154">Votre disque dur virtuel Linux est alors prêt pour le téléchargement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="36fc0-154">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36fc0-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36fc0-155">Next steps</span></span>
<span data-ttu-id="36fc0-156">Vous êtes maintenant prêt à utiliser votre disque dur virtuel Ubuntu Linux pour créer des machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="36fc0-156">You're now ready to use your Ubuntu Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="36fc0-157">S’il s’agit de la première fois que vous chargez le fichier .vhd sur Azure, consultez les étapes 2 et 3 dans [Création et chargement d’un disque dur virtuel contenant le système d’exploitation Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36fc0-157">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="36fc0-158">Références</span><span class="sxs-lookup"><span data-stu-id="36fc0-158">References</span></span>
<span data-ttu-id="36fc0-159">Noyau HWE (HardWare Enablement) Ubuntu :</span><span class="sxs-lookup"><span data-stu-id="36fc0-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="36fc0-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="36fc0-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="36fc0-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="36fc0-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

