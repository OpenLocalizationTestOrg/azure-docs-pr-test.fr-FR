---
title: "Création et téléchargement d’un disque dur virtuel Red Hat Enterprise Linux pour une utilisation dans Azure | Microsoft Docs"
description: "Apprenez à créer et à télécharger un disque dur virtuel (VHD) Azure contenant un système d'exploitation Red Hat Linux."
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
ms.openlocfilehash: b753c76b8c3d789c681d7fbff6aa07590b860be5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="f2138-103">Préparation d'une machine virtuelle Red Hat pour Azure</span><span class="sxs-lookup"><span data-stu-id="f2138-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="f2138-104">Dans cet article, vous allez apprendre à préparer une machine virtuelle Red Hat Enterprise Linux (RHEL) à utiliser dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="f2138-105">Cet article couvre les versions de RHEL 6.7 et 7.1+.</span><span class="sxs-lookup"><span data-stu-id="f2138-105">The versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="f2138-106">Les hyperviseurs de préparation abordés dans cet article sont Hyper-V, KVM (Machine virtuelle basée sur le noyau) et VMware.</span><span class="sxs-lookup"><span data-stu-id="f2138-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="f2138-107">Pour plus d’informations sur les conditions d’éligibilité pour participer au programme d’accès au Cloud de Red Hat, consultez le [site Web d’accès au cloud de Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) et [Exécution RHEL sous Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="f2138-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="f2138-108">Préparer une machine virtuelle Red Hat à partir du Gestionnaire Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f2138-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f2138-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f2138-109">Prerequisites</span></span>
<span data-ttu-id="f2138-110">Cette section suppose que vous avez déjà obtenu un fichier ISO depuis le site web Red Hat et installé l’image RHEL sur un disque dur virtuel (VHD).</span><span class="sxs-lookup"><span data-stu-id="f2138-110">This section assumes that you have already obtained an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span></span> <span data-ttu-id="f2138-111">Pour plus d’informations sur l’utilisation du Gestionnaire Hyper-V pour installer une image de système d’exploitation, voir [Installer le rôle Hyper-V et configurer une machine virtuelle](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2138-111">For more details about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="f2138-112">**Notes d'installation de RHEL**</span><span class="sxs-lookup"><span data-stu-id="f2138-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="f2138-113">Azure ne prend pas en charge le format VHDX.</span><span class="sxs-lookup"><span data-stu-id="f2138-113">Azure does not support the VHDX format.</span></span> <span data-ttu-id="f2138-114">Azure prend uniquement en charge les VHD fixes.</span><span class="sxs-lookup"><span data-stu-id="f2138-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="f2138-115">Vous pouvez utiliser Hyper-V Manager pour convertir le disque au format VHD, ou l’applet de commande Convert-VHD.</span><span class="sxs-lookup"><span data-stu-id="f2138-115">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span></span> <span data-ttu-id="f2138-116">Si vous utilisez VirtualBox, sélectionnez **Taille fixe** par opposition à l’option de valeur par défaut allouée dynamiquement lorsque vous créez le disque.</span><span class="sxs-lookup"><span data-stu-id="f2138-116">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span></span>
* <span data-ttu-id="f2138-117">Azure ne prend en charge que les machines virtuelles de la génération 1.</span><span class="sxs-lookup"><span data-stu-id="f2138-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="f2138-118">Vous pouvez convertir une machine virtuelle de génération 1 du format VHDX au format VHD et d'une taille à expansion dynamique en taille fixe.</span><span class="sxs-lookup"><span data-stu-id="f2138-118">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span></span> <span data-ttu-id="f2138-119">Vous ne pouvez pas modifier la génération d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="f2138-120">Pour plus d’informations, consultez [Dois-je créer une machine virtuelle de génération 1 ou 2 dans Hyper-V ?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="f2138-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="f2138-121">La taille maximale autorisée pour le disque dur virtuel s’élève à 1 023 Go.</span><span class="sxs-lookup"><span data-stu-id="f2138-121">The maximum size that's allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="f2138-122">Lorsque vous installez le système d’exploitation Linux, nous vous recommandons d’utiliser les partitions standard plutôt que le Gestionnaire de volumes logiques (LVM), qui constitue souvent le choix par défaut pour de nombreuses installations.</span><span class="sxs-lookup"><span data-stu-id="f2138-122">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span></span> <span data-ttu-id="f2138-123">Cette pratique permettra d’éviter les conflits de noms avec des machines virtuelles clonées, notamment si un disque de système d’exploitation doit être relié à une autre machine virtuelle identique à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="f2138-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="f2138-124">La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données.</span><span class="sxs-lookup"><span data-stu-id="f2138-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="f2138-125">La prise en charge du noyau pour le montage de systèmes de fichiers UDF (Universal Disk Format) est requise.</span><span class="sxs-lookup"><span data-stu-id="f2138-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="f2138-126">Au premier démarrage sur Azure, le support au format UDF relié à l’invité transmet la configuration d’approvisionnement à la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="f2138-126">At first boot on Azure, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span></span> <span data-ttu-id="f2138-127">L’agent Linux Azure doit être en mesure de monter le système de fichiers UDF pour lire sa configuration et approvisionner la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-127">The Azure Linux Agent must be able to mount the UDF file system to read its configuration and provision the virtual machine.</span></span>
* <span data-ttu-id="f2138-128">Les versions du noyau Linux antérieures à 2.6.37 ne gèrent pas les accès mémoire non uniformes (NUMA) sur Hyper-V avec des machines virtuelles de grande taille.</span><span class="sxs-lookup"><span data-stu-id="f2138-128">Versions of the Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="f2138-129">Ce problème concerne principalement les distributions antérieures utilisant le noyau Red Hat 2.6.32 en amont et a été corrigé dans la version RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="f2138-129">This issue primarily impacts older distributions that use the upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="f2138-130">Pour les systèmes exécutant des noyaux personnalisés dont la version est antérieure à la version 2.6.37 ou des noyaux basés sur RHEL antérieurs à la version 2.6.32-504, le paramètre de démarrage `numa=off` doit être défini sur la ligne de commande du noyau dans grub.conf.</span><span class="sxs-lookup"><span data-stu-id="f2138-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set the `numa=off` boot parameter on the kernel command line in grub.conf.</span></span> <span data-ttu-id="f2138-131">Pour plus d’informations, consultez l’article [KB 436883](https://access.redhat.com/solutions/436883) sur Red Hat.</span><span class="sxs-lookup"><span data-stu-id="f2138-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="f2138-132">Ne configurez pas de partition swap sur le système d’exploitation ou le disque.</span><span class="sxs-lookup"><span data-stu-id="f2138-132">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="f2138-133">L'agent Linux est configurable pour créer un fichier d'échange sur le disque de ressources temporaire.</span><span class="sxs-lookup"><span data-stu-id="f2138-133">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="f2138-134">Les étapes suivantes fournissent plus d'informations à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="f2138-134">More information about this can be found in the following steps.</span></span>
* <span data-ttu-id="f2138-135">La taille de tout disque dur virtuel doit être un multiple de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="f2138-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="f2138-136">Préparer une machine virtuelle RHEL 6 à partir du Gestionnaire Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f2138-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="f2138-137">Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-137">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="f2138-138">Cliquez sur **Connecter** pour ouvrir une fenêtre de console de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-138">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="f2138-139">Dans RHEL 6, NetworkManager peut interférer avec l’agent Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-139">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="f2138-140">Exécutez la commande suivante pour désinstaller le package :</span><span class="sxs-lookup"><span data-stu-id="f2138-140">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="f2138-141">Créez ou modifiez le fichier `/etc/sysconfig/network`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-141">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="f2138-142">Créez ou modifiez le fichier `/etc/sysconfig/network-scripts/ifcfg-eth0`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-142">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="f2138-143">Déplacez (ou supprimez) les règles udev afin d’éviter la génération de règles statiques pour l’interface Ethernet.</span><span class="sxs-lookup"><span data-stu-id="f2138-143">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="f2138-144">Ces règles entraînent des problèmes lorsque vous clonez une machine virtuelle dans Microsoft Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="f2138-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="f2138-145">Assurez-vous que le service réseau commencera aux heures de démarrage en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-145">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="f2138-146">Inscrivez votre abonnement Red Hat pour installer des packages à partir du référentiel RHEL en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-146">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="f2138-147">Le package WALinuxAgent, `WALinuxAgent-<version>`, a fait l’objet d’une transmission de type push vers le référentiel Red Hat « extras ».</span><span class="sxs-lookup"><span data-stu-id="f2138-147">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="f2138-148">Activez le référentiel extras en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-148">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="f2138-149">Modifiez la ligne de démarrage du noyau dans votre configuration grub pour y inclure les paramètres de noyau supplémentaires pour Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-149">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="f2138-150">Pour effectuer cette modification, ouvrez `/boot/grub/menu.lst` dans un éditeur de texte et vérifiez que le noyau par défaut comprend les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="f2138-150">To do this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="f2138-151">Ce permet également d’assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour la prise en charge d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-151">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="f2138-152">Outre les précautions ci-dessus, nous recommandons de supprimer les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="f2138-152">In addition, we recommended that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="f2138-153">Le démarrage graphique et transparent n'est pas utile dans un environnement cloud où nous voulons que tous les journaux soient envoyés au port série.</span><span class="sxs-lookup"><span data-stu-id="f2138-153">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="f2138-154">Vous pouvez laisser l’option `crashkernel` configurée le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="f2138-154">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="f2138-155">Notez que ce paramètre réduit la quantité de mémoire disponible dans la machine virtuelle de 128 Mo ou plus.</span><span class="sxs-lookup"><span data-stu-id="f2138-155">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more.</span></span> <span data-ttu-id="f2138-156">Cette configuration peut être problématique sur les machines virtuelles de petite taille.</span><span class="sxs-lookup"><span data-stu-id="f2138-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="f2138-157">RHEL 6.5 et versions antérieures doivent également définir le paramètre de noyau `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="f2138-157">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="f2138-158">Consultez Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="f2138-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="f2138-159">Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu. Il s’agit généralement du réglage par défaut.</span><span class="sxs-lookup"><span data-stu-id="f2138-159">Ensure that the secure shell (SSH) server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="f2138-160">Modifiez /etc/ssh/sshd_config pour inclure la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-160">Modify /etc/ssh/sshd_config to include the following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="f2138-161">Installez l'agent linux Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-161">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="f2138-162">l'installation du package WALinuxAgent entraîne la suppression des packages NetworkManager et NetworkManager-gnome, s'ils n'avaient pas déjà été supprimés à l'étape 3.</span><span class="sxs-lookup"><span data-stu-id="f2138-162">Installing the WALinuxAgent package removes the NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="f2138-163">Ne créez pas d’espace d’échange sur le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f2138-163">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="f2138-164">L’agent Linux Azure peut configurer automatiquement un espace d’échange à l’aide du disque de ressources local attaché à la machine virtuelle après l’approvisionnement de cette dernière sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-164">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="f2138-165">Notez que le disque de ressources local est un disque temporaire et qu’il peut être vidé lors de l’annulation de l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-165">Note that the local resource disk is a temporary disk and that it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="f2138-166">Une fois que vous avez installé l’agent Linux Azure lors de l’étape précédente, modifiez les paramètres suivants dans le fichier /etc/waagent.conf :</span><span class="sxs-lookup"><span data-stu-id="f2138-166">After you install the Azure Linux Agent in the previous step, modify the following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

14. <span data-ttu-id="f2138-167">Annulez l'inscription de l'abonnement (le cas échéant) en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-167">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="f2138-168">Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :</span><span class="sxs-lookup"><span data-stu-id="f2138-168">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="f2138-169">Cliquez sur **Action** > **Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f2138-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="f2138-170">Votre disque dur virtuel Linux est alors prêt pour le téléchargement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-170">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="f2138-171">Préparer une machine virtuelle RHEL 7 à partir du Gestionnaire Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f2138-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="f2138-172">Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-172">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="f2138-173">Cliquez sur **Connecter** pour ouvrir une fenêtre de console de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-173">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="f2138-174">Créez ou modifiez le fichier `/etc/sysconfig/network`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-174">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="f2138-175">Créez ou modifiez le fichier `/etc/sysconfig/network-scripts/ifcfg-eth0`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-175">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="f2138-176">Assurez-vous que le service réseau commencera aux heures de démarrage en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-176">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="f2138-177">Inscrivez votre abonnement Red Hat pour installer des packages à partir du référentiel RHEL en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-177">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="f2138-178">Modifiez la ligne de démarrage du noyau dans votre configuration grub pour y inclure les paramètres de noyau supplémentaires pour Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-178">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="f2138-179">Pour effectuer cette modification, ouvrez le fichier `/etc/default/grub` dans un éditeur de texte et modifiez le paramètre `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="f2138-179">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="f2138-180">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f2138-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="f2138-181">Ce permet également d’assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour la prise en charge d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-181">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="f2138-182">Cette configuration désactive également les nouvelles conventions d’affectation de noms RHEL 7 pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="f2138-182">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="f2138-183">De plus, nous vous recommandons de supprimer les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="f2138-183">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="f2138-184">Le démarrage graphique et transparent n'est pas utile dans un environnement cloud où nous voulons que tous les journaux soient envoyés au port série.</span><span class="sxs-lookup"><span data-stu-id="f2138-184">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="f2138-185">Vous pouvez laisser l’option `crashkernel` configurée le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="f2138-185">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="f2138-186">Notez que ce paramètre réduit la quantité de mémoire disponible dans la machine virtuelle de 128 Mo ou plus, ce qui peut être problématique sur les machines virtuelles de petite taille.</span><span class="sxs-lookup"><span data-stu-id="f2138-186">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="f2138-187">Une fois que vous avez fini de modifier `/etc/default/grub`, exécutez la commande suivante pour régénérer la configuration grub :</span><span class="sxs-lookup"><span data-stu-id="f2138-187">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="f2138-188">Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu, ce qui est généralement le réglage par défaut.</span><span class="sxs-lookup"><span data-stu-id="f2138-188">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="f2138-189">Modifiez `/etc/ssh/sshd_config` pour y inclure la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-189">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="f2138-190">Le package WALinuxAgent, `WALinuxAgent-<version>`, a fait l’objet d’une transmission de type push vers le référentiel Red Hat « extras ».</span><span class="sxs-lookup"><span data-stu-id="f2138-190">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="f2138-191">Activez le référentiel extras en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-191">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="f2138-192">Installez l'agent linux Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-192">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="f2138-193">Ne créez pas d’espace d’échange sur le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f2138-193">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="f2138-194">L’agent Linux Azure peut configurer automatiquement un espace d’échange à l’aide du disque de ressources local attaché à la machine virtuelle après l’approvisionnement de cette dernière sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-194">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="f2138-195">Notez que le disque de ressources local est un disque temporaire et qu’il peut être vidé lors de l’annulation de l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-195">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="f2138-196">Après avoir installé l’agent Linux Azure lors de l’étape précédente, modifiez en conséquence les paramètres suivants dans le fichier `/etc/waagent.conf` :</span><span class="sxs-lookup"><span data-stu-id="f2138-196">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="f2138-197">Si vous souhaitez annuler l'inscription de l'abonnement, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-197">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="f2138-198">Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :</span><span class="sxs-lookup"><span data-stu-id="f2138-198">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="f2138-199">Cliquez sur **Action** > **Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f2138-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="f2138-200">Votre disque dur virtuel Linux est alors prêt pour le téléchargement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-200">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="f2138-201">Préparer une machine virtuelle Red Hat à partir de KVM</span><span class="sxs-lookup"><span data-stu-id="f2138-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="f2138-202">Préparer une machine virtuelle RHEL 6 à partir de KMV</span><span class="sxs-lookup"><span data-stu-id="f2138-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="f2138-203">Téléchargez l'image KVM de RHEL 6 depuis le site web Red Hat.</span><span class="sxs-lookup"><span data-stu-id="f2138-203">Download the KVM image of RHEL 6 from the Red Hat website.</span></span>

2. <span data-ttu-id="f2138-204">Définissez un mot de passe racine.</span><span class="sxs-lookup"><span data-stu-id="f2138-204">Set a root password.</span></span>

    <span data-ttu-id="f2138-205">Générez un mot de passe chiffré et copiez la sortie de la commande :</span><span class="sxs-lookup"><span data-stu-id="f2138-205">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="f2138-206">Définissez un mot de passe racine avec guestfish :</span><span class="sxs-lookup"><span data-stu-id="f2138-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="f2138-207">Modifiez le second champ de l’utilisateur racine en remplaçant « !! »</span><span class="sxs-lookup"><span data-stu-id="f2138-207">Change the second field of the root user from "!!"</span></span> <span data-ttu-id="f2138-208">» par le mot de passe chiffré.</span><span class="sxs-lookup"><span data-stu-id="f2138-208">to the encrypted password.</span></span>

3. <span data-ttu-id="f2138-209">Créez une machine virtuelle dans KVM à partir de l’image qcow2.</span><span class="sxs-lookup"><span data-stu-id="f2138-209">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="f2138-210">Définissez le type de disque sur **qcow2**, puis définissez le modèle d’appareil de l’interface réseau virtuelle sur **virtio**.</span><span class="sxs-lookup"><span data-stu-id="f2138-210">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="f2138-211">Démarrez ensuite la machine virtuelle, puis connectez-vous en tant que racine.</span><span class="sxs-lookup"><span data-stu-id="f2138-211">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="f2138-212">Créez ou modifiez le fichier `/etc/sysconfig/network`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-212">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="f2138-213">Créez ou modifiez le fichier `/etc/sysconfig/network-scripts/ifcfg-eth0`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-213">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="f2138-214">Déplacez (ou supprimez) les règles udev afin d’éviter la génération de règles statiques pour l’interface Ethernet.</span><span class="sxs-lookup"><span data-stu-id="f2138-214">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="f2138-215">Ces règles entraînent des problèmes lorsque vous clonez une machine virtuelle dans Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="f2138-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="f2138-216">Assurez-vous que le service réseau commencera aux heures de démarrage en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-216">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="f2138-217">Inscrivez votre abonnement Red Hat pour installer des packages à partir du référentiel RHEL en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-217">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="f2138-218">Modifiez la ligne de démarrage du noyau dans votre configuration grub pour y inclure les paramètres de noyau supplémentaires pour Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-218">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="f2138-219">Pour effectuer cette configuration, ouvrez `/boot/grub/menu.lst` dans un éditeur de texte et vérifiez que le noyau par défaut comprend les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="f2138-219">To do this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="f2138-220">Ce permet également d’assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour la prise en charge d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-220">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="f2138-221">De plus, nous vous recommandons de supprimer les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="f2138-221">In addition, we recommend that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="f2138-222">Le démarrage graphique et transparent n'est pas utile dans un environnement cloud où nous voulons que tous les journaux soient envoyés au port série.</span><span class="sxs-lookup"><span data-stu-id="f2138-222">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="f2138-223">Vous pouvez laisser l’option `crashkernel` configurée le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="f2138-223">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="f2138-224">Notez que ce paramètre réduit la quantité de mémoire disponible dans la machine virtuelle de 128 Mo ou plus, ce qui peut être problématique sur les machines virtuelles de petite taille.</span><span class="sxs-lookup"><span data-stu-id="f2138-224">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="f2138-225">RHEL 6.5 et versions antérieures doivent également définir le paramètre de noyau `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="f2138-225">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="f2138-226">Consultez Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="f2138-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="f2138-227">Ajoutez des modules de Hyper-V dans initramfs :</span><span class="sxs-lookup"><span data-stu-id="f2138-227">Add Hyper-V modules to initramfs:</span></span>  

    <span data-ttu-id="f2138-228">Modifiez `/etc/dracut.conf` et ajoutez le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-228">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="f2138-229">Régénérez initramfs :</span><span class="sxs-lookup"><span data-stu-id="f2138-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="f2138-230">Désinstallez Cloud-Init :</span><span class="sxs-lookup"><span data-stu-id="f2138-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="f2138-231">Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu :</span><span class="sxs-lookup"><span data-stu-id="f2138-231">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="f2138-232">Modifiez /etc/ssh/sshd_config pour y inclure les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2138-232">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="f2138-233">Le package WALinuxAgent, `WALinuxAgent-<version>`, a fait l’objet d’une transmission de type push vers le référentiel Red Hat « extras ».</span><span class="sxs-lookup"><span data-stu-id="f2138-233">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="f2138-234">Activez le référentiel extras en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-234">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="f2138-235">Installez l'agent linux Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-235">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="f2138-236">L’agent Linux Azure peut configurer automatiquement un espace d’échange à l’aide du disque de ressources local attaché à la machine virtuelle après l’approvisionnement de cette dernière sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-236">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="f2138-237">Notez que le disque de ressources local est un disque temporaire et qu’il peut être vidé lors de l’annulation de l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-237">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="f2138-238">Une fois que vous avez installé l’agent Linux Azure lors de l’étape précédente, modifiez les paramètres suivants dans le fichier **/etc/waagent.conf** :</span><span class="sxs-lookup"><span data-stu-id="f2138-238">After you install the Azure Linux Agent in the previous step, modify the following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="f2138-239">Annulez l'inscription de l'abonnement (le cas échéant) en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-239">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="f2138-240">Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :</span><span class="sxs-lookup"><span data-stu-id="f2138-240">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="f2138-241">Arrêtez la machine virtuelle dans KVM.</span><span class="sxs-lookup"><span data-stu-id="f2138-241">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="f2138-242">Convertissez l’image qcow2 au format VHD.</span><span class="sxs-lookup"><span data-stu-id="f2138-242">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="f2138-243">Convertissez tout d'abord l'image au format RAW :</span><span class="sxs-lookup"><span data-stu-id="f2138-243">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="f2138-244">Assurez-vous que la taille de l’image RAW est alignée sur 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="f2138-244">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="f2138-245">Dans le cas contraire, arrondissez la taille pour l’aligner sur 1 Mo :</span><span class="sxs-lookup"><span data-stu-id="f2138-245">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="f2138-246">Convertissez le disque brut en VHD à taille fixe :</span><span class="sxs-lookup"><span data-stu-id="f2138-246">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="f2138-247">Préparer une machine virtuelle RHEL 7 à partir de KMV</span><span class="sxs-lookup"><span data-stu-id="f2138-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="f2138-248">Téléchargez l'image KVM de RHEL 7 depuis le site web Red Hat.</span><span class="sxs-lookup"><span data-stu-id="f2138-248">Download the KVM image of RHEL 7 from the Red Hat website.</span></span> <span data-ttu-id="f2138-249">Cette procédure utilise RHEL 7 comme exemple.</span><span class="sxs-lookup"><span data-stu-id="f2138-249">This procedure uses RHEL 7 as the example.</span></span>

2. <span data-ttu-id="f2138-250">Définissez un mot de passe racine.</span><span class="sxs-lookup"><span data-stu-id="f2138-250">Set a root password.</span></span>

    <span data-ttu-id="f2138-251">Générez un mot de passe chiffré et copiez la sortie de la commande :</span><span class="sxs-lookup"><span data-stu-id="f2138-251">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="f2138-252">Définissez un mot de passe racine avec guestfish :</span><span class="sxs-lookup"><span data-stu-id="f2138-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="f2138-253">Modifiez le second champ de l'utilisateur racine en remplaçant « !! »</span><span class="sxs-lookup"><span data-stu-id="f2138-253">Change the second field of root user from "!!"</span></span> <span data-ttu-id="f2138-254">» par le mot de passe chiffré.</span><span class="sxs-lookup"><span data-stu-id="f2138-254">to the encrypted password.</span></span>

3. <span data-ttu-id="f2138-255">Créez une machine virtuelle dans KVM à partir de l’image qcow2.</span><span class="sxs-lookup"><span data-stu-id="f2138-255">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="f2138-256">Définissez le type de disque sur **qcow2**, puis définissez le modèle d’appareil de l’interface réseau virtuelle sur **virtio**.</span><span class="sxs-lookup"><span data-stu-id="f2138-256">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="f2138-257">Démarrez ensuite la machine virtuelle, puis connectez-vous en tant que racine.</span><span class="sxs-lookup"><span data-stu-id="f2138-257">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="f2138-258">Créez ou modifiez le fichier `/etc/sysconfig/network`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-258">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="f2138-259">Créez ou modifiez le fichier `/etc/sysconfig/network-scripts/ifcfg-eth0`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-259">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="f2138-260">Assurez-vous que le service réseau commencera aux heures de démarrage en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-260">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="f2138-261">Inscrivez votre abonnement Red Hat pour installer des packages à partir du référentiel RHEL en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-261">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="f2138-262">Modifiez la ligne de démarrage du noyau dans votre configuration grub pour y inclure les paramètres de noyau supplémentaires pour Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-262">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="f2138-263">Pour effectuer cette configuration, ouvrez le fichier `/etc/default/grub` dans un éditeur de texte et modifiez le paramètre `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="f2138-263">To do this configuration, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="f2138-264">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f2138-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="f2138-265">Cette commande permet également d’assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour la prise en charge d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-265">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="f2138-266">Cette commande désactive également les nouvelles conventions d’affectation de noms RHEL 7 pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="f2138-266">The command also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="f2138-267">De plus, nous vous recommandons de supprimer les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="f2138-267">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="f2138-268">Le démarrage graphique et transparent n'est pas utile dans un environnement cloud où nous voulons que tous les journaux soient envoyés au port série.</span><span class="sxs-lookup"><span data-stu-id="f2138-268">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="f2138-269">Vous pouvez laisser l’option `crashkernel` configurée le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="f2138-269">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="f2138-270">Notez que ce paramètre réduit la quantité de mémoire disponible dans la machine virtuelle de 128 Mo ou plus, ce qui peut être problématique sur les machines virtuelles de petite taille.</span><span class="sxs-lookup"><span data-stu-id="f2138-270">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="f2138-271">Une fois que vous avez fini de modifier `/etc/default/grub`, exécutez la commande suivante pour régénérer la configuration grub :</span><span class="sxs-lookup"><span data-stu-id="f2138-271">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="f2138-272">Ajoutez des modules de Hyper-V dans initramfs.</span><span class="sxs-lookup"><span data-stu-id="f2138-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="f2138-273">Modifiez `/etc/dracut.conf` en y ajoutant le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="f2138-274">Régénérez initramfs :</span><span class="sxs-lookup"><span data-stu-id="f2138-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="f2138-275">Désinstallez Cloud-Init :</span><span class="sxs-lookup"><span data-stu-id="f2138-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="f2138-276">Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu :</span><span class="sxs-lookup"><span data-stu-id="f2138-276">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="f2138-277">Modifiez /etc/ssh/sshd_config pour y inclure les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2138-277">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="f2138-278">Le package WALinuxAgent, `WALinuxAgent-<version>`, a fait l’objet d’une transmission de type push vers le référentiel Red Hat « extras ».</span><span class="sxs-lookup"><span data-stu-id="f2138-278">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="f2138-279">Activez le référentiel extras en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-279">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="f2138-280">Installez l'agent linux Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-280">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="f2138-281">Activez le service waagent :</span><span class="sxs-lookup"><span data-stu-id="f2138-281">Enable the waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="f2138-282">Ne créez pas d’espace d’échange sur le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f2138-282">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="f2138-283">L’agent Linux Azure peut configurer automatiquement un espace d’échange à l’aide du disque de ressources local attaché à la machine virtuelle après l’approvisionnement de cette dernière sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-283">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="f2138-284">Notez que le disque de ressources local est un disque temporaire et qu’il peut être vidé lors de l’annulation de l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-284">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="f2138-285">Après avoir installé l’agent Linux Azure lors de l’étape précédente, modifiez en conséquence les paramètres suivants dans le fichier `/etc/waagent.conf` :</span><span class="sxs-lookup"><span data-stu-id="f2138-285">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="f2138-286">Annulez l'inscription de l'abonnement (le cas échéant) en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-286">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="f2138-287">Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :</span><span class="sxs-lookup"><span data-stu-id="f2138-287">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="f2138-288">Arrêtez la machine virtuelle dans KVM.</span><span class="sxs-lookup"><span data-stu-id="f2138-288">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="f2138-289">Convertissez l’image qcow2 au format VHD.</span><span class="sxs-lookup"><span data-stu-id="f2138-289">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="f2138-290">Convertissez tout d'abord l'image au format RAW :</span><span class="sxs-lookup"><span data-stu-id="f2138-290">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="f2138-291">Assurez-vous que la taille de l’image RAW est alignée sur 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="f2138-291">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="f2138-292">Dans le cas contraire, arrondissez la taille pour l’aligner sur 1 Mo :</span><span class="sxs-lookup"><span data-stu-id="f2138-292">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="f2138-293">Convertissez le disque brut en VHD à taille fixe :</span><span class="sxs-lookup"><span data-stu-id="f2138-293">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="f2138-294">Préparer une machine virtuelle Red Hat à partir de VMware</span><span class="sxs-lookup"><span data-stu-id="f2138-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="f2138-295">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f2138-295">Prerequisites</span></span>
<span data-ttu-id="f2138-296">Cette section suppose que vous avez déjà installé une machine virtuelle RHEL dans VMWare.</span><span class="sxs-lookup"><span data-stu-id="f2138-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="f2138-297">Pour plus d’informations sur l’installation d’un système d’exploitation dans VMWare, voir le document [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html)(Guide d’installation de système d’exploitation invité VMWare).</span><span class="sxs-lookup"><span data-stu-id="f2138-297">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="f2138-298">Lorsque vous installez le système d’exploitation Linux, nous vous recommandons d’utiliser les partitions standard plutôt que LVM, ce qui constitue souvent le choix par défaut pour de nombreuses installations.</span><span class="sxs-lookup"><span data-stu-id="f2138-298">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span></span> <span data-ttu-id="f2138-299">Cela permettra d’éviter les conflits de noms avec des machines virtuelles clonées, notamment si un disque de système d’exploitation doit être relié à une autre machine virtuelle à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="f2138-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span></span> <span data-ttu-id="f2138-300">Vous pouvez utiliser les techniques LVM ou RAID sur les disques de données si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="f2138-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="f2138-301">Ne configurez pas de partition swap sur le système d’exploitation ou le disque.</span><span class="sxs-lookup"><span data-stu-id="f2138-301">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="f2138-302">Vous pouvez configurer l’agent Linux pour la création d’un fichier d’échange sur le disque de ressources temporaire.</span><span class="sxs-lookup"><span data-stu-id="f2138-302">You can configure the Linux agent to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="f2138-303">Les étapes qui suivent fournissent plus d’informations à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="f2138-303">You can find more information about this in the steps that follow.</span></span>
* <span data-ttu-id="f2138-304">Lorsque vous créez le disque dur virtuel, sélectionnez **Stocker le disque virtuel en un seul fichier**.</span><span class="sxs-lookup"><span data-stu-id="f2138-304">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="f2138-305">Préparer une machine virtuelle RHEL 6 à partir de VMWare</span><span class="sxs-lookup"><span data-stu-id="f2138-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="f2138-306">Dans RHEL 6, NetworkManager peut interférer avec l’agent Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-306">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="f2138-307">Exécutez la commande suivante pour désinstaller le package :</span><span class="sxs-lookup"><span data-stu-id="f2138-307">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="f2138-308">Créez un fichier nommé **network** dans le répertoire /etc/sysconfig/ contenant le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-308">Create a file named **network** in the /etc/sysconfig/ directory that contains the following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="f2138-309">Créez ou modifiez le fichier `/etc/sysconfig/network-scripts/ifcfg-eth0`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-309">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="f2138-310">Déplacez (ou supprimez) les règles udev afin d’éviter la génération de règles statiques pour l’interface Ethernet.</span><span class="sxs-lookup"><span data-stu-id="f2138-310">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="f2138-311">Ces règles entraînent des problèmes lorsque vous clonez une machine virtuelle dans Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="f2138-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="f2138-312">Assurez-vous que le service réseau commencera aux heures de démarrage en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-312">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="f2138-313">Inscrivez votre abonnement Red Hat pour installer des packages à partir du référentiel RHEL en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-313">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="f2138-314">Le package WALinuxAgent, `WALinuxAgent-<version>`, a fait l’objet d’une transmission de type push vers le référentiel Red Hat « extras ».</span><span class="sxs-lookup"><span data-stu-id="f2138-314">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="f2138-315">Activez le référentiel extras en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-315">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="f2138-316">Modifiez la ligne de démarrage du noyau dans votre configuration grub pour y inclure les paramètres de noyau supplémentaires pour Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-316">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="f2138-317">Pour cela, ouvrez le fichier `/etc/default/grub` dans un éditeur de texte et modifiez le paramètre `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="f2138-317">To do this, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="f2138-318">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f2138-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="f2138-319">Ce permet également d’assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour la prise en charge d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-319">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="f2138-320">De plus, nous vous recommandons de supprimer les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="f2138-320">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="f2138-321">Le démarrage graphique et transparent n'est pas utile dans un environnement cloud où nous voulons que tous les journaux soient envoyés au port série.</span><span class="sxs-lookup"><span data-stu-id="f2138-321">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="f2138-322">Vous pouvez laisser l’option `crashkernel` configurée le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="f2138-322">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="f2138-323">Notez que ce paramètre réduit la quantité de mémoire disponible dans la machine virtuelle de 128 Mo ou plus, ce qui peut être problématique sur les machines virtuelles de petite taille.</span><span class="sxs-lookup"><span data-stu-id="f2138-323">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="f2138-324">Ajoutez des modules de Hyper-V dans initramfs :</span><span class="sxs-lookup"><span data-stu-id="f2138-324">Add Hyper-V modules to initramfs:</span></span>

    <span data-ttu-id="f2138-325">Modifiez `/etc/dracut.conf` et ajoutez le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-325">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="f2138-326">Régénérez initramfs :</span><span class="sxs-lookup"><span data-stu-id="f2138-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="f2138-327">Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu, ce qui est généralement le réglage par défaut.</span><span class="sxs-lookup"><span data-stu-id="f2138-327">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="f2138-328">Modifiez `/etc/ssh/sshd_config` pour y inclure la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-328">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

    <span data-ttu-id="f2138-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="f2138-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="f2138-330">Installez l'agent linux Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-330">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="f2138-331">Ne créez pas d’espace d’échange sur le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f2138-331">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="f2138-332">L’agent Linux Azure peut configurer automatiquement un espace d’échange à l’aide du disque de ressources local attaché à la machine virtuelle après l’approvisionnement de cette dernière sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-332">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="f2138-333">Notez que le disque de ressources local est un disque temporaire et qu’il peut être vidé lors de l’annulation de l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-333">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="f2138-334">Après avoir installé l’agent Linux Azure lors de l’étape précédente, modifiez en conséquence les paramètres suivants dans le fichier `/etc/waagent.conf` :</span><span class="sxs-lookup"><span data-stu-id="f2138-334">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="f2138-335">Annulez l'inscription de l'abonnement (le cas échéant) en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-335">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="f2138-336">Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :</span><span class="sxs-lookup"><span data-stu-id="f2138-336">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="f2138-337">Arrêtez la machine virtuelle, puis convertissez le fichier VMDK en fichier .vhd.</span><span class="sxs-lookup"><span data-stu-id="f2138-337">Shut down the virtual machine, and convert the VMDK file to a .vhd file.</span></span>

    <span data-ttu-id="f2138-338">Convertissez tout d'abord l'image au format RAW :</span><span class="sxs-lookup"><span data-stu-id="f2138-338">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="f2138-339">Assurez-vous que la taille de l’image RAW est alignée sur 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="f2138-339">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="f2138-340">Dans le cas contraire, arrondissez la taille pour l’aligner sur 1 Mo :</span><span class="sxs-lookup"><span data-stu-id="f2138-340">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="f2138-341">Convertissez le disque brut en VHD à taille fixe :</span><span class="sxs-lookup"><span data-stu-id="f2138-341">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="f2138-342">Préparer une machine virtuelle RHEL 7 à partir de VMWare</span><span class="sxs-lookup"><span data-stu-id="f2138-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="f2138-343">Créez ou modifiez le fichier `/etc/sysconfig/network`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-343">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="f2138-344">Créez ou modifiez le fichier `/etc/sysconfig/network-scripts/ifcfg-eth0`, puis ajoutez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-344">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="f2138-345">Assurez-vous que le service réseau commencera aux heures de démarrage en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-345">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="f2138-346">Inscrivez votre abonnement Red Hat pour installer des packages à partir du référentiel RHEL en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-346">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="f2138-347">Modifiez la ligne de démarrage du noyau dans votre configuration grub pour y inclure les paramètres de noyau supplémentaires pour Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-347">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="f2138-348">Pour effectuer cette modification, ouvrez le fichier `/etc/default/grub` dans un éditeur de texte et modifiez le paramètre `GRUB_CMDLINE_LINUX`.</span><span class="sxs-lookup"><span data-stu-id="f2138-348">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="f2138-349">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f2138-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="f2138-350">Cette configuration permet également d’assurer que tous les messages de la console sont envoyés vers le premier port série, ce qui peut simplifier les problèmes de débogage pour la prise en charge d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-350">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="f2138-351">Cela désactive également les nouvelles conventions d’affectation de noms RHEL 7 pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="f2138-351">It also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="f2138-352">De plus, nous vous recommandons de supprimer les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="f2138-352">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="f2138-353">Le démarrage graphique et transparent n'est pas utile dans un environnement cloud où nous voulons que tous les journaux soient envoyés au port série.</span><span class="sxs-lookup"><span data-stu-id="f2138-353">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="f2138-354">Vous pouvez laisser l’option `crashkernel` configurée le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="f2138-354">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="f2138-355">Notez que ce paramètre réduit la quantité de mémoire disponible dans la machine virtuelle de 128 Mo ou plus, ce qui peut être problématique sur les machines virtuelles de petite taille.</span><span class="sxs-lookup"><span data-stu-id="f2138-355">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="f2138-356">Une fois que vous avez fini de modifier `/etc/default/grub`, exécutez la commande suivante pour régénérer la configuration grub :</span><span class="sxs-lookup"><span data-stu-id="f2138-356">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="f2138-357">Ajoutez des modules de Hyper-V dans initramfs.</span><span class="sxs-lookup"><span data-stu-id="f2138-357">Add Hyper-V modules to initramfs.</span></span>

    <span data-ttu-id="f2138-358">Modifiez `/etc/dracut.conf`, ajoutez le contenu :</span><span class="sxs-lookup"><span data-stu-id="f2138-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="f2138-359">Régénérez initramfs :</span><span class="sxs-lookup"><span data-stu-id="f2138-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="f2138-360">Vérifiez que le serveur SSH est installé et configuré pour démarrer au moment prévu.</span><span class="sxs-lookup"><span data-stu-id="f2138-360">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="f2138-361">Ce paramètre est généralement la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="f2138-361">This setting is usually the default.</span></span> <span data-ttu-id="f2138-362">Modifiez `/etc/ssh/sshd_config` pour y inclure la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-362">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="f2138-363">Le package WALinuxAgent, `WALinuxAgent-<version>`, a fait l’objet d’une transmission de type push vers le référentiel Red Hat « extras ».</span><span class="sxs-lookup"><span data-stu-id="f2138-363">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="f2138-364">Activez le référentiel extras en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-364">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="f2138-365">Installez l'agent linux Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-365">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="f2138-366">Ne créez pas d’espace d’échange sur le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f2138-366">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="f2138-367">L’agent Linux Azure peut configurer automatiquement un espace d’échange à l’aide du disque de ressources local attaché à la machine virtuelle après l’approvisionnement de cette dernière sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-367">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="f2138-368">Notez que le disque de ressources local est un disque temporaire et qu’il peut être vidé lors de l’annulation de l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-368">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="f2138-369">Après avoir installé l’agent Linux Azure lors de l’étape précédente, modifiez en conséquence les paramètres suivants dans le fichier `/etc/waagent.conf` :</span><span class="sxs-lookup"><span data-stu-id="f2138-369">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

12. <span data-ttu-id="f2138-370">Si vous souhaitez annuler l'inscription de l'abonnement, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f2138-370">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="f2138-371">Exécutez les commandes suivantes pour annuler le déploiement de la machine virtuelle et préparer son déploiement sur Azure :</span><span class="sxs-lookup"><span data-stu-id="f2138-371">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="f2138-372">Arrêtez l’ordinateur virtuel et convertir le fichier VMDK au format VHD.</span><span class="sxs-lookup"><span data-stu-id="f2138-372">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span></span>

    <span data-ttu-id="f2138-373">Convertissez tout d'abord l'image au format RAW :</span><span class="sxs-lookup"><span data-stu-id="f2138-373">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="f2138-374">Assurez-vous que la taille de l’image RAW est alignée sur 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="f2138-374">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="f2138-375">Dans le cas contraire, arrondissez la taille pour l’aligner sur 1 Mo :</span><span class="sxs-lookup"><span data-stu-id="f2138-375">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="f2138-376">Convertissez le disque brut en VHD à taille fixe :</span><span class="sxs-lookup"><span data-stu-id="f2138-376">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="f2138-377">Préparer une machine virtuelle Red Hat à partir d’un fichier ISO grâce à l’utilisation automatique d’un fichier Kickstart</span><span class="sxs-lookup"><span data-stu-id="f2138-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="f2138-378">Préparer une machine virtuelle RHEL 7 à partir d'un fichier Kickstart</span><span class="sxs-lookup"><span data-stu-id="f2138-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="f2138-379">Créez un fichier qui inclut le contenu suivant et enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="f2138-379">Create a kickstart file that includes the following content, and save the file.</span></span> <span data-ttu-id="f2138-380">Pour plus d’informations sur l’installation de Kickstart, voir le document [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html)(Guide d’installation Kickstart).</span><span class="sxs-lookup"><span data-stu-id="f2138-380">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run the Setup Agent on first boot
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

        # Clear the MBR
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

        # Power down the machine after install
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

        # Disable the root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set the cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build the grub cfg
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

2. <span data-ttu-id="f2138-381">Placez le fichier Kickstart à un emplacement auquel système d’installation peut accéder.</span><span class="sxs-lookup"><span data-stu-id="f2138-381">Place the kickstart file where the installation system can access it.</span></span>

3. <span data-ttu-id="f2138-382">Dans le Gestionnaire Hyper-V, créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="f2138-383">Sur la page **Connecter un disque dur virtuel**, sélectionnez **Attacher un disque dur virtuel ultérieurement**, puis exécutez l’Assistant Nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-383">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="f2138-384">Ouvrez les paramètres de la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="f2138-384">Open the virtual machine settings:</span></span>

    <span data-ttu-id="f2138-385">a.</span><span class="sxs-lookup"><span data-stu-id="f2138-385">a.</span></span>  <span data-ttu-id="f2138-386">Attachez un nouveau disque dur virtuel à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-386">Attach a new virtual hard disk to the virtual machine.</span></span> <span data-ttu-id="f2138-387">Veillez à sélectionner **Format VHD** et **Taille fixe**.</span><span class="sxs-lookup"><span data-stu-id="f2138-387">Make sure to select **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="f2138-388">b.</span><span class="sxs-lookup"><span data-stu-id="f2138-388">b.</span></span>  <span data-ttu-id="f2138-389">Attachez l’ISO d’installation au lecteur de DVD.</span><span class="sxs-lookup"><span data-stu-id="f2138-389">Attach the installation ISO to the DVD drive.</span></span>

    <span data-ttu-id="f2138-390">c.</span><span class="sxs-lookup"><span data-stu-id="f2138-390">c.</span></span>  <span data-ttu-id="f2138-391">Configurez le BIOS de manière à exécuter le démarrage à partir d’un CD.</span><span class="sxs-lookup"><span data-stu-id="f2138-391">Set the BIOS to boot from CD.</span></span>

5. <span data-ttu-id="f2138-392">Démarrez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2138-392">Start the virtual machine.</span></span> <span data-ttu-id="f2138-393">Lorsque le guide d’installation s’affiche, appuyez sur la touche **Tab** pour configurer les options de démarrage.</span><span class="sxs-lookup"><span data-stu-id="f2138-393">When the installation guide appears, press **Tab** to configure the boot options.</span></span>

6. <span data-ttu-id="f2138-394">Entrez `inst.ks=<the location of the kickstart file>` à la fin des options de démarrage, puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="f2138-394">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="f2138-395">Attendez que l'installation se termine.</span><span class="sxs-lookup"><span data-stu-id="f2138-395">Wait for the installation to finish.</span></span> <span data-ttu-id="f2138-396">À la fin de l’installation, la machine virtuelle s’arrête automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f2138-396">When it's finished, the virtual machine will be shut down automatically.</span></span> <span data-ttu-id="f2138-397">Votre disque dur virtuel Linux est alors prêt pour le téléchargement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-397">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="f2138-398">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="f2138-398">Known issues</span></span>
### <a name="the-hyper-v-driver-could-not-be-included-in-the-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="f2138-399">Impossible d’inclure le pilote Hyper-V dans le disque virtuel initial lors de l’utilisation d’un hyperviseur non-Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f2138-399">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="f2138-400">Dans certains cas, les programmes d’installation de Linux n’incluent pas les pilotes pour Hyper-V dans le disque virtuel initial (initrd ou initramfs), sauf si Linux détecte que ce dernier s’exécute dans un environnement Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f2138-400">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="f2138-401">Lorsque vous utilisez un système de virtualisation différent (c’est-à-dire Virtualbox, Xen, etc.) pour préparer votre image Linux, vous pouvez avoir besoin de recréer initrd pour vous assurer que les modules noyau hv_vmbus et hv_storvsc figurent au moins parmi les modules disponibles sur le disque virtuel initial.</span><span class="sxs-lookup"><span data-stu-id="f2138-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span></span> <span data-ttu-id="f2138-402">Ceci est un problème connu, touchant au moins les systèmes basés sur la distribution Red Hat en amont.</span><span class="sxs-lookup"><span data-stu-id="f2138-402">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="f2138-403">Pour résoudre ce problème, ajoutez des modules Hyper-V dans initramfs, puis régénérez ce dernier :</span><span class="sxs-lookup"><span data-stu-id="f2138-403">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span></span>

<span data-ttu-id="f2138-404">Modifiez `/etc/dracut.conf` et ajoutez le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="f2138-404">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="f2138-405">Régénérez initramfs :</span><span class="sxs-lookup"><span data-stu-id="f2138-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="f2138-406">Pour plus d’informations, voir l’article concernant la [régénération d’initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="f2138-406">For more details, see the information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2138-407">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2138-407">Next steps</span></span>
<span data-ttu-id="f2138-408">Vous êtes maintenant prêt à utiliser votre disque dur virtuel Red Hat Enterprise Linux pour créer des machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f2138-408">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="f2138-409">S’il s’agit de la première fois que vous chargez le fichier .vhd sur Azure, consultez les étapes 2 et 3 dans [Création et chargement d’un disque dur virtuel contenant le système d’exploitation Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2138-409">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="f2138-410">Pour plus d’informations sur les hyperviseurs certifiés pour l’exécution de Red Hat Enterprise Linux, voir le [site web de Red Hat](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="f2138-410">For more details about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
