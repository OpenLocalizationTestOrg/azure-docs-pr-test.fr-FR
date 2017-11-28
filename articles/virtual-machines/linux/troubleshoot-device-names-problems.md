---
title: "les noms des périphériques aaaLinux machine virtuelle sont modifiés dans Azure | Documents Microsoft"
description: "Explique hello pourquoi les noms des périphériques sont modifiés et fournissent des solutions pour résoudre ce problème."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="4442d-103">Résolution des problèmes : les noms d’appareil des machines virtuelles Linux sont modifiés</span><span class="sxs-lookup"><span data-stu-id="4442d-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="4442d-104">Hello explique pourquoi les noms des périphériques sont modifiés après avoir redémarrer une machine virtuelle de Linux (VM), ou rattacher les disques hello.</span><span class="sxs-lookup"><span data-stu-id="4442d-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="4442d-105">Il fournit également des solutions de hello pour résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="4442d-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="4442d-106">Symptôme</span><span class="sxs-lookup"><span data-stu-id="4442d-106">Symptom</span></span>

<span data-ttu-id="4442d-107">Vous pouvez rencontrer les problèmes suivants lors de l’exécution des machines virtuelles Linux dans Microsoft Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="4442d-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="4442d-108">Hello VM échoue tooboot après un redémarrage.</span><span class="sxs-lookup"><span data-stu-id="4442d-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="4442d-109">Si les disques de données sont détachées et rattachés, les noms de périphériques hello pour les disques sont modifiés.</span><span class="sxs-lookup"><span data-stu-id="4442d-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="4442d-110">Les applications ou un scripts faisant référence à un disque par son nom d’appareil échouent.</span><span class="sxs-lookup"><span data-stu-id="4442d-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="4442d-111">Vous trouverez ce hello nom du périphérique de disque de hello est modifiée.</span><span class="sxs-lookup"><span data-stu-id="4442d-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="4442d-112">Cause :</span><span class="sxs-lookup"><span data-stu-id="4442d-112">Cause</span></span>

<span data-ttu-id="4442d-113">Chemins d’accès de périphérique dans Linux ne sont pas garantis toobe cohérent entre les redémarrages.</span><span class="sxs-lookup"><span data-stu-id="4442d-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="4442d-114">Les noms d’appareil se composent de numéros principaux (lettre) et secondaires.</span><span class="sxs-lookup"><span data-stu-id="4442d-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="4442d-115">Lorsque le pilote de périphérique de stockage de Linux hello détecte un nouveau périphérique, il assigne tooit de numéros de périphériques principaux et secondaires à partir de la plage de hello disponibles.</span><span class="sxs-lookup"><span data-stu-id="4442d-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="4442d-116">Lorsqu’un périphérique est supprimé, hello numéros sont libéré toobe le réutiliser ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="4442d-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="4442d-117">Hello dû hello analyse dans Linux planifiée par le sous-système SCSI hello se produit en mode asynchrone.</span><span class="sxs-lookup"><span data-stu-id="4442d-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="4442d-118">Hello périphérique final chemin d’accès d’affectation de noms peut varier entre les redémarrages.</span><span class="sxs-lookup"><span data-stu-id="4442d-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="4442d-119">Solution</span><span class="sxs-lookup"><span data-stu-id="4442d-119">Solution</span></span>

