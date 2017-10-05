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
ms.openlocfilehash: 084cdb26c7dfd8f46fb6ec7f8c48f7b4a327e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-local-linux-password-on-azure-vms"></a>Réinitialiser votre mot de passe Linux local sur les machines virtuelles Azure

Cet article présente plusieurs méthodes pour réinitialiser les mots de passe Linux locaux sur les machines virtuelles. Si le compte utilisateur a expiré ou si vous souhaitez simplement créer un nouveau compte, utilisez les méthodes suivantes pour créer un nouveau compte d’administrateur local pour retrouver l’accès à la machine virtuelle.

## <a name="symptoms"></a>Symptômes

Vous ne pouvez pas vous connecter à la machine virtuelle, et vous recevez un message vous informant que votre mot de passe est incorrect. De plus, vous ne pouvez pas utiliser VMAgent pour réinitialiser votre mot de passe sur le portail Azure. 

## <a name="manual-password-reset-procedure"></a>Procédure de réinitialisation manuelle du mot de passe

1.  Supprimez la machine virtuelle et conservez les disques joints.

2.  Joignez le lecteur du système d’exploitation comme disque de données à une autre machine virtuelle temporaire, située au même endroit.

3.  Exécutez la commande SSH suivante dans la machine virtuelle temporaire pour devenir un super utilisateur.


    ~~~~
    sudo su
    ~~~~

4.  Exécutez **fdisk -l** ou consultez les journaux système pour trouver le disque joint. Recherchez le nom du lecteur à monter. Sur la machine virtuelle temporaire, cherchez dans le fichier journal correspondant.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    Voici un exemple de sortie de la commande grep :

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  Créer un point de montage nommé **tempmount**.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Monter le disque du système d’exploitation sur le point de montage. Il faut en général monter sdc1 ou sdc2. Tout dépend de la partition d’hébergement dans le répertoire /etc du disque de la machine défaillante.

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  Effectuez une sauvegarde avant toute modification :

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  Réinitialisez le mot de passe de l'utilisateur dont vous avez besoin :

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  Déplacez les fichiers modifiés dans le bon dossier sur le disque de la machine défaillante.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back to the root and unmount the disk.

    ~~~~
    cd / umount /tempmount
    ~~~~

11. Detach the disk from the management portal.

12. Recreate the VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk to another Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How to delete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)