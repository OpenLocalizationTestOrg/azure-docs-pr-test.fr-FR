---
title: "aaaCreate et télécharger Red Hat Enterprise Linux disque dur virtuel pour une utilisation dans Azure | Documents Microsoft"
description: "En savoir plus toocreate et téléchargez un Azure disque dur virtuel (VHD) qui contient un système d’exploitation Red Hat Linux."
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
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="40ccf-103">Préparation d'une machine virtuelle Red Hat pour Azure</span><span class="sxs-lookup"><span data-stu-id="40ccf-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="40ccf-104">Dans cet article, vous allez apprendre comment tooprepare un ordinateur virtuel de Red Hat Enterprise Linux (RHEL) pour une utilisation dans Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="40ccf-105">les versions de Hello de RHEL qui sont abordées dans cet article sont 6.7 + et 7.1.</span><span class="sxs-lookup"><span data-stu-id="40ccf-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="40ccf-106">les hyperviseurs Hello de préparation qui sont abordées dans cet article sont virtuels Hyper-V, basée sur le noyau (KVM) et VMware.</span><span class="sxs-lookup"><span data-stu-id="40ccf-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="40ccf-107">Pour plus d’informations sur les conditions d’éligibilité pour participer au programme d’accès au Cloud de Red Hat, consultez le [site Web d’accès au cloud de Red Hat](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) et [Exécution RHEL sous Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="40ccf-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="40ccf-108">Préparer une machine virtuelle Red Hat à partir du Gestionnaire Hyper-V</span><span class="sxs-lookup"><span data-stu-id="40ccf-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="40ccf-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="40ccf-109">Prerequisites</span></span>
<span data-ttu-id="40ccf-110">Cette section part du principe que vous avez déjà obtenu un fichier ISO à partir du site Web de Red Hat hello et installé hello RHEL image tooa disque dur virtuel (VHD).</span><span class="sxs-lookup"><span data-stu-id="40ccf-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="40ccf-111">Pour plus d’informations sur la façon toouse Gestionnaire Hyper-V tooinstall une image de système d’exploitation, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="40ccf-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="40ccf-112">**Notes d'installation de RHEL**</span><span class="sxs-lookup"><span data-stu-id="40ccf-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="40ccf-113">Azure ne prend pas en charge le format VHDX hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="40ccf-114">Azure prend uniquement en charge les VHD fixes.</span><span class="sxs-lookup"><span data-stu-id="40ccf-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="40ccf-115">Vous pouvez utiliser le Gestionnaire Hyper-V tooconvert hello disque tooVHD format, ou vous pouvez utiliser les applets de commande convert-vhd hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="40ccf-116">Si vous utilisez VirtualBox, sélectionnez **une taille fixe** par opposition toohello par défaut alloué dynamiquement option lorsque vous créez le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="40ccf-117">Azure ne prend en charge que les machines virtuelles de la génération 1.</span><span class="sxs-lookup"><span data-stu-id="40ccf-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="40ccf-118">Vous pouvez convertir un ordinateur virtuel de génération 1 à partir du format de fichier de disque dur virtuel VHDX toohello et à partir du disque de taille fixe tooa de taille dynamique.</span><span class="sxs-lookup"><span data-stu-id="40ccf-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="40ccf-119">Vous ne pouvez pas modifier la génération d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="40ccf-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="40ccf-120">Pour plus d’informations, consultez [Dois-je créer une machine virtuelle de génération 1 ou 2 dans Hyper-V ?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="40ccf-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="40ccf-121">taille maximale Hello est autorisée pour hello disque dur virtuel est de 1 023 go.</span><span class="sxs-lookup"><span data-stu-id="40ccf-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="40ccf-122">Lorsque vous installez le système d’exploitation de Linux hello, nous vous recommandons d’utiliser les partitions standards plutôt que le Gestionnaire de Volume logique (LVM), qui est souvent hello par défaut pour le nombre d’installations.</span><span class="sxs-lookup"><span data-stu-id="40ccf-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="40ccf-123">Cette pratique permet d’éviter les conflits de nom Gestionnaire de volume logique avec les ordinateurs virtuels clonés, en particulier si vous avez besoin de tooattach un système d’exploitation disque tooanother ordinateur virtuel pour le dépannage.</span><span class="sxs-lookup"><span data-stu-id="40ccf-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="40ccf-124">La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données.</span><span class="sxs-lookup"><span data-stu-id="40ccf-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="40ccf-125">La prise en charge du noyau pour le montage de systèmes de fichiers UDF (Universal Disk Format) est requise.</span><span class="sxs-lookup"><span data-stu-id="40ccf-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="40ccf-126">Au premier démarrage sur Azure, hello au format UDF support qui est attaché toohello invité passe hello configuration configuration toohello machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="40ccf-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="40ccf-127">Hello Linux Agent Azure doit être en mesure de toomount hello UDF fichier système tooread sa configuration et configurer l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="40ccf-128">Versions du noyau de Linux hello qui sont antérieures à 2.6.37 ne gèrent pas l’accès mémoire non uniforme (NUMA) sur Hyper-V avec des tailles de machine virtuelle plus importantes.</span><span class="sxs-lookup"><span data-stu-id="40ccf-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="40ccf-129">Ce problème principalement les impacts anciennes distributions qui utilisent hello en amont noyau de Red Hat 2.6.32 et a été corrigé dans RHEL 6.6 (noyau-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="40ccf-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="40ccf-130">Les systèmes qui exécutent des noyaux personnalisés qui sont antérieurs à 2.6.37 ou les noyaux RHEL qui sont antérieurs à 2.6.32-504 doivent définir hello `numa=off` paramètre de démarrage sur la ligne de commande de noyau hello dans grub.conf.</span><span class="sxs-lookup"><span data-stu-id="40ccf-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="40ccf-131">Pour plus d’informations, consultez l’article [KB 436883](https://access.redhat.com/solutions/436883) sur Red Hat.</span><span class="sxs-lookup"><span data-stu-id="40ccf-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="40ccf-132">Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="40ccf-133">Hello Linux Agent peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="40ccf-134">Vous trouverez plus d’informations à ce sujet Bonjour comme suit.</span><span class="sxs-lookup"><span data-stu-id="40ccf-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="40ccf-135">La taille de tout disque dur virtuel doit être un multiple de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="40ccf-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="40ccf-136">Préparer une machine virtuelle RHEL 6 à partir du Gestionnaire Hyper-V</span><span class="sxs-lookup"><span data-stu-id="40ccf-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="40ccf-137">Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="40ccf-138">Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="40ccf-139">RHEL 6, NetworkManager peut interférer avec l’agent de hello Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="40ccf-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="40ccf-140">Désinstaller ce package en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="40ccf-141">Créer ou modifier hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="40ccf-142">Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="40ccf-143">Déplacer (ou supprimer) hello udev règles tooavoid génération de règles statiques pour l’interface de Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="40ccf-144">Ces règles entraînent des problèmes lorsque vous clonez une machine virtuelle dans Microsoft Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="40ccf-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="40ccf-145">Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="40ccf-146">Inscrire votre installation de hello Red Hat abonnement tooenable des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="40ccf-147">package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="40ccf-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="40ccf-148">Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="40ccf-149">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="40ccf-150">toodo cette modification, ouvre `/boot/grub/menu.lst` dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="40ccf-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="40ccf-151">Cela permet également de garantir que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="40ccf-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="40ccf-152">En outre, nous recommandons de supprimer hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="40ccf-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="40ccf-153">Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.</span><span class="sxs-lookup"><span data-stu-id="40ccf-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="40ccf-154">Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="40ccf-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="40ccf-155">Notez que ce paramètre réduit hello de mémoire disponible dans l’ordinateur virtuel hello 128 Mo ou plus.</span><span class="sxs-lookup"><span data-stu-id="40ccf-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="40ccf-156">Cette configuration peut être problématique sur les machines virtuelles de petite taille.</span><span class="sxs-lookup"><span data-stu-id="40ccf-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="40ccf-157">RHEL 6.5 et versions antérieur doive également définir hello `numa=off` paramètre de noyau.</span><span class="sxs-lookup"><span data-stu-id="40ccf-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="40ccf-158">Consultez Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="40ccf-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="40ccf-159">Vérifiez le serveur hello SSH (secure shell) est installé et configuré toostart au moment du démarrage, qui est généralement hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="40ccf-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="40ccf-160">Modifiez hello de tooinclude /etc/ssh/sshd_config ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="40ccf-161">Installez hello Linux Agent Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="40ccf-162">Package de WALinuxAgent hello lors de l’installation supprime hello NetworkManager et packages de NetworkManager-gnome si elles n’étaient pas déjà supprimées à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="40ccf-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="40ccf-163">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="40ccf-164">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="40ccf-165">Notez que hello local disque de ressources est un disque temporaire et qu’il doit être vidé lors de la machine virtuelle de hello est annulé.</span><span class="sxs-lookup"><span data-stu-id="40ccf-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="40ccf-166">Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifiez hello suivant correctement les paramètres dans /etc/waagent.conf :</span><span class="sxs-lookup"><span data-stu-id="40ccf-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="40ccf-167">Annuler l’inscription d’abonnement de hello (si nécessaire) en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="40ccf-168">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="40ccf-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="40ccf-169">Cliquez sur **Action** > **Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="40ccf-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="40ccf-170">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="40ccf-171">Préparer une machine virtuelle RHEL 7 à partir du Gestionnaire Hyper-V</span><span class="sxs-lookup"><span data-stu-id="40ccf-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="40ccf-172">Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="40ccf-173">Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="40ccf-174">Créer ou modifier hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="40ccf-175">Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="40ccf-176">Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="40ccf-177">Inscrire votre installation de hello Red Hat abonnement tooenable des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="40ccf-178">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="40ccf-179">toodo cette modification, ouvre `/etc/default/grub` dans un éditeur de texte et l’édition hello `GRUB_CMDLINE_LINUX` paramètre.</span><span class="sxs-lookup"><span data-stu-id="40ccf-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="40ccf-180">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="40ccf-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="40ccf-181">Cela permet également de garantir que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="40ccf-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="40ccf-182">Cette configuration désactive également des conventions d’affectation de noms hello nouvelle RHEL 7 pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="40ccf-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="40ccf-183">En outre, nous vous recommandons de supprimer hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="40ccf-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="40ccf-184">Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.</span><span class="sxs-lookup"><span data-stu-id="40ccf-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="40ccf-185">Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="40ccf-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="40ccf-186">Notez que ce paramètre réduit hello de mémoire disponible dans la machine virtuelle de hello de 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites.</span><span class="sxs-lookup"><span data-stu-id="40ccf-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="40ccf-187">Après avoir effectué édition `/etc/default/grub`, exécutez hello après la commande toorebuild hello grub configuration :</span><span class="sxs-lookup"><span data-stu-id="40ccf-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="40ccf-188">Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage, qui est généralement hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="40ccf-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="40ccf-189">Modifier `/etc/ssh/sshd_config` hello tooinclude ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="40ccf-190">package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="40ccf-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="40ccf-191">Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="40ccf-192">Installez hello Linux Agent Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="40ccf-193">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="40ccf-194">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="40ccf-195">Notez que hello disque de ressources locales est un disque temporaire, et il doit être vidé lorsque l’ordinateur virtuel hello est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="40ccf-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="40ccf-196">Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :</span><span class="sxs-lookup"><span data-stu-id="40ccf-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="40ccf-197">Si vous souhaitez abonnement de hello toounregister, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="40ccf-198">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="40ccf-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="40ccf-199">Cliquez sur **Action** > **Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="40ccf-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="40ccf-200">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="40ccf-201">Préparer une machine virtuelle Red Hat à partir de KVM</span><span class="sxs-lookup"><span data-stu-id="40ccf-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="40ccf-202">Préparer une machine virtuelle RHEL 6 à partir de KMV</span><span class="sxs-lookup"><span data-stu-id="40ccf-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="40ccf-203">Télécharger l’image KVM hello RHEL 6 à partir du site Web de Red Hat hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="40ccf-204">Définissez un mot de passe racine.</span><span class="sxs-lookup"><span data-stu-id="40ccf-204">Set a root password.</span></span>

    <span data-ttu-id="40ccf-205">Générer un mot de passe chiffré et copier le résultat de hello de commande hello :</span><span class="sxs-lookup"><span data-stu-id="40ccf-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="40ccf-206">Définissez un mot de passe racine avec guestfish :</span><span class="sxs-lookup"><span data-stu-id="40ccf-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="40ccf-207">Modification hello deuxième champ de l’utilisateur racine hello « ! »</span><span class="sxs-lookup"><span data-stu-id="40ccf-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="40ccf-208">toohello le mot de passe chiffré.</span><span class="sxs-lookup"><span data-stu-id="40ccf-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="40ccf-209">Créer une machine virtuelle dans KVM à partir de l’image de qcow2 hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="40ccf-210">Définir le type de disque hello trop**qcow2**et définir le modèle d’appareil hello réseau virtuel interface trop**virtio**.</span><span class="sxs-lookup"><span data-stu-id="40ccf-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="40ccf-211">Ensuite, démarrer l’ordinateur virtuel de hello et connectez-vous en tant que racine.</span><span class="sxs-lookup"><span data-stu-id="40ccf-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="40ccf-212">Créer ou modifier hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="40ccf-213">Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="40ccf-214">Déplacer (ou supprimer) hello udev règles tooavoid génération de règles statiques pour l’interface de Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="40ccf-215">Ces règles entraînent des problèmes lorsque vous clonez une machine virtuelle dans Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="40ccf-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="40ccf-216">Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="40ccf-217">Inscrire votre installation de hello Red Hat abonnement tooenable des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="40ccf-218">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="40ccf-219">toodo cette configuration, ouvre `/boot/grub/menu.lst` dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="40ccf-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="40ccf-220">Cela permet également de garantir que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="40ccf-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="40ccf-221">En outre, nous vous recommandons de supprimer hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="40ccf-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="40ccf-222">Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.</span><span class="sxs-lookup"><span data-stu-id="40ccf-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="40ccf-223">Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="40ccf-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="40ccf-224">Notez que ce paramètre réduit hello de mémoire disponible dans la machine virtuelle de hello de 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites.</span><span class="sxs-lookup"><span data-stu-id="40ccf-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="40ccf-225">RHEL 6.5 et versions antérieur doive également définir hello `numa=off` paramètre de noyau.</span><span class="sxs-lookup"><span data-stu-id="40ccf-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="40ccf-226">Consultez Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="40ccf-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="40ccf-227">Ajoutez tooinitramfs de modules Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="40ccf-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="40ccf-228">Modifier `/etc/dracut.conf`et ajoutez hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="40ccf-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="40ccf-229">Régénérez initramfs :</span><span class="sxs-lookup"><span data-stu-id="40ccf-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="40ccf-230">Désinstallez Cloud-Init :</span><span class="sxs-lookup"><span data-stu-id="40ccf-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="40ccf-231">Vérifiez que ce serveur SSH hello est installé et configuré toostart au moment du démarrage :</span><span class="sxs-lookup"><span data-stu-id="40ccf-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="40ccf-232">Modifiez hello de tooinclude /etc/ssh/sshd_config lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="40ccf-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="40ccf-233">package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="40ccf-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="40ccf-234">Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="40ccf-235">Installez hello Linux Agent Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="40ccf-236">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="40ccf-237">Notez que hello disque de ressources locales est un disque temporaire, et il doit être vidé lorsque l’ordinateur virtuel hello est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="40ccf-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="40ccf-238">Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifier hello suivant les paramètres dans **/etc/waagent.conf** correctement :</span><span class="sxs-lookup"><span data-stu-id="40ccf-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="40ccf-239">Annuler l’inscription d’abonnement de hello (si nécessaire) en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="40ccf-240">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="40ccf-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="40ccf-241">Arrêter la machine virtuelle hello KVM.</span><span class="sxs-lookup"><span data-stu-id="40ccf-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="40ccf-242">Convertir le format VHD toohello hello qcow2 image.</span><span class="sxs-lookup"><span data-stu-id="40ccf-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="40ccf-243">Tout d’abord convertir le format de tooraw d’image hello :</span><span class="sxs-lookup"><span data-stu-id="40ccf-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="40ccf-244">Assurez-vous que la taille hello d’image brute de hello est aligné avec 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="40ccf-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="40ccf-245">Sinon, arrondir tooalign de taille hello avec 1 Mo :</span><span class="sxs-lookup"><span data-stu-id="40ccf-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="40ccf-246">Convertir hello disque raw tooa disque dur virtuel de taille fixe :</span><span class="sxs-lookup"><span data-stu-id="40ccf-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="40ccf-247">Préparer une machine virtuelle RHEL 7 à partir de KMV</span><span class="sxs-lookup"><span data-stu-id="40ccf-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="40ccf-248">Télécharger l’image KVM hello de RHEL 7 à partir du site Web de Red Hat hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="40ccf-249">Cette procédure utilise RHEL 7 comme exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="40ccf-250">Définissez un mot de passe racine.</span><span class="sxs-lookup"><span data-stu-id="40ccf-250">Set a root password.</span></span>

    <span data-ttu-id="40ccf-251">Générer un mot de passe chiffré et copier le résultat de hello de commande hello :</span><span class="sxs-lookup"><span data-stu-id="40ccf-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="40ccf-252">Définissez un mot de passe racine avec guestfish :</span><span class="sxs-lookup"><span data-stu-id="40ccf-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="40ccf-253">Modification hello deuxième champ de l’utilisateur racine à partir de « ! »</span><span class="sxs-lookup"><span data-stu-id="40ccf-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="40ccf-254">toohello le mot de passe chiffré.</span><span class="sxs-lookup"><span data-stu-id="40ccf-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="40ccf-255">Créer une machine virtuelle dans KVM à partir de l’image de qcow2 hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="40ccf-256">Définir le type de disque hello trop**qcow2**et définir le modèle d’appareil hello réseau virtuel interface trop**virtio**.</span><span class="sxs-lookup"><span data-stu-id="40ccf-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="40ccf-257">Ensuite, démarrer l’ordinateur virtuel de hello et connectez-vous en tant que racine.</span><span class="sxs-lookup"><span data-stu-id="40ccf-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="40ccf-258">Créer ou modifier hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="40ccf-259">Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="40ccf-260">Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="40ccf-261">Inscrire votre installation de tooenable abonnement Red Hat des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="40ccf-262">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="40ccf-263">toodo cette configuration, ouvre `/etc/default/grub` dans un éditeur de texte et l’édition hello `GRUB_CMDLINE_LINUX` paramètre.</span><span class="sxs-lookup"><span data-stu-id="40ccf-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="40ccf-264">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="40ccf-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="40ccf-265">Cette commande garantit également que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="40ccf-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="40ccf-266">commande Hello désactive également des conventions d’affectation de noms hello nouvelle RHEL 7 pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="40ccf-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="40ccf-267">En outre, nous vous recommandons de supprimer hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="40ccf-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="40ccf-268">Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.</span><span class="sxs-lookup"><span data-stu-id="40ccf-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="40ccf-269">Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="40ccf-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="40ccf-270">Notez que ce paramètre réduit hello de mémoire disponible dans la machine virtuelle de hello de 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites.</span><span class="sxs-lookup"><span data-stu-id="40ccf-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="40ccf-271">Après avoir effectué édition `/etc/default/grub`, exécutez hello après la commande toorebuild hello grub configuration :</span><span class="sxs-lookup"><span data-stu-id="40ccf-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="40ccf-272">Ajoutez des modules de Hyper-V dans initramfs.</span><span class="sxs-lookup"><span data-stu-id="40ccf-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="40ccf-273">Modifiez `/etc/dracut.conf` en y ajoutant le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="40ccf-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="40ccf-274">Régénérez initramfs :</span><span class="sxs-lookup"><span data-stu-id="40ccf-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="40ccf-275">Désinstallez Cloud-Init :</span><span class="sxs-lookup"><span data-stu-id="40ccf-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="40ccf-276">Vérifiez que ce serveur SSH hello est installé et configuré toostart au moment du démarrage :</span><span class="sxs-lookup"><span data-stu-id="40ccf-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="40ccf-277">Modifiez hello de tooinclude /etc/ssh/sshd_config lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="40ccf-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="40ccf-278">package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="40ccf-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="40ccf-279">Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="40ccf-280">Installez hello Linux Agent Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="40ccf-281">Activer le service de waagent hello :</span><span class="sxs-lookup"><span data-stu-id="40ccf-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="40ccf-282">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="40ccf-283">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="40ccf-284">Notez que hello disque de ressources locales est un disque temporaire, et il doit être vidé lorsque l’ordinateur virtuel hello est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="40ccf-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="40ccf-285">Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :</span><span class="sxs-lookup"><span data-stu-id="40ccf-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="40ccf-286">Annuler l’inscription d’abonnement de hello (si nécessaire) en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="40ccf-287">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="40ccf-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="40ccf-288">Arrêter la machine virtuelle hello KVM.</span><span class="sxs-lookup"><span data-stu-id="40ccf-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="40ccf-289">Convertir le format VHD toohello hello qcow2 image.</span><span class="sxs-lookup"><span data-stu-id="40ccf-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="40ccf-290">Tout d’abord convertir le format de tooraw d’image hello :</span><span class="sxs-lookup"><span data-stu-id="40ccf-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="40ccf-291">Assurez-vous que la taille hello d’image brute de hello est aligné avec 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="40ccf-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="40ccf-292">Sinon, arrondir tooalign de taille hello avec 1 Mo :</span><span class="sxs-lookup"><span data-stu-id="40ccf-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="40ccf-293">Convertir hello disque raw tooa disque dur virtuel de taille fixe :</span><span class="sxs-lookup"><span data-stu-id="40ccf-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="40ccf-294">Préparer une machine virtuelle Red Hat à partir de VMware</span><span class="sxs-lookup"><span data-stu-id="40ccf-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="40ccf-295">Composants requis</span><span class="sxs-lookup"><span data-stu-id="40ccf-295">Prerequisites</span></span>
