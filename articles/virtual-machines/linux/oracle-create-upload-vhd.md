---
title: "aaaCreate et télécharger un disque dur virtuel de Oracle Linux | Documents Microsoft"
description: "En savoir plus toocreate et téléchargez un Azure disque dur virtuel (VHD) qui contient un système d’exploitation de Oracle Linux."
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
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="82310-103">Préparation d’une machine virtuelle Linux Oracle pour Azure</span><span class="sxs-lookup"><span data-stu-id="82310-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="82310-104">Composants requis</span><span class="sxs-lookup"><span data-stu-id="82310-104">Prerequisites</span></span>
<span data-ttu-id="82310-105">Cet article suppose que vous avez déjà installé un disque dur virtuel tooa Oracle Linux système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="82310-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="82310-106">Plusieurs outils existent toocreate les fichiers .vhd, par exemple une solution de virtualisation comme Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="82310-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="82310-107">Pour obtenir des instructions, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="82310-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="82310-108">Notes générales d’installation d’Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="82310-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="82310-109">Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="82310-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="82310-110">Le noyau Oracle compatible Red Hat et leur noyau UEK3 (Unbreakable Enterprise Kernel) sont tous les deux pris en charge sur Hyper-V et Azure.</span><span class="sxs-lookup"><span data-stu-id="82310-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="82310-111">Pour de meilleurs résultats, soyez noyau de dernière toohello tooupdate que lors de la préparation de votre disque dur virtuel de Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="82310-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="82310-112">Oracle UEK2 n’est pas prise en charge Hyper-V et sur Azure qu’il n’inclut pas les pilotes hello requis.</span><span class="sxs-lookup"><span data-stu-id="82310-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="82310-113">format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**.</span><span class="sxs-lookup"><span data-stu-id="82310-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="82310-114">Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="82310-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="82310-115">Lors de l’installation de système de Linux hello, il est recommandé que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations).</span><span class="sxs-lookup"><span data-stu-id="82310-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="82310-116">Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un système d’exploitation du disque jamais besoin toobe jointe tooanother machine virtuelle pour le dépannage.</span><span class="sxs-lookup"><span data-stu-id="82310-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="82310-117">La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="82310-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="82310-118">NUMA n’est pas pris en charge pour les tailles de machine virtuelle plus grandes en raison du bogue tooa dans les versions de noyau Linux ci-dessous 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="82310-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="82310-119">Ce problème principalement les impacts à l’aide de distributions hello rouge en amont noyau de Hat 2.6.32.</span><span class="sxs-lookup"><span data-stu-id="82310-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="82310-120">Installation manuelle de l’agent Azure Linux de hello (waagent) sera automatiquement désactivée NUMA dans la configuration de GRUB hello pour le noyau Linux de hello.</span><span class="sxs-lookup"><span data-stu-id="82310-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="82310-121">Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="82310-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="82310-122">Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="82310-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="82310-123">l’agent de Hello Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.</span><span class="sxs-lookup"><span data-stu-id="82310-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="82310-124">Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="82310-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="82310-125">Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="82310-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="82310-126">Vérifiez que hello `Addons` référentiel est activé.</span><span class="sxs-lookup"><span data-stu-id="82310-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="82310-127">Modifier le fichier de hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) et remplacez-la par hello `enabled=0` trop`enabled=1` sous **[ol6_addons]** ou **[ol7_addons]** dans cette fichier.</span><span class="sxs-lookup"><span data-stu-id="82310-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="82310-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="82310-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="82310-129">Vous devez effectuer les étapes de configuration spécifique dans le système d’exploitation hello toorun de machine virtuelle hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="82310-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="82310-130">Dans le volet central de hello du Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="82310-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="82310-131">Cliquez sur **Connect** fenêtre hello de tooopen pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="82310-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="82310-132">Désinstaller NetworkManager en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="82310-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="82310-133">**Remarque :** si le package de hello n’est pas déjà installé, cette commande échoue avec un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="82310-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="82310-134">Ceci est normal.</span><span class="sxs-lookup"><span data-stu-id="82310-134">This is expected.</span></span>
4. <span data-ttu-id="82310-135">Créez un fichier nommé **réseau** Bonjour `/etc/sysconfig/` répertoire contenant hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="82310-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="82310-136">Créez un fichier nommé **ifcfg-eth0** Bonjour `/etc/sysconfig/network-scripts/` répertoire contenant hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="82310-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="82310-137">Modifier udev tooavoid de règles générant des règles statiques pour hello les interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="82310-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="82310-138">Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="82310-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="82310-139">Vérifiez que hello network service démarre au moment du démarrage en cours d’exécution hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="82310-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="82310-140">Installer python-pyasn1 en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="82310-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="82310-141">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="82310-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="82310-142">toodo ouvrir ce « / boot/grub/menu.lst » dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="82310-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="82310-143">Cela garantit également tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="82310-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="82310-144">Cette opération va désactiver NUMA en raison du bogue tooa dans le noyau compatible de Red Hat d’Oracle.</span><span class="sxs-lookup"><span data-stu-id="82310-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="82310-145">En outre toohello ci-dessus, il est recommandé de trop*supprimer* hello après les paramètres :</span><span class="sxs-lookup"><span data-stu-id="82310-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="82310-146">Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.</span><span class="sxs-lookup"><span data-stu-id="82310-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="82310-147">Hello `crashkernel` option peut être gauche configuré si vous le souhaitez, mais notez que ce paramètre réduit hello de mémoire disponible dans hello VM à 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites hello.</span><span class="sxs-lookup"><span data-stu-id="82310-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="82310-148">Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="82310-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="82310-149">Cela est généralement hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="82310-149">This is usually hello default.</span></span>
11. <span data-ttu-id="82310-150">Installez hello Linux Agent Azure en exécutant hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="82310-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="82310-151">version la plus récente Hello est 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="82310-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="82310-152">Notez que le lot d’installation hello WALinuxAgent supprimera hello NetworkManager et packages de NetworkManager-gnome si elles n’étaient pas déjà supprimées comme décrit à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="82310-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="82310-153">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="82310-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="82310-154">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="82310-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="82310-155">Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="82310-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="82310-156">Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello suivant correctement les paramètres dans /etc/waagent.conf :</span><span class="sxs-lookup"><span data-stu-id="82310-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="82310-157">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="82310-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="82310-158">Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="82310-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="82310-159">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="82310-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="82310-160">Oracle Linux 7.0+</span><span class="sxs-lookup"><span data-stu-id="82310-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="82310-161">**Modifications dans Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="82310-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="82310-162">Préparation d’une machine virtuelle de Oracle Linux 7 pour Azure est très similaire tooOracle Linux 6, cependant, il existe plusieurs différences importantes à noter :</span><span class="sxs-lookup"><span data-stu-id="82310-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="82310-163">Noyau compatible de hello Red Hat et UEK3 d’Oracle sont pris en charge dans Azure.</span><span class="sxs-lookup"><span data-stu-id="82310-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="82310-164">noyau de UEK3 Hello est recommandé.</span><span class="sxs-lookup"><span data-stu-id="82310-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="82310-165">Hello NetworkManager du package n’est plus en conflit avec l’agent de hello Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="82310-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="82310-166">Ce package est installé par défaut ; nous recommandons de ne pas le supprimer.</span><span class="sxs-lookup"><span data-stu-id="82310-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="82310-167">GRUB2 est désormais utilisé comme hello du chargeur de démarrage par défaut, afin de la procédure hello pour la modification des paramètres de noyau a changé (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="82310-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="82310-168">XFS est désormais hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="82310-168">XFS is now hello default file system.</span></span> <span data-ttu-id="82310-169">système de fichiers ext4 Hello peut toujours être utilisé si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="82310-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="82310-170">**Configuration**</span><span class="sxs-lookup"><span data-stu-id="82310-170">**Configuration steps**</span></span>

