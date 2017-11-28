---
title: "aaaCreate et téléchargez un disque dur virtuel de Linux SUSE dans Azure"
description: "En savoir plus toocreate et téléchargez un Azure disque dur virtuel (VHD) qui contient un système d’exploitation SUSE Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="ac36b-103">Préparation d'une machine virtuelle SLES ou openSUSE pour Azure</span><span class="sxs-lookup"><span data-stu-id="ac36b-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="ac36b-104">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ac36b-104">Prerequisites</span></span>
<span data-ttu-id="ac36b-105">Cet article suppose que vous avez déjà installé un SUSE ou un openSUSE Linux système d’exploitation tooa disque virtuel.</span><span class="sxs-lookup"><span data-stu-id="ac36b-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="ac36b-106">Plusieurs outils existent toocreate les fichiers .vhd, par exemple une solution de virtualisation comme Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ac36b-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="ac36b-107">Pour obtenir des instructions, consultez [installer hello rôle Hyper-V et configurer un ordinateur virtuel](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac36b-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="ac36b-108">Notes d'installation SLES/openSUSE</span><span class="sxs-lookup"><span data-stu-id="ac36b-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="ac36b-109">Consultez également les [Notes générales d’installation sous Linux](create-upload-generic.md#general-linux-installation-notes) pour obtenir d’autres conseils sur la préparation de Linux pour Azure.</span><span class="sxs-lookup"><span data-stu-id="ac36b-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="ac36b-110">format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**.</span><span class="sxs-lookup"><span data-stu-id="ac36b-110">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="ac36b-111">Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="ac36b-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="ac36b-112">Lors de l’installation de système de Linux hello, il est recommandé que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations).</span><span class="sxs-lookup"><span data-stu-id="ac36b-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="ac36b-113">Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un système d’exploitation du disque jamais besoin toobe jointe tooanother machine virtuelle pour le dépannage.</span><span class="sxs-lookup"><span data-stu-id="ac36b-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="ac36b-114">La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="ac36b-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="ac36b-115">Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="ac36b-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="ac36b-116">l’agent de Hello Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.</span><span class="sxs-lookup"><span data-stu-id="ac36b-116">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="ac36b-117">Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ac36b-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="ac36b-118">Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="ac36b-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="ac36b-119">Utilisation de SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="ac36b-119">Use SUSE Studio</span></span>
<span data-ttu-id="ac36b-120">[SUSE Studio](http://www.susestudio.com) peut facilement créer et gérer vos images SLES et openSUSE pour Azure et Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ac36b-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="ac36b-121">Il s’agit de hello approche pour la personnalisation de vos propres images SLES et openSUSE recommandée.</span><span class="sxs-lookup"><span data-stu-id="ac36b-121">This is hello recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="ac36b-122">En tant qu’une autre toobuilding votre propre disque dur virtuel, le SUSE publie également les images BYOS (apportez votre propre abonnement) pour SLES à [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="ac36b-122">As an alternative toobuilding your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="ac36b-123">Préparation de SUSE Linux Enterprise Server 11 SP4</span><span class="sxs-lookup"><span data-stu-id="ac36b-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="ac36b-124">Dans le volet central de hello du Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ac36b-124">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="ac36b-125">Cliquez sur **Connect** fenêtre hello de tooopen pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ac36b-125">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="ac36b-126">Inscrire votre tooallow de système de SUSE Linux Enterprise il toodownload les mises à jour et les packages d’installation.</span><span class="sxs-lookup"><span data-stu-id="ac36b-126">Register your SUSE Linux Enterprise system tooallow it toodownload updates and install packages.</span></span>
4. <span data-ttu-id="ac36b-127">Système de hello mise à jour avec les derniers correctifs de hello :</span><span class="sxs-lookup"><span data-stu-id="ac36b-127">Update hello system with hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="ac36b-128">Installez hello Linux Agent Azure à partir du référentiel SLES hello :</span><span class="sxs-lookup"><span data-stu-id="ac36b-128">Install hello Azure Linux Agent from hello SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="ac36b-129">Vérifiez si waagent est défini trop « on » dans la commande chkconfig et, dans le cas contraire, activez-le pour démarrer automatiquement :</span><span class="sxs-lookup"><span data-stu-id="ac36b-129">Check if waagent is set too"on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="ac36b-130">Vérifiez que le service waagent est en cours d’exécution et, dans le cas contraire, démarrez-le :</span><span class="sxs-lookup"><span data-stu-id="ac36b-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="ac36b-131">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="ac36b-131">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ac36b-132">toodo ouvrir ce « / boot/grub/menu.lst » dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="ac36b-132">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="ac36b-133">Ainsi, tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="ac36b-133">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="ac36b-134">Confirmez que fstab /boot/grub/menu.lst et/etc/les deux disques hello de référence à l’aide de son UUID (par uuid) au lieu de l’ID du disque hello (par id).</span><span class="sxs-lookup"><span data-stu-id="ac36b-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference hello disk using its UUID (by-uuid) instead of hello disk ID (by-id).</span></span> 
   
    <span data-ttu-id="ac36b-135">Obtention de l’UUID du disque</span><span class="sxs-lookup"><span data-stu-id="ac36b-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="ac36b-136">Si /dev/disk/by-id est utilisé, de mettre à jour /boot/grub/menu.lst et/etc/fstab avec la valeur appropriée par uuid de hello</span><span class="sxs-lookup"><span data-stu-id="ac36b-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with hello proper by-uuid value</span></span>
   
    <span data-ttu-id="ac36b-137">Avant la modification</span><span class="sxs-lookup"><span data-stu-id="ac36b-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="ac36b-138">Après la modification</span><span class="sxs-lookup"><span data-stu-id="ac36b-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="ac36b-139">Modifier udev tooavoid de règles générant des règles statiques pour hello les interfaces Ethernet.</span><span class="sxs-lookup"><span data-stu-id="ac36b-139">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="ac36b-140">Ces règles peuvent causer des problèmes lors du clonage d’une machine virtuelle dans Microsoft Azure ou Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="ac36b-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="ac36b-141">Il est recommandé de fichier de hello tooedit « / etc/sysconfig/réseau/dhcp » et remplacez hello `DHCLIENT_SET_HOSTNAME` paramètre toohello suivant :</span><span class="sxs-lookup"><span data-stu-id="ac36b-141">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
    
     <span data-ttu-id="ac36b-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="ac36b-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="ac36b-143">Dans « / etc/programmes sudo », commentez ou supprimez les hello lignes suivantes si elles existent :</span><span class="sxs-lookup"><span data-stu-id="ac36b-143">In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
    
     <span data-ttu-id="ac36b-144">Valeur par défaut est targetpw # demande hello de mot de passe de l’utilisateur cible de hello c'est-à-dire racine de tous les ALL=(ALL) tous les # avertissement !</span><span class="sxs-lookup"><span data-stu-id="ac36b-144">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="ac36b-145">N’utilisez cette option qu’avec « Defaults targetpw » !</span><span class="sxs-lookup"><span data-stu-id="ac36b-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="ac36b-146">Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="ac36b-146">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="ac36b-147">Cela est généralement hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="ac36b-147">This is usually hello default.</span></span>
14. <span data-ttu-id="ac36b-148">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="ac36b-148">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="ac36b-149">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="ac36b-149">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="ac36b-150">Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="ac36b-150">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="ac36b-151">Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello suivant correctement les paramètres dans /etc/waagent.conf :</span><span class="sxs-lookup"><span data-stu-id="ac36b-151">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="ac36b-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Remarque : définissez cette toowhatever vous en avez besoin toobe.</span><span class="sxs-lookup"><span data-stu-id="ac36b-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
15. <span data-ttu-id="ac36b-153">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="ac36b-153">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="ac36b-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="ac36b-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="ac36b-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="ac36b-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="ac36b-156">logout</span><span class="sxs-lookup"><span data-stu-id="ac36b-156">logout</span></span>
16. <span data-ttu-id="ac36b-157">Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ac36b-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="ac36b-158">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ac36b-158">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="ac36b-159">Préparation de openSUSE 13.1+</span><span class="sxs-lookup"><span data-stu-id="ac36b-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="ac36b-160">Dans le volet central de hello du Gestionnaire Hyper-V, sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ac36b-160">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="ac36b-161">Cliquez sur **Connect** fenêtre hello de tooopen pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ac36b-161">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="ac36b-162">Sur l’interpréteur de commandes hello, exécuter la commande hello '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="ac36b-162">On hello shell, run hello command '`zypper lr`'.</span></span> <span data-ttu-id="ac36b-163">Si cette commande renvoie la sortie similaire toohello suivant, puis les référentiels hello sont configurés comme prévu--aucune ajustements ne sont nécessaires (Notez que les numéros de version peuvent varier) :</span><span class="sxs-lookup"><span data-stu-id="ac36b-163">If this command returns output similar toohello following, then hello repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="ac36b-164">Si la commande hello ne retourne « Aucun référentiel définies... » puis utilisez hello suivant de commandes tooadd ces référentiels :</span><span class="sxs-lookup"><span data-stu-id="ac36b-164">If hello command returns "No repositories defined..." then use hello following commands tooadd these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="ac36b-165">Vous pouvez ensuite vérifier les référentiels hello ont été ajoutés en exécutant la commande hello '`zypper lr`' à nouveau.</span><span class="sxs-lookup"><span data-stu-id="ac36b-165">You can then verify hello repositories have been added by running hello command '`zypper lr`' again.</span></span> <span data-ttu-id="ac36b-166">Dans le cas où un des référentiels de mise à jour appropriée hello n’est pas activé, activez-le avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ac36b-166">In case one of hello relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="ac36b-167">Mise à jour hello noyau toohello version la plus récente :</span><span class="sxs-lookup"><span data-stu-id="ac36b-167">Update hello kernel toohello latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="ac36b-168">Tooupdate hello système ou avec tous les correctifs les plus récents hello :</span><span class="sxs-lookup"><span data-stu-id="ac36b-168">Or tooupdate hello system with all hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="ac36b-169">Installez hello Linux Agent Azure.</span><span class="sxs-lookup"><span data-stu-id="ac36b-169">Install hello Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="ac36b-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="ac36b-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="ac36b-171">Modifier la ligne de démarrage du noyau hello dans les paramètres supplémentaires de noyau tooinclude grub pour Azure.</span><span class="sxs-lookup"><span data-stu-id="ac36b-171">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ac36b-172">toodo, ouvrez « / boot/grub/menu.lst » dans un éditeur de texte et assurez-vous que ce noyau de la valeur par défaut hello inclut hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="ac36b-172">toodo this, open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
     <span data-ttu-id="ac36b-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="ac36b-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="ac36b-174">Ainsi, tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.</span><span class="sxs-lookup"><span data-stu-id="ac36b-174">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="ac36b-175">En outre, supprimez hello paramètres suivants à partir de la ligne de démarrage du noyau hello s’ils existent :</span><span class="sxs-lookup"><span data-stu-id="ac36b-175">In addition, remove hello following parameters from hello kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="ac36b-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="ac36b-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="ac36b-177">Il est recommandé de fichier de hello tooedit « / etc/sysconfig/réseau/dhcp » et remplacez hello `DHCLIENT_SET_HOSTNAME` paramètre toohello suivant :</span><span class="sxs-lookup"><span data-stu-id="ac36b-177">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
   
     <span data-ttu-id="ac36b-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="ac36b-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="ac36b-179">**Important :** dans « / etc/programmes sudo », supprimez ou commentez hello lignes suivantes si elles existent :</span><span class="sxs-lookup"><span data-stu-id="ac36b-179">**Important:** In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
   
     <span data-ttu-id="ac36b-180">Valeur par défaut est targetpw # demande hello de mot de passe de l’utilisateur cible de hello c'est-à-dire racine de tous les ALL=(ALL) tous les # avertissement !</span><span class="sxs-lookup"><span data-stu-id="ac36b-180">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="ac36b-181">N’utilisez cette option qu’avec « Defaults targetpw » !</span><span class="sxs-lookup"><span data-stu-id="ac36b-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="ac36b-182">Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="ac36b-182">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="ac36b-183">Cela est généralement hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="ac36b-183">This is usually hello default.</span></span>
10. <span data-ttu-id="ac36b-184">Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="ac36b-184">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="ac36b-185">Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="ac36b-185">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="ac36b-186">Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="ac36b-186">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="ac36b-187">Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello suivant correctement les paramètres dans /etc/waagent.conf :</span><span class="sxs-lookup"><span data-stu-id="ac36b-187">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="ac36b-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Remarque : définissez cette toowhatever vous en avez besoin toobe.</span><span class="sxs-lookup"><span data-stu-id="ac36b-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
11. <span data-ttu-id="ac36b-189">Exécutez hello suivant de commandes toodeprovision hello virtual machine et le préparer pour la configuration sur Azure :</span><span class="sxs-lookup"><span data-stu-id="ac36b-189">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="ac36b-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="ac36b-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="ac36b-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="ac36b-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="ac36b-192">logout</span><span class="sxs-lookup"><span data-stu-id="ac36b-192">logout</span></span>
12. <span data-ttu-id="ac36b-193">Vérifiez que hello Qu'agent Linux Azure s’exécute au démarrage :</span><span class="sxs-lookup"><span data-stu-id="ac36b-193">Ensure hello Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="ac36b-194">Cliquez sur **Action -> Arrêter** dans le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ac36b-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="ac36b-195">Votre VHD Linux est maintenant prêt toobe téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ac36b-195">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac36b-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ac36b-196">Next steps</span></span>
<span data-ttu-id="ac36b-197">Vous êtes maintenant prêt toouse votre SUSE Linux disque dur virtuel toocreate nouvelles machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ac36b-197">You're now ready toouse your SUSE Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="ac36b-198">S’il s’agit hello première fois que vous téléchargez tooAzure de fichier .vhd hello, consultez les étapes 2 et 3 dans [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac36b-198">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