<span data-ttu-id="40ccf-296">Cette section suppose que vous avez déjà installé une machine virtuelle RHEL dans VMWare.</span><span class="sxs-lookup"><span data-stu-id="40ccf-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="40ccf-297">Pour plus d’informations sur la façon dont tooinstall un système d’exploitation dans les environnements VMware, consultez [Guide d’Installation système d’exploitation invité VMware](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="40ccf-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="40ccf-298">Lorsque vous installez le système d’exploitation de Linux hello, nous vous recommandons d’utiliser les partitions standards au lieu du Gestionnaire de volume logique, qui est souvent hello par défaut pour le nombre d’installations.</span><span class="sxs-lookup"><span data-stu-id="40ccf-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="40ccf-299">Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec les ordinateurs virtuels clonés, en particulier si un disque de système d’exploitation a besoin de machine virtuelle de tooanother toobe attaché pour le dépannage.</span><span class="sxs-lookup"><span data-stu-id="40ccf-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="40ccf-300">Vous pouvez utiliser les techniques LVM ou RAID sur les disques de données si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="40ccf-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="40ccf-301">Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="40ccf-302">Vous pouvez configurer hello Linux agent toocreate un fichier d’échange sur le disque de ressources temporaires hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="40ccf-303">Vous trouverez plus d’informations à ce sujet dans les étapes de hello qui suivent.</span><span class="sxs-lookup"><span data-stu-id="40ccf-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="40ccf-304">Lorsque vous créez un disque dur virtuel hello, sélectionnez **disque virtuel de magasin en tant qu’un seul fichier**.</span><span class="sxs-lookup"><span data-stu-id="40ccf-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="40ccf-305">Préparer une machine virtuelle RHEL 6 à partir de VMWare</span><span class="sxs-lookup"><span data-stu-id="40ccf-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="40ccf-306">RHEL 6, NetworkManager peut interférer avec l’agent de hello Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="40ccf-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="40ccf-307">Désinstaller ce package en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="40ccf-308">Créez un fichier nommé **réseau** hello etc/sysconfig/répertoire contenant hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="40ccf-309">Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="40ccf-310">Déplacer (ou supprimer) hello udev règles tooavoid génération de règles statiques pour l’interface de Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="40ccf-311">Ces règles entraînent des problèmes lorsque vous clonez une machine virtuelle dans Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="40ccf-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="40ccf-312">Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="40ccf-313">Inscrire votre installation de hello Red Hat abonnement tooenable des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="40ccf-314">package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="40ccf-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="40ccf-315">Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="40ccf-316">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="40ccf-317">toodo, ouvrez `/etc/default/grub` dans un éditeur de texte et l’édition hello `GRUB_CMDLINE_LINUX` paramètre.</span><span class="sxs-lookup"><span data-stu-id="40ccf-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="40ccf-318">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="40ccf-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="40ccf-319">Cela permet également de garantir que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="40ccf-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="40ccf-320">En outre, nous vous recommandons de supprimer hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="40ccf-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="40ccf-321">Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.</span><span class="sxs-lookup"><span data-stu-id="40ccf-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="40ccf-322">Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="40ccf-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="40ccf-323">Notez que ce paramètre réduit hello de mémoire disponible dans la machine virtuelle de hello de 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites.</span><span class="sxs-lookup"><span data-stu-id="40ccf-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="40ccf-324">Ajoutez tooinitramfs de modules Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="40ccf-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="40ccf-325">Modifier `/etc/dracut.conf`et ajoutez hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="40ccf-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="40ccf-326">Régénérez initramfs :</span><span class="sxs-lookup"><span data-stu-id="40ccf-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="40ccf-327">Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage, qui est généralement hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="40ccf-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="40ccf-328">Modifier `/etc/ssh/sshd_config` hello tooinclude ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="40ccf-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="40ccf-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="40ccf-330">Installez hello Linux Agent Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="40ccf-331">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="40ccf-332">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="40ccf-333">Notez que hello disque de ressources locales est un disque temporaire, et il doit être vidé lorsque l’ordinateur virtuel hello est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="40ccf-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="40ccf-334">Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :</span><span class="sxs-lookup"><span data-stu-id="40ccf-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="40ccf-335">Annuler l’inscription d’abonnement de hello (si nécessaire) en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="40ccf-336">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="40ccf-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="40ccf-337">Arrêt de la machine virtuelle de hello et convertir le fichier .vhd tooa hello VMDK fichier.</span><span class="sxs-lookup"><span data-stu-id="40ccf-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="40ccf-338">Tout d’abord convertir le format de tooraw d’image hello :</span><span class="sxs-lookup"><span data-stu-id="40ccf-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="40ccf-339">Assurez-vous que la taille hello d’image brute de hello est aligné avec 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="40ccf-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="40ccf-340">Sinon, arrondir tooalign de taille hello avec 1 Mo :</span><span class="sxs-lookup"><span data-stu-id="40ccf-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="40ccf-341">Convertir hello disque raw tooa disque dur virtuel de taille fixe :</span><span class="sxs-lookup"><span data-stu-id="40ccf-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="40ccf-342">Préparer une machine virtuelle RHEL 7 à partir de VMWare</span><span class="sxs-lookup"><span data-stu-id="40ccf-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="40ccf-343">Créer ou modifier hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="40ccf-344">Créer ou modifier hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="40ccf-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="40ccf-345">Démarrera service de réseau hello au moment du démarrage en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="40ccf-346">Inscrire votre installation de hello Red Hat abonnement tooenable des packages à partir du référentiel RHEL hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="40ccf-347">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="40ccf-348">toodo cette modification, ouvre `/etc/default/grub` dans un éditeur de texte et l’édition hello `GRUB_CMDLINE_LINUX` paramètre.</span><span class="sxs-lookup"><span data-stu-id="40ccf-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="40ccf-349">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="40ccf-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="40ccf-350">Cette configuration garantit également que tous les messages de la console sont envoyées toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="40ccf-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="40ccf-351">Il désactive également de nouvelles conventions de nommage RHEL 7 hello pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="40ccf-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="40ccf-352">En outre, nous vous recommandons de supprimer hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="40ccf-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="40ccf-353">Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.</span><span class="sxs-lookup"><span data-stu-id="40ccf-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="40ccf-354">Vous pouvez laisser hello `crashkernel` option configurée Si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="40ccf-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="40ccf-355">Notez que ce paramètre réduit hello de mémoire disponible dans la machine virtuelle de hello de 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites.</span><span class="sxs-lookup"><span data-stu-id="40ccf-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="40ccf-356">Après avoir effectué édition `/etc/default/grub`, exécutez hello après la commande toorebuild hello grub configuration :</span><span class="sxs-lookup"><span data-stu-id="40ccf-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="40ccf-357">Ajoutez tooinitramfs de modules Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="40ccf-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="40ccf-358">Modifiez `/etc/dracut.conf`, ajoutez le contenu :</span><span class="sxs-lookup"><span data-stu-id="40ccf-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="40ccf-359">Régénérez initramfs :</span><span class="sxs-lookup"><span data-stu-id="40ccf-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="40ccf-360">Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="40ccf-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="40ccf-361">Ce paramètre est généralement hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="40ccf-361">This setting is usually hello default.</span></span> <span data-ttu-id="40ccf-362">Modifier `/etc/ssh/sshd_config` hello tooinclude ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="40ccf-363">package de WALinuxAgent Hello, `WALinuxAgent-<version>`, ont été envoyées de référentiel d’extras toohello Red Hat.</span><span class="sxs-lookup"><span data-stu-id="40ccf-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="40ccf-364">Activer le référentiel des fonctionnalités supplémentaires de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="40ccf-365">Installez hello Linux Agent Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="40ccf-366">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="40ccf-367">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello virtual machine après la configuration de machine virtuelle de hello sur Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="40ccf-368">Notez que hello disque de ressources locales est un disque temporaire, et il doit être vidé lorsque l’ordinateur virtuel hello est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="40ccf-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="40ccf-369">Après avoir installé hello Linux Agent Azure à l’étape précédente de hello, modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :</span><span class="sxs-lookup"><span data-stu-id="40ccf-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="40ccf-370">Si vous souhaitez abonnement de hello toounregister, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="40ccf-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="40ccf-371">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="40ccf-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="40ccf-372">Arrêt de la machine virtuelle de hello et convertir le format de disque dur virtuel du fichier toohello hello VMDK.</span><span class="sxs-lookup"><span data-stu-id="40ccf-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="40ccf-373">Tout d’abord convertir le format de tooraw d’image hello :</span><span class="sxs-lookup"><span data-stu-id="40ccf-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="40ccf-374">Assurez-vous que la taille hello d’image brute de hello est aligné avec 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="40ccf-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="40ccf-375">Sinon, arrondir tooalign de taille hello avec 1 Mo :</span><span class="sxs-lookup"><span data-stu-id="40ccf-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="40ccf-376">Convertir hello disque raw tooa disque dur virtuel de taille fixe :</span><span class="sxs-lookup"><span data-stu-id="40ccf-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="40ccf-377">Préparer une machine virtuelle Red Hat à partir d’un fichier ISO grâce à l’utilisation automatique d’un fichier Kickstart</span><span class="sxs-lookup"><span data-stu-id="40ccf-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="40ccf-378">Préparer une machine virtuelle RHEL 7 à partir d'un fichier Kickstart</span><span class="sxs-lookup"><span data-stu-id="40ccf-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="40ccf-379">Créer un fichier qui inclut hello suivant le contenu et enregistrer le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="40ccf-380">Pour plus d’informations sur l’installation de démarrer, consultez hello [Guide d’Installation de démarrer](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="40ccf-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
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

        # Clear hello MBR
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

        # Power down hello machine after install
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

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
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

