---
title: "Création et téléchargement d'un VHD Oracle Linux | Microsoft Docs"
description: "Apprenez à créer et à télécharger un disque dur virtuel (VHD) Azure contenant un système d'exploitation Oracle Linux."
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
ms.openlocfilehash: c631ddf3acf6df7364c03eb4691b78be0493e0d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="504d5-103">Préparation d’une machine virtuelle Linux Oracle pour Azure</span><span class="sxs-lookup"><span data-stu-id="504d5-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="504d5-104">Composants requis</span><span class="sxs-lookup"><span data-stu-id="504d5-104">Prerequisites</span></span>
<span data-ttu-id="504d5-105">Cet article suppose que vous avez déjà installé un système d'exploitation Oracle Linux dans un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="504d5-105">This article assumes that you have already installed an Oracle Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="504d5-106">Il existe de multiples outils dédiés à la création de fichiers .vhd, comme la solution de virtualisation Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="504d5-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="504d5-107">Pour obtenir des instructions, consultez la page [Installation du rôle Hyper-V et configuration d'une machine virtuelle](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="504d5-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="504d5-108">Notes générales d’installation d’Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="504d5-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="504d5-109">Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="504d5-110">Le noyau Oracle compatible Red Hat et leur noyau UEK3 (Unbreakable Enterprise Kernel) sont tous les deux pris en charge sur Hyper-V et Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="504d5-111">Pour de meilleurs résultats, n'oubliez pas de mettre à jour le noyau lorsque vous préparez votre disque dur virtuel Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="504d5-111">For best results, please be sure to update to the latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="504d5-112">Le noyau UEK2 d'Oracle n'est pas pris en charge sur Hyper-V et Azure, car il ne comporte pas les pilotes nécessaires.</span><span class="sxs-lookup"><span data-stu-id="504d5-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include the required drivers.</span></span>
* <span data-ttu-id="504d5-113">Azure ne prend pas en charge le format VHDX, seulement le **VHD fixe**.</span><span class="sxs-lookup"><span data-stu-id="504d5-113">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="504d5-114">Vous pouvez convertir le disque au format VHD à l'aide de Hyper-V Manager ou de l’applet de commande convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="504d5-114">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="504d5-115">Lors de l’installation du système Linux, il est recommandé d’utiliser les partitions standard plutôt que LVM (qui est souvent le choix par défaut pour de nombreuses installations).</span><span class="sxs-lookup"><span data-stu-id="504d5-115">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="504d5-116">Ceci permettra d'éviter les conflits de noms avec des machines virtuelles clonées, notamment si un disque de système d'exploitation doit être relié à une autre machine virtuelle pour la dépanner.</span><span class="sxs-lookup"><span data-stu-id="504d5-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="504d5-117">La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) est utilisable sur les disques de données, si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="504d5-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="504d5-118">NUMA n'est pas pris en charge pour les tailles de machines virtuelles plus élevées en raison d'un bogue dans les versions du noyau Linux inférieures à 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="504d5-118">NUMA is not supported for larger VM sizes due to a bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="504d5-119">Ce problème touche spécialement les distributions utilisant le noyau Red Hat 2.6.32 en amont.</span><span class="sxs-lookup"><span data-stu-id="504d5-119">This issue primarily impacts distributions using the upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="504d5-120">L'installation manuelle de l'Agent Linux Azure (waagent) désactive automatiquement NUMA dans la configuration GRUB pour le noyau Linux.</span><span class="sxs-lookup"><span data-stu-id="504d5-120">Manual installation of the Azure Linux agent (waagent) will automatically disable NUMA in the GRUB configuration for the Linux kernel.</span></span> <span data-ttu-id="504d5-121">Les étapes ci-dessous fournissent plus d'informations à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="504d5-121">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="504d5-122">Ne configurez pas une partition d'échange sur le disque du système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="504d5-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="504d5-123">L'agent Linux est configurable pour créer un fichier d'échange sur le disque de ressources temporaire.</span><span class="sxs-lookup"><span data-stu-id="504d5-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="504d5-124">Les étapes ci-dessous fournissent plus d'informations à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="504d5-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="504d5-125">La taille des disques durs virtuels doit être un multiple de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="504d5-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="504d5-126">Assurez-vous que le référentiel `Addons` est activé.</span><span class="sxs-lookup"><span data-stu-id="504d5-126">Make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="504d5-127">Modifiez le fichier `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux), remplacez la ligne `enabled=0` par `enabled=1` sous **[ol6_addons]** ou **[ol7_addons]** dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="504d5-127">Edit the file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="504d5-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="504d5-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="504d5-129">Vous devez suivre des étapes de configuration spécifiques dans le système d'exploitation afin que la machine virtuelle fonctionne sur Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-129">You must complete specific configuration steps in the operating system for the virtual machine to run in Azure.</span></span>

1. <span data-ttu-id="504d5-130">Dans le panneau central de Hyper-V Manager, sélectionnez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="504d5-130">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="504d5-131">Cliquez sur **Connect** pour ouvrir la fenêtre de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="504d5-131">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="504d5-132">Exécutez la commande suivante pour désinstaller NetworkManager :</span><span class="sxs-lookup"><span data-stu-id="504d5-132">Uninstall NetworkManager by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="504d5-133">**Remarque :** si le package n’est pas déjà installé, la commande échoue et un message d’erreur s’affiche.</span><span class="sxs-lookup"><span data-stu-id="504d5-133">**Note:** If the package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="504d5-134">Ceci est normal.</span><span class="sxs-lookup"><span data-stu-id="504d5-134">This is expected.</span></span>
4. <span data-ttu-id="504d5-135">Créez un fichier nommé **network** in the `/etc/sysconfig/` et entrez-y le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="504d5-135">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="504d5-136">Créez un fichier nommé **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` et entrez-y le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="504d5-136">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="504d5-137">Modifiez les règles udev pour éviter la génération de règles statiques pour les interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="504d5-137">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="504d5-138">Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="504d5-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="504d5-139">Assurez-vous que le service réseau commencera aux heures de démarrage en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="504d5-139">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="504d5-140">Saisissez la commande suivante pour installer python-pyasn1 :</span><span class="sxs-lookup"><span data-stu-id="504d5-140">Install python-pyasn1 by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="504d5-141">Modifiez la ligne de démarrage du noyau dans votre configuration grub pour y inclure les paramètres de noyau supplémentaires pour Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="504d5-142">Pour cela, ouvrez le fichier « /boot/grub/menu.lst » dans un éditeur de texte et vérifiez que le noyau par défaut comprend les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="504d5-142">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="504d5-143">Ce permet également d'assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour la prise en charge d'Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-143">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="504d5-144">Cela désactive NUMA en raison d'une erreur dans le noyau compatible Red Hat d'Oracle.</span><span class="sxs-lookup"><span data-stu-id="504d5-144">This will disable NUMA due to a bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="504d5-145">Outre les précautions ci-dessus, il est recommandé de *supprimer* les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="504d5-145">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="504d5-146">Le démarrage graphique et transparent n'est pas utile dans un environnement cloud où nous voulons que tous les journaux soient envoyés au port série.</span><span class="sxs-lookup"><span data-stu-id="504d5-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="504d5-147">L’option `crashkernel` peut éventuellement être conservée. Notez cependant que ce paramètre réduit la quantité de mémoire disponible dans la machine virtuelle de 128 Mo ou plus, ce qui peut être problématique sur les machines virtuelles de petite taille.</span><span class="sxs-lookup"><span data-stu-id="504d5-147">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="504d5-148">Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu.</span><span class="sxs-lookup"><span data-stu-id="504d5-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="504d5-149">C'est généralement le cas par défaut.</span><span class="sxs-lookup"><span data-stu-id="504d5-149">This is usually the default.</span></span>
11. <span data-ttu-id="504d5-150">Installez l’agent Linux Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="504d5-150">Install the Azure Linux Agent by running the following command.</span></span> <span data-ttu-id="504d5-151">La version la plus récente est la 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="504d5-151">The latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="504d5-152">L'installation du package WALinuxAgent entraîne la suppression des packages NetworkManager et NetworkManager-gnome, s'ils n'avaient pas déjà été supprimés comme indiqué à l'étape 2.</span><span class="sxs-lookup"><span data-stu-id="504d5-152">Note that installing the WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="504d5-153">Ne créez pas d'espace swap sur le disque du système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="504d5-153">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="504d5-154">L'agent Linux Azure peut configurer automatiquement un espace swap à l'aide du disque local de ressources connecté à la machine virtuelle après déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-154">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="504d5-155">Notez que le disque de ressources local est un disque *temporaire* et qu'il peut être vidé lors de l'annulation de l'approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="504d5-155">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="504d5-156">Après avoir installé l'agent Linux Azure (voir l'étape précédente), modifiez les paramètres suivants dans le fichier /etc/waagent.conf :</span><span class="sxs-lookup"><span data-stu-id="504d5-156">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
13. <span data-ttu-id="504d5-157">Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :</span><span class="sxs-lookup"><span data-stu-id="504d5-157">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="504d5-158">Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="504d5-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="504d5-159">Votre disque dur virtuel Linux est alors prêt pour le téléchargement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-159">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="504d5-160">Oracle Linux 7.0+</span><span class="sxs-lookup"><span data-stu-id="504d5-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="504d5-161">**Modifications dans Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="504d5-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="504d5-162">La préparation d'une machine virtuelle Oracle Linux 7 pour Azure est très similaire à Oracle Linux 6 ; cependant, certaines différences importantes méritent d'être notées :</span><span class="sxs-lookup"><span data-stu-id="504d5-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar to Oracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="504d5-163">Le noyau compatible Red Hat et le noyau UEK3 d'Oracle sont pris en charge dans Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-163">Both the Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="504d5-164">Le noyau UEK3 est recommandé.</span><span class="sxs-lookup"><span data-stu-id="504d5-164">The UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="504d5-165">Le package NetworkManager n'est plus en conflit avec l'agent Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="504d5-165">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="504d5-166">Ce package est installé par défaut ; nous recommandons de ne pas le supprimer.</span><span class="sxs-lookup"><span data-stu-id="504d5-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="504d5-167">GRUB2 est maintenant utilisé comme chargeur de démarrage (bootloader) par défaut ; la modification des paramètres du noyau a donc changé (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="504d5-167">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="504d5-168">XFS est maintenant le système de fichiers par défaut.</span><span class="sxs-lookup"><span data-stu-id="504d5-168">XFS is now the default file system.</span></span> <span data-ttu-id="504d5-169">Le système de fichiers ext4 est toujours utilisable si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="504d5-169">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="504d5-170">**Configuration**</span><span class="sxs-lookup"><span data-stu-id="504d5-170">**Configuration steps**</span></span>