<span data-ttu-id="4442d-120">tooresolve ce problème, utilisez persistant d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="4442d-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="4442d-121">Il existe quatre méthodes toopersistent d’affectation de noms - par l’étiquette de système de fichiers, par uuid, par id et par chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="4442d-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="4442d-122">Nous vous recommandons d’étiquette de système de fichiers hello et les méthodes de l’UUID pour les machines virtuelles Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="4442d-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="4442d-123">La plupart des distributions fournissent également soit hello **nofail** ou **nobootwait** fstab options.</span><span class="sxs-lookup"><span data-stu-id="4442d-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="4442d-124">Ces options permettent une tooboot système même en cas de disque de hello toomount au démarrage.</span><span class="sxs-lookup"><span data-stu-id="4442d-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="4442d-125">Consultez la documentation de la distribution hello pour plus d’informations sur ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="4442d-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="4442d-126">Pour plus d’informations sur comment tooconfigure un toouse Linux VM un UUID lorsque vous ajoutez un disque de données, consultez [connecter toohello nouveau disque Linux VM toomount hello](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="4442d-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="4442d-127">Lorsque l’agent de hello Azure Linux est installé sur une machine virtuelle, il utilise Udev règles tooconstruct un ensemble de liens symboliques sous **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="4442d-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="4442d-128">Ces règles Udev peuvent être utilisées par les applications et les disques tooidentify scripts sont attaché toohello machine virtuelle, leur type, hello numéro d’unité logique.</span><span class="sxs-lookup"><span data-stu-id="4442d-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="4442d-129">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="4442d-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="4442d-130">Identifier les numéros d’unité logique des disques</span><span class="sxs-lookup"><span data-stu-id="4442d-130">Identify disk LUNs</span></span>

<span data-ttu-id="4442d-131">Une application peut utiliser des numéros d’unités logiques toofind tous les disques de hello attaché et créer des liens symboliques.</span><span class="sxs-lookup"><span data-stu-id="4442d-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="4442d-132">l’agent Azure Linux de Hello inclut désormais les règles d’uDev pour configurer des liens symboliques à partir d’une unité de toohello numéro d’unité logique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4442d-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="4442d-133">Numéro d’unité logique peut également être récupérée à partir Bonjour Linux invité à l’aide de lsscsi ou un outil similaire comme suit.</span><span class="sxs-lookup"><span data-stu-id="4442d-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="4442d-134">Ces informations de numéro d’unité logique invité peuvent être utilisées à l’abonnement Azure métadonnées tooidentify hello emplacement dans le stockage Azure hello disque dur virtuel qui stocke les données de partition hello.</span><span class="sxs-lookup"><span data-stu-id="4442d-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="4442d-135">Par exemple, utilisez hello az cli :</span><span class="sxs-lookup"><span data-stu-id="4442d-135">For example, use hello az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="4442d-136">Découvrir les UUID de système de fichiers à l’aide de l’utilitaire blkid</span><span class="sxs-lookup"><span data-stu-id="4442d-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="4442d-137">Un script ou une application peut lire la sortie hello du blkid ou autres sources similaires et construire des liens symboliques dans **dev** à utiliser.</span><span class="sxs-lookup"><span data-stu-id="4442d-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="4442d-138">sortie de Hello affiche hello UUID de tous les disques attachés toohello machine virtuelle et hello appareil fichier toowhich elles sont associées :</span><span class="sxs-lookup"><span data-stu-id="4442d-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="4442d-139">règles d’udev Hello waagent construire un ensemble de liens symboliques sous **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="4442d-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="4442d-140">application Hello peut utiliser ces informations identifier le périphérique de disque de démarrage hello et le disque de la ressource (éphémère) hello.</span><span class="sxs-lookup"><span data-stu-id="4442d-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="4442d-141">Dans Azure, les applications doivent faire référence trop**/dev/disk/azure/root-part1** ou **/dev/disk/azure-resource-part1** toodiscover ces partitions.</span><span class="sxs-lookup"><span data-stu-id="4442d-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="4442d-142">S’il existe des partitions supplémentaires à partir de la liste du blkid hello, ils se trouvent sur un disque de données.</span><span class="sxs-lookup"><span data-stu-id="4442d-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="4442d-143">Applications hello UUID pour ces partitions et vous utilisez un chemin d’accès comme hello sous nom du périphérique toodiscover hello lors de l’exécution :</span><span class="sxs-lookup"><span data-stu-id="4442d-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="4442d-144">Obtenir des règles de stockage Azure hello plus récente</span><span class="sxs-lookup"><span data-stu-id="4442d-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="4442d-145">toohello dernières règles de stockage Azure, exécutez th suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="4442d-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="4442d-146">Pour plus d’informations, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="4442d-146">For more information, see hello following articles:</span></span>

- <span data-ttu-id="4442d-147">[Ubuntu: Using UUID](https://help.ubuntu.com/community/UsingUUID) (Utilisation des UUID)</span><span class="sxs-lookup"><span data-stu-id="4442d-147">[Ubuntu: Using UUID](https://help.ubuntu.com/community/UsingUUID)</span></span>

- <span data-ttu-id="4442d-148">[Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html) (Attribution de noms persistants)</span><span class="sxs-lookup"><span data-stu-id="4442d-148">[Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)</span></span>

- <span data-ttu-id="4442d-149">[Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you) (Ce que les UUID peuvent faire pour vous)</span><span class="sxs-lookup"><span data-stu-id="4442d-149">[Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you)</span></span>

- [<span data-ttu-id="4442d-150">UDev : Introduction tooDevice Management dans le système moderne Linux</span><span class="sxs-lookup"><span data-stu-id="4442d-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

