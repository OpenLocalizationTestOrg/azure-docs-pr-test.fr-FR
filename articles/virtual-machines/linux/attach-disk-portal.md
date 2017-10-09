---
title: "aaaAttach un tooa de disque de données Linux VM | Documents Microsoft"
description: "Comment tooattach données nouvelles ou existantes disque tooa Linux VM dans le portail Azure à l’aide de hello hello modèle de déploiement de gestionnaire de ressources."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a>Tooattach données de disque tooa Linux VM Bonjour portail Azure
Cet article explique comment tooattach nouveaux et existant disques tooa une machine virtuelle Linux via hello portail Azure. Vous pouvez également [attacher un tooa de disque de données machine virtuelle Windows Bonjour Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Vous pouvez choisir toouse soit des disques Azure géré ou non des disques. Disques gérés sont gérés par hello plateforme Azure et ne nécessitent pas de n’importe quel toostore préparation ou emplacement les. Les disques non gérés requièrent un compte de stockage et sont soumis à un certain nombre de [quotas et de limites](../../azure-subscription-service-limits.md#storage-limits). Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](../windows/managed-disks-overview.md).

Avant de joindre des disques tooyour machine virtuelle, consultez les conseils suivants :

* taille de Hello de machine virtuelle de hello détermine le nombre que vous pouvez attacher des disques de données. Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* toouse stockage Premium, vous devez un ordinateur virtuel de la série DS ou GS-series. Vous pouvez utiliser des disques Premium et Standard avec ces machines virtuelles. Le stockage Premium est disponible dans certaines régions. Pour plus d’informations, voir l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Les disques attachés toovirtual machines sont réellement les fichiers .vhd stockés dans Azure. Pour en savoir plus, voir la section [À propos des disques et VHD pour machines virtuelles](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-hello-virtual-machine"></a>Trouver l’ordinateur virtuel de hello
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le menu du Hub hello, cliquez sur **virtuels**.
3. Sélectionnez hello virtuels à partir de la liste de hello.
4. toohello Virtual machines panneau, dans **Essentials**, cliquez sur **disques**.
   
    ![Ouverture des paramètres d’un disque](./media/attach-disk-portal/find-disk-settings.png)

Continuez en suivant les instructions pour attacher un [disque géré](#use-azure-managed-disks) ou un [disque non géré](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Utiliser Azure Managed Disks

### <a name="attach-a-new-disk"></a>Attacher un nouveau disque

1. Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.
2. Cliquez sur le menu déroulant de hello pour **nom** et sélectionnez **créer disque**:

    ![Créer un disque géré Azure](./media/attach-disk-portal/create-new-md.png)

3. Entrez un nom pour votre disque géré. Passez en revue les paramètres par défaut de hello, mettre à jour si nécessaire, puis cliquez sur **créer**.
   
   ![Examen des paramètres d’un disque](./media/attach-disk-portal/create-new-md-settings.png)

4. Cliquez sur **enregistrer** toocreate hello gérés disque et mise à jour de configuration d’ordinateur virtuel hello :

   ![Enregistrer le nouveau disque géré Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. Une fois Azure crée le disque de hello et attache la machine virtuelle de toohello, nouveau disque de hello est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**. Disques gérés comme une ressource de niveau supérieur, disque de hello apparaît au niveau racine hello hello du groupe de ressources :

   ![Disque géré Azure dans le groupe de ressources](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>Association d'un disque existant
1. Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.
2. Cliquez sur le menu déroulant de hello pour **nom** tooview une liste existante géré tooyour de disques accessibles abonnement Azure. Sélectionnez hello géré tooattach de disque :

   ![Attacher un disque géré Azure existant](./media/attach-disk-portal/select-existing-md.png)

3. Cliquez sur **enregistrer** existant de hello tooattach gérés disque et mise à jour de configuration d’ordinateur virtuel hello :
   
   ![Enregistrer les mises à jour Azure Managed Disk](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Une fois Azure attache hello disque toohello virtual machine, il est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.

## <a name="use-unmanaged-disks"></a>Utiliser des disques non gérés

### <a name="attach-a-new-disk"></a>Attacher un nouveau disque

1. Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.
2. Passez en revue les paramètres par défaut de hello, mettre à jour si nécessaire, puis cliquez sur **OK**.
   
   ![Examen des paramètres d’un disque](./media/attach-disk-portal/attach-new.png)
3. Une fois Azure crée le disque de hello et attache la machine virtuelle de toohello, nouveau disque de hello est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.

### <a name="attach-an-existing-disk"></a>Association d'un disque existant
1. Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.
2. Sous **Attacher un disque existant**, cliquez sur **Fichier VHD**.
   
   ![Attachement d’un disque existant](./media/attach-disk-portal/attach-existing.png)
3. Sous **comptes de stockage**, sélectionnez le compte de hello et conteneur qui contient le fichier .vhd de hello.
   
   ![Recherche d’emplacement VHD](./media/attach-disk-portal/find-storage-container.png)
4. Sélectionnez le fichier .vhd de hello.
5. Sous **attachement du disque existant**, fichier hello vous venez de sélectionner est répertorié sous **fichier de disque dur virtuel**. Cliquez sur **OK**.
6. Une fois Azure attache hello disque toohello virtual machine, il est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.


## <a name="next-steps"></a>Étapes suivantes
Une fois le disque de hello est ajouté, vous devez tooprepare son utilisation. Pour plus d'informations, consultez [Initialisation d’un nouveau disque de données sous Linux](add-disk.md).
