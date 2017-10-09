---
title: "aaaCreate et télécharger un VHD Linux CentOS base dans Azure"
description: "En savoir plus toocreate et téléchargez un Azure disque dur virtuel (VHD) qui contient un système d’exploitation Linux basée sur CentOS."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="d691f-103">Préparation d'une machine virtuelle CentOS pour Azure</span><span class="sxs-lookup"><span data-stu-id="d691f-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="d691f-104">Préparation d’une machine virtuelle CentOS 6.x pour Azure</span><span class="sxs-lookup"><span data-stu-id="d691f-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="d691f-105">Préparation d’une machine virtuelle CentOS 7.0+ pour Azure</span><span class="sxs-lookup"><span data-stu-id="d691f-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="d691f-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d691f-106">Prerequisites</span></span>
<span data-ttu-id="d691f-107">Cet article suppose que vous avez déjà installé un CentOS (ou dérivé similaire) Linux système d’exploitation tooa disque virtuel.</span><span class="sxs-lookup"><span data-stu-id="d691f-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="d691f-108">Plusieurs outils existent toocreate les fichiers .vhd, par exemple une solution de virtualisation comme Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d691f-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="d691f-109">Pour obtenir des instructions, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="d691f-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="d691f-110">**Notes d'installation CentOS**</span><span class="sxs-lookup"><span data-stu-id="d691f-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="d691f-111">Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="d691f-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="d691f-112">format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**.</span><span class="sxs-lookup"><span data-stu-id="d691f-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="d691f-113">Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="d691f-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="d691f-114">Si vous utilisez VirtualBox, cela signifie en sélectionnant **une taille fixe** en tant qu’et non par défaut de toohello allouée dynamiquement lors de la création du disque de hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="d691f-115">Lorsque vous installez le système de Linux hello *recommandé* que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations).</span><span class="sxs-lookup"><span data-stu-id="d691f-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="d691f-116">Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un disque du système d’exploitation a besoin toobe jointe tooanother VM identiques pour le dépannage.</span><span class="sxs-lookup"><span data-stu-id="d691f-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="d691f-117">La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données.</span><span class="sxs-lookup"><span data-stu-id="d691f-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="d691f-118">La prise en charge du noyau pour le montage de systèmes de fichiers UDF est requise.</span><span class="sxs-lookup"><span data-stu-id="d691f-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="d691f-119">Au premier démarrage sur Azure hello mise en service de configuration est passée toohello Linux VM via un support au format UDF qui est attaché toohello invité.</span><span class="sxs-lookup"><span data-stu-id="d691f-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="d691f-120">l’agent Azure Linux de Hello doit être en mesure de toomount hello UDF fichier système tooread sa configuration et configurer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d691f-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="d691f-121">Les versions du noyau Linux antérieures à la version 2.6.37 ne prennent pas en charge NUMA sur Hyper-V avec des machines virtuelles de taille supérieure.</span><span class="sxs-lookup"><span data-stu-id="d691f-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="d691f-122">Ce problème principalement les impacts de distributions antérieures à l’aide de hello en amont noyau de Red Hat 2.6.32 et a été corrigé dans RHEL 6.6 (noyau-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="d691f-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="d691f-123">Systèmes en cours d’exécution personnalisées noyaux antérieures à 2.6.37 ou les noyaux basée sur RHEL plus anciens que 2.6.32-504 doit définir hello paramètre démarrage `numa=off` sur noyau hello de ligne de commande dans grub.conf.</span><span class="sxs-lookup"><span data-stu-id="d691f-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="d691f-124">Pour plus d’informations, consultez l’article [KB 436883](https://access.redhat.com/solutions/436883) sur Red Hat.</span><span class="sxs-lookup"><span data-stu-id="d691f-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="d691f-125">Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="d691f-126">l’agent de Hello Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="d691f-127">Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d691f-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="d691f-128">Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="d691f-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="d691f-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="d691f-129">CentOS 6.x</span></span>

