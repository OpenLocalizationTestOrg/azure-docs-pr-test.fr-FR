---
title: aaaHow tooreset Linux mot de passe local sur les machines virtuelles Azure | Documents Microsoft
description: "Introduire hello étapes tooreset hello Linux mot de passe local sur la machine virtuelle Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: b28a679a36bf93c6881633eefa03aef3cd33e804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="359d0-103">Comment tooreset Linux mot de passe local sur les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="359d0-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="359d0-104">Cet article présente plusieurs méthodes tooreset local Linux Virtual Machine (VM) des mots de passe.</span><span class="sxs-lookup"><span data-stu-id="359d0-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="359d0-105">Si le compte d’utilisateur hello a expiré ou que vous souhaitiez toocreate un nouveau compte, vous pouvez utiliser hello suivant les méthodes toocreate un nouveau compte d’administrateur local et ré-obtenir l’accès toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="359d0-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="359d0-106">Symptômes</span><span class="sxs-lookup"><span data-stu-id="359d0-106">Symptoms</span></span>

<span data-ttu-id="359d0-107">Vous ne pouvez pas vous connecter toohello machine virtuelle, et vous recevez un message indiquant que ce mot de passe hello que vous avez utilisé est incorrect.</span><span class="sxs-lookup"><span data-stu-id="359d0-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="359d0-108">En outre, vous ne pouvez pas utiliser défini tooreset votre mot de passe sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="359d0-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="359d0-109">Procédure de réinitialisation manuelle du mot de passe</span><span class="sxs-lookup"><span data-stu-id="359d0-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="359d0-110">Supprimer hello machine virtuelle et conserver les disques hello attaché.</span><span class="sxs-lookup"><span data-stu-id="359d0-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="359d0-111">Attacher hello lecteur du système d’exploitation comme un tooanother de disque de données temporel VM Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="359d0-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="359d0-112">Exécutez hello suivant de commande SSH sur hello temporelle VM toobecome un super utilisateur.</span><span class="sxs-lookup"><span data-stu-id="359d0-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="359d0-113">Exécutez **fdisk -l** ou regardez hello de toofind journaux système disque a été attaché récemment.</span><span class="sxs-lookup"><span data-stu-id="359d0-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="359d0-114">Recherchez toomount de nom de lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="359d0-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="359d0-115">Puis sur hello le VM temporelle, Regarder dans hello pertinentes fichier journal.</span><span class="sxs-lookup"><span data-stu-id="359d0-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="359d0-116">Hello Voici la sortie de l’exemple de commande de grep hello :</span><span class="sxs-lookup"><span data-stu-id="359d0-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="359d0-117">Créer un point de montage nommé **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="359d0-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="359d0-118">Montez le disque de hello du système d’exploitation sur le point de montage hello.</span><span class="sxs-lookup"><span data-stu-id="359d0-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="359d0-119">Vous devez généralement toomount sdc1 ou sdc2.</span><span class="sxs-lookup"><span data-stu-id="359d0-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="359d0-120">Cela dépend de hello partition directory etc à partir du disque de machine rompue hello d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="359d0-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="359d0-121">Effectuez une sauvegarde avant toute modification :</span><span class="sxs-lookup"><span data-stu-id="359d0-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="359d0-122">Réinitialiser le mot de passe de l’utilisateur hello dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="359d0-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="359d0-123">Déplacement hello modifié emplacement correct des fichiers toohello sur hello rompu disque de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="359d0-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="359d0-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="359d0-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
