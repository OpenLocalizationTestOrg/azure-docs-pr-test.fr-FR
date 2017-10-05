---
title: "Réinitialiser votre mot de passe Linux local sur les machines virtuelles Azure | Microsoft Docs"
description: "Introduction des étapes pour réinitialiser votre mot de passe Linux local sur la machine virtuelle Azure"
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
ms.openlocfilehash: bd48128a078821b7a4baa02d5d7ceecc6de99608
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-reset-local-linux-password-on-azure-vms"></a><span data-ttu-id="5ffc9-103">Réinitialiser votre mot de passe Linux local sur les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="5ffc9-103">How to reset local Linux password on Azure VMs</span></span>

<span data-ttu-id="5ffc9-104">Cet article présente plusieurs méthodes pour réinitialiser les mots de passe Linux locaux sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-104">This article introduces several methods to reset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="5ffc9-105">Si le compte utilisateur a expiré ou si vous souhaitez simplement créer un nouveau compte, utilisez les méthodes suivantes pour créer un nouveau compte d’administrateur local pour retrouver l’accès à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-105">If the user account is expired or you just want to create a new account, you can use the following methods to create a new local admin account and re-gain access to the VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="5ffc9-106">Symptômes</span><span class="sxs-lookup"><span data-stu-id="5ffc9-106">Symptoms</span></span>

<span data-ttu-id="5ffc9-107">Vous ne pouvez pas vous connecter à la machine virtuelle, et vous recevez un message vous informant que votre mot de passe est incorrect.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-107">You can't log in to the VM, and you receive a message that indicates that the password that you used is incorrect.</span></span> <span data-ttu-id="5ffc9-108">De plus, vous ne pouvez pas utiliser VMAgent pour réinitialiser votre mot de passe sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-108">Additionally, you can't use VMAgent to reset your password on the Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="5ffc9-109">Procédure de réinitialisation manuelle du mot de passe</span><span class="sxs-lookup"><span data-stu-id="5ffc9-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="5ffc9-110">Supprimez la machine virtuelle et conservez les disques joints.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-110">Delete the VM and keep the attached disks.</span></span>

2.  <span data-ttu-id="5ffc9-111">Joignez le lecteur du système d’exploitation comme disque de données à une autre machine virtuelle temporaire, située au même endroit.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-111">Attach the OS Drive as a data disk to another temporal VM in the same location.</span></span>

3.  <span data-ttu-id="5ffc9-112">Exécutez la commande SSH suivante dans la machine virtuelle temporaire pour devenir un super utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-112">Run the following SSH command on the temporal VM to become a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="5ffc9-113">Exécutez **fdisk -l** ou consultez les journaux système pour trouver le disque joint.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-113">Run **fdisk -l** or look at system logs to find the newly attached disk.</span></span> <span data-ttu-id="5ffc9-114">Recherchez le nom du lecteur à monter.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-114">Locate the drive name to mount.</span></span> <span data-ttu-id="5ffc9-115">Sur la machine virtuelle temporaire, cherchez dans le fichier journal correspondant.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-115">Then on the temporal VM, look in the relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="5ffc9-116">Voici un exemple de sortie de la commande grep :</span><span class="sxs-lookup"><span data-stu-id="5ffc9-116">The following is example output of the grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="5ffc9-117">Créer un point de montage nommé **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="5ffc9-118">Monter le disque du système d’exploitation sur le point de montage.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-118">Mount the OS disk on the mount point.</span></span> <span data-ttu-id="5ffc9-119">Il faut en général monter sdc1 ou sdc2.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-119">You usually need to mount sdc1 or sdc2.</span></span> <span data-ttu-id="5ffc9-120">Tout dépend de la partition d’hébergement dans le répertoire /etc du disque de la machine défaillante.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-120">This will depend on the hosting partition in /etc directory from the broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="5ffc9-121">Effectuez une sauvegarde avant toute modification :</span><span class="sxs-lookup"><span data-stu-id="5ffc9-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="5ffc9-122">Réinitialisez le mot de passe de l'utilisateur dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="5ffc9-122">Reset the user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="5ffc9-123">Déplacez les fichiers modifiés dans le bon dossier sur le disque de la machine défaillante.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-123">Move the modified files to the correct location on the broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back to the root and unmount the disk.

    ~~~~
    <span data-ttu-id="5ffc9-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="5ffc9-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach the disk from the management portal.

12. Recreate the VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk to another Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How to delete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)