1. <span data-ttu-id="504d5-171">Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="504d5-171">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="504d5-172">Cliquez sur **Connecter** pour ouvrir une fenêtre de console de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="504d5-172">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="504d5-173">Créez un fichier nommé **network** in the `/etc/sysconfig/` et entrez-y le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="504d5-173">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="504d5-174">Créez un fichier nommé **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` et entrez-y le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="504d5-174">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="504d5-175">Modifiez les règles udev pour éviter la génération de règles statiques pour les interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="504d5-175">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="504d5-176">Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="504d5-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="504d5-177">Assurez-vous que le service réseau commencera aux heures de démarrage en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="504d5-177">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="504d5-178">Exécutez la commande suivante pour installer le package python-pyasn1 :</span><span class="sxs-lookup"><span data-stu-id="504d5-178">Install the python-pyasn1 package by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="504d5-179">Exécutez la commande suivante pour effacer les métadonnées yum actuelles et installer les mises à jour le cas échéant :</span><span class="sxs-lookup"><span data-stu-id="504d5-179">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="504d5-180">Modifiez la ligne de démarrage du noyau dans votre configuration grub pour y inclure les paramètres de noyau supplémentaires pour Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-180">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="504d5-181">Pour cela, ouvrez le fichier « /etc/default/grub » dans un éditeur de texte et modifiez le paramètre `GRUB_CMDLINE_LINUX` , par exemple :</span><span class="sxs-lookup"><span data-stu-id="504d5-181">To do this open "/etc/default/grub" in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="504d5-182">Ce permet également d'assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour la prise en charge d'Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-182">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="504d5-183">Cela désactive également les nouvelles conventions d’affectation de noms OEL 7 pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="504d5-183">It also turns off the new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="504d5-184">Outre les précautions ci-dessus, il est recommandé de *supprimer* les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="504d5-184">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="504d5-185">Le démarrage graphique et transparent n'est pas utile dans un environnement cloud où nous voulons que tous les journaux soient envoyés au port série.</span><span class="sxs-lookup"><span data-stu-id="504d5-185">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="504d5-186">L’option `crashkernel` peut éventuellement être conservée. Notez cependant que ce paramètre réduit la quantité de mémoire disponible dans la machine virtuelle de 128 Mo ou plus, ce qui peut être problématique sur les machines virtuelles de petite taille.</span><span class="sxs-lookup"><span data-stu-id="504d5-186">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="504d5-187">Lorsque vous avez fini de modifier le fichier « /etc/default/grub », exécutez la commande suivante pour régénérer la configuration grub :</span><span class="sxs-lookup"><span data-stu-id="504d5-187">Once you are done editing "/etc/default/grub" per above, run the following command to rebuild the grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="504d5-188">Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu.</span><span class="sxs-lookup"><span data-stu-id="504d5-188">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="504d5-189">C'est généralement le cas par défaut.</span><span class="sxs-lookup"><span data-stu-id="504d5-189">This is usually the default.</span></span>
12. <span data-ttu-id="504d5-190">Installez l'agent linux Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="504d5-190">Install the Azure Linux Agent by running the following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="504d5-191">Ne créez pas d'espace swap sur le disque du système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="504d5-191">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="504d5-192">L'agent Linux Azure peut configurer automatiquement un espace swap à l'aide du disque local de ressources connecté à la machine virtuelle après déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-192">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="504d5-193">Notez que le disque de ressources local est un disque *temporaire* et qu'il peut être vidé lors de l'annulation de l'approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="504d5-193">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="504d5-194">Après avoir installé l’agent Linux Azure (voir l’étape précédente), modifiez les paramètres suivants dans le fichier /etc/waagent.conf :</span><span class="sxs-lookup"><span data-stu-id="504d5-194">After installing the Azure Linux Agent (see the previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
14. <span data-ttu-id="504d5-195">Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :</span><span class="sxs-lookup"><span data-stu-id="504d5-195">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="504d5-196">Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="504d5-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="504d5-197">Votre disque dur virtuel Linux est alors prêt pour le téléchargement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-197">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="504d5-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="504d5-198">Next steps</span></span>
<span data-ttu-id="504d5-199">Vous êtes maintenant prêt à utiliser votre disque dur virtuel Oracle Linux .vhd pour créer des machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="504d5-199">You're now ready to use your Oracle Linux .vhd to create new virtual machines in Azure.</span></span> <span data-ttu-id="504d5-200">S’il s’agit de la première fois que vous chargez le fichier .vhd sur Azure, consultez les étapes 2 et 3 dans [Création et chargement d’un disque dur virtuel contenant le système d’exploitation Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="504d5-200">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

