---
title: "aaaDownload un disque dur virtuel Windows à partir de Azure | Documents Microsoft"
description: "Téléchargez un disque dur virtuel Windows à l’aide de hello portail Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>Télécharger un VHD Windows à partir d’Azure

Dans cet article, vous apprendrez comment toodownload un [(VHD) du disque dur virtuel Windows](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) fichier à partir d’Azure à l’aide hello portail Azure. 

Machines virtuelles (VM) en cours d’utilisation Azure [disques](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) comme un toostore place un système d’exploitation, des applications et des données. Toutes les machines virtuelles Azure possèdent au moins deux disques : un disque de système d’exploitation Windows et un disque temporaire. disque de système d’exploitation Hello est initialement créé à partir d’une image et disque de système d’exploitation hello et image de hello sont des disques durs virtuels stockés dans un compte de stockage Azure. Les machines virtuelles peuvent également disposer d’un ou plusieurs disques de données, également stockés sur les VHD.

## <a name="stop-hello-vm"></a>Arrêter hello machine virtuelle

Un disque dur virtuel ne peut être téléchargé à partir d’Azure, si elle est attachée tooa machine virtuelle en cours d’exécution. Vous devez toodownload de machine virtuelle hello toostop un disque dur virtuel. Si vous voulez toouse un disque dur virtuel en tant qu’un [image](tutorial-custom-images.md) toocreate autres machines virtuelles avec de nouveaux disques, vous utilisez [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello du système d’exploitation contenu dans le fichier de hello et arrêtez la machine virtuelle de hello. toouse hello disque dur virtuel en tant que disque d’une nouvelle instance d’un ordinateur virtuel existant ou d’un disque de données, vous seulement devez toostop et désallouer hello machine virtuelle.

toouse hello de disque dur virtuel en tant qu’une image toocreate autres machines virtuelles, procédez comme suit :

1.  Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2.  [Se connecter toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
3.  Sur la machine virtuelle de hello, ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur.
4.  Basculez hello trop*%windir%\system32\sysprep* et exécutez sysprep.exe.
5.  Dans la boîte de dialogue Outil de préparation système hello, sélectionnez **entrer le système Out-of-Box Experience (OOBE)**et vous assurer que **Generalize** est sélectionnée.
6.  Dans Options d’arrêt, sélectionnez **Arrêter**, puis cliquez sur **OK**. 

toouse hello disque dur virtuel en tant que disque d’une nouvelle instance d’un ordinateur virtuel existant ou d’un disque de données, procédez comme suit :

1.  Dans menu Hub hello hello portail Azure, cliquez sur **virtuels**.
2.  Sélectionnez hello machine virtuelle à partir de la liste de hello.
3.  Dans le panneau hello pour hello machine virtuelle, cliquez sur **arrêter**.

    ![Arrêter la machine virtuelle](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Générer une URL de SAP

fichier de disque dur virtuel toodownload hello, vous devez toogenerate une [signature d’accès partagé (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Lorsque l’URL de hello est généré, un délai d’expiration est affecté toohello URL.

1.  Dans menu hello du panneau hello pour hello machine virtuelle, cliquez sur **disques**.
2.  Sélectionnez le disque du système d’exploitation hello pour hello machine virtuelle, puis cliquez sur **exporter**.
3.  Définir le délai d’expiration de hello de hello URL trop*36000*.
4.  Cliquez sur **Générer l’URL**.

    ![Générer une URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> délai d’expiration de Hello est augmentée de hello par défaut tooprovide suffisamment de temps toodownload hello grand fichier de disque dur virtuel pour un système d’exploitation Windows. Vous pouvez vous attendre un fichier de disque dur virtuel qui contient tootake de système d’exploitation Windows Server hello plusieurs toodownload heures en fonction de votre connexion. Si vous téléchargez un disque dur virtuel pour un disque de données, la durée par défaut de hello est suffisante. 
> 
> 

## <a name="download-vhd"></a>Télécharger un VHD

1.  URL hello qui a été généré, cliquez sur fichier de disque dur virtuel de téléchargement hello.

    ![Télécharger un VHD](./media/download-vhd/export-download.png)

2.  Vous devrez peut-être tooclick **enregistrer** dans le téléchargement de hello navigateur toostart hello. nom par défaut de Hello pour le fichier de disque dur virtuel hello est *abcd*.

    ![Cliquez sur Enregistrer dans le navigateur de hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment trop[télécharger un tooAzure de fichier de disque dur virtuel](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
- [Créez des disques gérés à partir de disques non gérés dans un compte de stockage](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
- [Gérez des disques Azure avec PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

