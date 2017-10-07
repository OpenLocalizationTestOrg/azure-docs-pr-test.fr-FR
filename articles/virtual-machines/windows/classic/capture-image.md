---
title: "aaaCapture une image d’une machine virtuelle de Windows Azure | Documents Microsoft"
description: "Capturer une image d’ordinateur virtuel Azure Windows créé avec le modèle de déploiement classique hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Capturer une image d’ordinateur virtuel Azure Windows créé avec le modèle de déploiement classique hello.
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour plus d’informations sur le modèle Azure Resource Manager, voir [Capturer une image managée d’une machine virtuelle généralisée dans Azure](../capture-image-resource.md).

Cet article vous montre comment toocapture une machine virtuelle Azure exécutant Windows afin de pouvoir l’utiliser comme une image toocreate autres machines virtuelles. Cette image comprend le disque du système d’exploitation hello et les disques de données qui sont attachés toohello virtual machine. Il n’inclut pas les configurations de mise en réseau, vous devez tooset des configurations de réseau lorsque vous créez des autres ordinateurs virtuels qui utilisent l’image de hello hello.

Magasins Azure hello image sous **images de machine virtuelle (classique)**, un **de calcul** service répertorié lorsque vous affichez tous les hello services Azure. Il s’agit de hello même endroit où sont stockées les images que vous avez téléchargé. Pour plus d’informations sur les images, consultez la page [À propos des images pour les machines virtuelles](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).

## <a name="before-you-begin"></a>Avant de commencer
Ces étapes supposent que vous avez déjà créé une machine virtuelle Azure et configuré le système d’exploitation de hello, y compris l’attachement des disques de données. Si vous n’avez pas encore fait, consultez hello suivant des articles pour plus d’informations sur la création et la préparation de la machine virtuelle de hello :

* [Création d’une machine virtuelle à partir d’une image](createportal.md)
* [Machine virtuelle de tooa de disque tooattach données](attach-disk.md)
* Assurez-vous que les rôles de serveur hello sont pris en charge avec Sysprep. Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

> [!WARNING]
> Ce processus supprime l’ordinateur virtuel d’origine de hello après sa capture.
>
>

Toocapturing préalable une image de machine virtuelle Azure, il est recommandé de sauvegarder la machine virtuelle cible hello. Les machines virtuelles Azure peuvent être sauvegardées à l’aide d’Azure Backup. Pour plus d’informations, voir [Sauvegarde des machines virtuelles Azure](../../../backup/backup-azure-vms.md). D’autres solutions sont disponibles auprès de partenaires certifiés. toofind ce qui est actuellement disponible, recherchez hello Azure Marketplace.

## <a name="capture-hello-virtual-machine"></a>Capture de machine virtuelle de hello
1. Bonjour [portail Azure](http://portal.azure.com), **Connect** toohello virtuels. Pour obtenir des instructions, consultez [comment toosign dans la machine virtuelle de tooa exécutant Windows Server][How toosign in tooa virtual machine running Windows Server].
2. Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.
3. Basculez hello trop`%windir%\system32\sysprep`, puis exécutez sysprep.exe.
4. Hello **outil de préparation système** boîte de dialogue s’affiche. Hello suivant :

   * Dans **Action de nettoyage du système**, sélectionnez **Entrer en mode OOBE (OOBE)** et vérifiez que la case à cocher **Généraliser** est activée. Pour plus d’informations sur l’utilisation de Sysprep, consultez [comment tooUse Sysprep : Introduction][How tooUse Sysprep: An Introduction].
   * Dans **Options d’arrêt**, sélectionnez **Arrêter**.
   * Cliquez sur **OK**.

   ![Exécutez Sysprep](./media/capture-image/SysprepGeneral.png)
5. Sysprep s’arrête l’ordinateur virtuel hello, ce qui modifie le statut hello de machine virtuelle de hello Bonjour Azure portal trop**arrêté**.
6. Bonjour portail Azure, cliquez sur **Machines virtuelles (classiques)** et sélectionnez hello machine virtuelle toocapture. Hello **images de machine virtuelle (classique)** groupe est répertorié sous **de calcul** lorsque vous affichez **davantage de services**.

7. Dans la barre de commandes hello, cliquez sur **Capture**.

   ![Capture machine virtuelle](./media/capture-image/CaptureVM.png)

   Hello **hello de Capture de Machine virtuelle** boîte de dialogue s’affiche.

8. Dans **nom de l’Image**, tapez un nom pour la nouvelle image de hello. Dans **libellé de l’Image**, tapez une étiquette pour la nouvelle image de hello.

9. Cliquez sur **j’ai exécuté Sysprep sur l’ordinateur virtuel de hello**. Cette case à cocher fait référence à des actions de toohello avec Sysprep dans les étapes 3 à 5. Une image _doit_ être généralisée à l’exécution de Sysprep avant d’ajouter un serveur Windows ensemble tooyour d’images d’images personnalisées.

10. Une fois la capture hello terminée, nouvelle image de hello devienne disponible dans hello **Marketplace**, Bonjour **de calcul**, **images de machine virtuelle (classique)** conteneur.

    ![Capture d’image réussie](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Étapes suivantes
image de Hello est prêt toobe utilisé toocreate virtual machines. toodo, vous allez créer une machine virtuelle en sélectionnant hello **davantage de services** élément de menu au bas de hello de menu des services hello, puis **images de machine virtuelle (classique)** Bonjour **decalcul**groupe. Pour obtenir des instructions, consultez [Création d’une machine virtuelle à partir d’une image](createportal.md).

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