2. <span data-ttu-id="40ccf-381">Placez le fichier hello où système d’installation hello peut y accéder.</span><span class="sxs-lookup"><span data-stu-id="40ccf-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="40ccf-382">Dans le Gestionnaire Hyper-V, créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="40ccf-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="40ccf-383">Sur hello **connecter un disque dur virtuel** page, sélectionnez **attacher un disque dur virtuel ultérieurement**et terminé hello Assistant Nouvel ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="40ccf-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="40ccf-384">Ouvrez les paramètres d’ordinateur virtuel hello :</span><span class="sxs-lookup"><span data-stu-id="40ccf-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="40ccf-385">a.</span><span class="sxs-lookup"><span data-stu-id="40ccf-385">a.</span></span>  <span data-ttu-id="40ccf-386">Joindre un ordinateur virtuel toohello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="40ccf-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="40ccf-387">Assurez-vous que tooselect **Format VHD** et **taille fixe**.</span><span class="sxs-lookup"><span data-stu-id="40ccf-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="40ccf-388">b.</span><span class="sxs-lookup"><span data-stu-id="40ccf-388">b.</span></span>  <span data-ttu-id="40ccf-389">Attachez l’installation hello lecteur de DVD toohello ISO.</span><span class="sxs-lookup"><span data-stu-id="40ccf-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="40ccf-390">c.</span><span class="sxs-lookup"><span data-stu-id="40ccf-390">c.</span></span>  <span data-ttu-id="40ccf-391">Définissez hello BIOS tooboot à partir du CD.</span><span class="sxs-lookup"><span data-stu-id="40ccf-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="40ccf-392">Démarrer l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-392">Start hello virtual machine.</span></span> <span data-ttu-id="40ccf-393">Guide d’installation Bonjour, appuyez sur **onglet** options de démarrage tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="40ccf-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="40ccf-394">Entrée `inst.ks=<hello location of hello kickstart file>` à fin hello des options de démarrage hello, appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="40ccf-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="40ccf-395">Attendez que hello installation toofinish.</span><span class="sxs-lookup"><span data-stu-id="40ccf-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="40ccf-396">Lorsqu’il est terminé, hello virtual machine s’arrête automatiquement.</span><span class="sxs-lookup"><span data-stu-id="40ccf-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="40ccf-397">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="40ccf-398">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="40ccf-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="40ccf-399">pilote de Hyper-V de Hello n’a pas pu être inclus dans le disque initiale hello lors de l’utilisation d’un hyperviseur Hyper-V</span><span class="sxs-lookup"><span data-stu-id="40ccf-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="40ccf-400">Dans certains cas, les programmes d’installation de Linux inclut ne peut-être pas les pilotes hello pour Hyper-V dans hello RAM disque initiale (initrd ou initramfs) à moins que Linux détecte qu’il s’exécute dans un environnement Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="40ccf-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="40ccf-401">Lorsque vous utilisez un tooprepare système (c'est-à-dire, Virtualbox, Xen, etc.) de virtualisation différent votre image Linux, vous devrez toorebuild initrd tooensure qui a au moins hello hv_vmbus et les modules de noyau hv_storvsc sont disponibles sur le disque virtuel hello initiale.</span><span class="sxs-lookup"><span data-stu-id="40ccf-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="40ccf-402">Il s’agit au moins un problème connu sur les systèmes qui reposent sur la distribution de Red Hat hello en amont.</span><span class="sxs-lookup"><span data-stu-id="40ccf-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="40ccf-403">tooresolve ce problème, ajoutez tooinitramfs de modules Hyper-V et le reconstruire :</span><span class="sxs-lookup"><span data-stu-id="40ccf-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="40ccf-404">Modifier `/etc/dracut.conf`et ajoutez hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="40ccf-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="40ccf-405">Régénérez initramfs :</span><span class="sxs-lookup"><span data-stu-id="40ccf-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="40ccf-406">Pour plus d’informations, consultez les informations de hello sur [reconstruction initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="40ccf-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="40ccf-407">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40ccf-407">Next steps</span></span>
<span data-ttu-id="40ccf-408">Vous êtes maintenant prêt toouse votre Red Hat Enterprise Linux disque dur virtuel toocreate nouvelles machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccf-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="40ccf-409">S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40ccf-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="40ccf-410">Pour plus d’informations sur les hyperviseurs hello qui sont certifiés toorun Red Hat Enterprise Linux, consultez [site Web de Red Hat hello](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="40ccf-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