1. <span data-ttu-id="82310-171">Dans le Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="82310-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="82310-172">Cliquez sur **Connect** tooopen une fenêtre de console pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="82310-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="82310-173">Créez un fichier nommé **réseau** Bonjour `/etc/sysconfig/` répertoire contenant hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="82310-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="82310-174">Créez un fichier nommé **ifcfg-eth0** Bonjour `/etc/sysconfig/network-scripts/` répertoire contenant hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="82310-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="82310-175">Modifier udev tooavoid de règles générant des règles statiques pour hello les interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="82310-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="82310-176">Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="82310-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="82310-177">Vérifiez que hello network service démarre au moment du démarrage en cours d’exécution hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="82310-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="82310-178">Installer le package de python-pyasn1 de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="82310-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="82310-179">Exécutez hello suivant actuel yum métadonnées de commande tooclear hello et installer les mises à jour :</span><span class="sxs-lookup"><span data-stu-id="82310-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="82310-180">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="82310-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="82310-181">toodo ce Ouvrez « / etc/par défaut/grub » dans un hello éditeur et l’édition de texte `GRUB_CMDLINE_LINUX` paramètre, par exemple :</span><span class="sxs-lookup"><span data-stu-id="82310-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="82310-182">Cela garantit également tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="82310-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="82310-183">Il désactive également de nouvelles conventions de nommage OEL 7 hello pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="82310-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="82310-184">En outre toohello ci-dessus, il est recommandé de trop*supprimer* hello après les paramètres :</span><span class="sxs-lookup"><span data-stu-id="82310-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="82310-185">Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série.</span><span class="sxs-lookup"><span data-stu-id="82310-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="82310-186">Hello `crashkernel` option peut être gauche configuré si vous le souhaitez, mais notez que ce paramètre réduit hello de mémoire disponible dans hello VM à 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites hello.</span><span class="sxs-lookup"><span data-stu-id="82310-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="82310-187">Une fois que vous avez terminé la modification « / etc/par défaut/grub » par ci-dessus, exécutez hello commande toorebuild hello grub configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="82310-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="82310-188">Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="82310-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="82310-189">Cela est généralement hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="82310-189">This is usually hello default.</span></span>
12. <span data-ttu-id="82310-190">Installez hello Linux Agent Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="82310-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="82310-191">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="82310-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="82310-192">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="82310-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="82310-193">Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="82310-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="82310-194">Après avoir installé hello Linux Agent Azure (voir l’étape précédente de hello), modifier hello suivant correctement les paramètres dans /etc/waagent.conf :</span><span class="sxs-lookup"><span data-stu-id="82310-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="82310-195">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="82310-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="82310-196">Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="82310-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="82310-197">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="82310-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82310-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82310-198">Next steps</span></span>
<span data-ttu-id="82310-199">Vous êtes maintenant prêt toouse votre Oracle Linux .vhd toocreate nouvelles machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="82310-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="82310-200">S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="82310-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