1. <span data-ttu-id="d691f-130">Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="d691f-131">Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="d691f-132">CentOS 6, NetworkManager peut interférer avec l’agent de hello Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="d691f-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="d691f-133">Désinstaller ce package en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d691f-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="d691f-134">Créer ou modifier le fichier de hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="d691f-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="d691f-135">Créer ou modifier le fichier de hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="d691f-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="d691f-136">Modifier udev tooavoid de règles générant des règles statiques pour hello les interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="d691f-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="d691f-137">Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="d691f-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="d691f-138">Vérifiez que hello network service démarre au moment du démarrage en cours d’exécution hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d691f-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="d691f-139">Si vous souhaitez que les miroirs OpenLogic toouse hello qui sont hébergés dans hello centres de données Azure, puis remplacez hello `/etc/yum.repos.d/CentOS-Base.repo` fichier avec hello suivant référentiels.</span><span class="sxs-lookup"><span data-stu-id="d691f-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="d691f-140">Cette action ajoutera également hello **[openlogic]** référentiel qui inclut les packages supplémentaires, telles que l’agent de hello Azure Linux :</span><span class="sxs-lookup"><span data-stu-id="d691f-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    <span data-ttu-id="d691f-141">Hello reste de ce guide suppose que vous utilisez au moins hello `[openlogic]` référentiel, qui sera utilisé tooinstall hello Azure Linux agent ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d691f-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="d691f-142">Ajoutez hello suivant ligne too/etc/yum.conf :</span><span class="sxs-lookup"><span data-stu-id="d691f-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="d691f-143">Exécutez hello suivant commande tooclear hello yum mise à jour et les métadonnées hello système actuel avec les derniers packages de hello :</span><span class="sxs-lookup"><span data-stu-id="d691f-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="d691f-144">Sauf si vous créez une image pour une version antérieure de CentOS, il est recommandé de tooupdate que tous hello packages toohello dernière :</span><span class="sxs-lookup"><span data-stu-id="d691f-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="d691f-145">Un redémarrage peut être nécessaire après avoir exécuté cette commande.</span><span class="sxs-lookup"><span data-stu-id="d691f-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="d691f-146">(Facultatif) Installer des pilotes hello pour hello Services d’intégration Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="d691f-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="d691f-147">étape de Hello est **requis** pour CentOS 6.3 et antérieures et facultatives pour les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="d691f-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="d691f-148">Ou bien, vous pouvez suivre les instructions d’installation manuelle hello sur hello [page de téléchargement LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d691f-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="d691f-149">Installez hello Linux Agent Azure et les dépendances :</span><span class="sxs-lookup"><span data-stu-id="d691f-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="d691f-150">package de WALinuxAgent hello supprimera hello NetworkManager et packages de NetworkManager-gnome si elles n’étaient pas déjà supprimées comme décrit à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="d691f-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="d691f-151">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="d691f-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="d691f-152">toodo, ouvrez `/boot/grub/menu.lst` dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="d691f-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="d691f-153">Cela garantit également tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="d691f-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="d691f-154">En outre toohello ci-dessus, il est recommandé de trop*supprimer* hello après les paramètres :</span><span class="sxs-lookup"><span data-stu-id="d691f-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="d691f-155">Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.</span><span class="sxs-lookup"><span data-stu-id="d691f-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="d691f-156">Hello `crashkernel` option peut être gauche configuré si vous le souhaitez, mais notez que ce paramètre réduit hello de mémoire disponible dans hello VM à 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="d691f-157">CentOS 6.5 et versions antérieures doivent également définir des paramètres de noyau hello `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="d691f-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="d691f-158">Consultez Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="d691f-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="d691f-159">Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="d691f-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="d691f-160">Cela est généralement hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="d691f-160">This is usually hello default.</span></span>

15. <span data-ttu-id="d691f-161">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="d691f-162">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d691f-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="d691f-163">Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="d691f-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="d691f-164">Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :</span><span class="sxs-lookup"><span data-stu-id="d691f-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="d691f-165">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="d691f-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="d691f-166">Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d691f-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="d691f-167">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d691f-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="d691f-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="d691f-168">CentOS 7.0+</span></span>
<span data-ttu-id="d691f-169">**Modifications dans CentOS 7 (et les distributions dérivées)**</span><span class="sxs-lookup"><span data-stu-id="d691f-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="d691f-170">Préparation d’un ordinateur virtuel de CentOS 7 pour Azure est très similaire tooCentOS 6, cependant, il existe plusieurs différences importantes à noter :</span><span class="sxs-lookup"><span data-stu-id="d691f-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="d691f-171">Hello NetworkManager du package n’est plus en conflit avec l’agent de hello Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="d691f-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="d691f-172">Ce package est installé par défaut ; nous recommandons de ne pas le supprimer.</span><span class="sxs-lookup"><span data-stu-id="d691f-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="d691f-173">GRUB2 est désormais utilisé comme hello du chargeur de démarrage par défaut, afin de la procédure hello pour la modification des paramètres de noyau a changé (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="d691f-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="d691f-174">XFS est désormais hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="d691f-174">XFS is now hello default file system.</span></span> <span data-ttu-id="d691f-175">système de fichiers ext4 Hello peut toujours être utilisé si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d691f-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="d691f-176">**Configuration**</span><span class="sxs-lookup"><span data-stu-id="d691f-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="d691f-177">Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="d691f-178">Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="d691f-179">Créer ou modifier le fichier de hello `/etc/sysconfig/network` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="d691f-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="d691f-180">Créer ou modifier le fichier de hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="d691f-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="d691f-181">Modifier udev tooavoid de règles générant des règles statiques pour hello les interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="d691f-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="d691f-182">Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="d691f-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="d691f-183">Si vous souhaitez que les miroirs OpenLogic toouse hello qui sont hébergés dans hello centres de données Azure, puis remplacez hello `/etc/yum.repos.d/CentOS-Base.repo` fichier avec hello suivant référentiels.</span><span class="sxs-lookup"><span data-stu-id="d691f-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="d691f-184">Cette action ajoutera également hello **[openlogic]** référentiel qui inclut des packages pour l’agent de hello Azure Linux :</span><span class="sxs-lookup"><span data-stu-id="d691f-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    <span data-ttu-id="d691f-185">Hello reste de ce guide suppose que vous utilisez au moins hello `[openlogic]` référentiel, qui sera utilisé tooinstall hello Azure Linux agent ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d691f-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="d691f-186">Exécutez hello suivant actuel yum métadonnées de commande tooclear hello et installer les mises à jour :</span><span class="sxs-lookup"><span data-stu-id="d691f-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="d691f-187">Sauf si vous créez une image pour une version antérieure de CentOS, il est recommandé de tooupdate que tous hello packages toohello dernière :</span><span class="sxs-lookup"><span data-stu-id="d691f-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="d691f-188">Un redémarrage peut être nécessaire après avoir exécuté cette commande.</span><span class="sxs-lookup"><span data-stu-id="d691f-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="d691f-189">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="d691f-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="d691f-190">toodo, ouvrez `/etc/default/grub` un Bonjour éditeur et l’édition de texte `GRUB_CMDLINE_LINUX` paramètre, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d691f-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="d691f-191">Cela garantit également tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="d691f-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="d691f-192">Il désactive également de nouvelles conventions de nommage CentOS 7 hello pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="d691f-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="d691f-193">En outre toohello ci-dessus, il est recommandé de trop*supprimer* hello après les paramètres :</span><span class="sxs-lookup"><span data-stu-id="d691f-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="d691f-194">Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.</span><span class="sxs-lookup"><span data-stu-id="d691f-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="d691f-195">Hello `crashkernel` option peut être gauche configuré si vous le souhaitez, mais notez que ce paramètre réduit hello de mémoire disponible dans hello VM à 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="d691f-196">Une fois que vous avez terminé édition `/etc/default/grub` par ci-dessus, exécutez hello commande toorebuild hello grub configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="d691f-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="d691f-197">Si la création d’image de système hello **VMWare, VirtualBox ou KVM :** Vérifiez que les pilotes hello Hyper-V sont inclus dans hello initramfs :</span><span class="sxs-lookup"><span data-stu-id="d691f-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="d691f-198">Modifiez `/etc/dracut.conf`, ajoutez le contenu :</span><span class="sxs-lookup"><span data-stu-id="d691f-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="d691f-199">Reconstruire hello initramfs :</span><span class="sxs-lookup"><span data-stu-id="d691f-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="d691f-200">Installez hello Linux Agent Azure et les dépendances :</span><span class="sxs-lookup"><span data-stu-id="d691f-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="d691f-201">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="d691f-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="d691f-202">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d691f-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="d691f-203">Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="d691f-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="d691f-204">Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello paramètres dans suivants `/etc/waagent.conf` correctement :</span><span class="sxs-lookup"><span data-stu-id="d691f-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="d691f-205">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="d691f-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="d691f-206">Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d691f-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="d691f-207">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d691f-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d691f-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d691f-208">Next steps</span></span>
<span data-ttu-id="d691f-209">Vous êtes maintenant prêt toouse votre CentOS Linux disque dur virtuel toocreate nouvelles machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d691f-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="d691f-210">S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d691f-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

