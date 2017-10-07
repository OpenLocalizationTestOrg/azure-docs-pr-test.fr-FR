---
title: "disque dur virtuel d’aaaUpload fichier tooAzure DevTest Labs, à l’aide de PowerShell | Documents Microsoft"
description: "Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide de PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a>Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide de PowerShell

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

Dans Azure DevTest Labs, les fichiers de disque dur virtuel peuvent être utilisé toocreate des images personnalisées, qui sont des ordinateurs virtuels tooprovision utilisé. Hello étapes suivantes vous guident à l’aide de PowerShell tooupload compte de stockage d’un disque dur virtuel fichier tooa du laboratoire. Une fois que vous avez téléchargé votre fichier de disque dur virtuel, hello [étapes section](#next-steps) répertorie certains articles qui expliquent comment toocreate une image personnalisée à partir de hello téléchargé le fichier de disque dur virtuel. Pour plus d’informations sur les disques et les disques durs virtuels dans Azure, consultez [À propos des disques et des VHD pour les machines virtuelles Azure](../virtual-machines/linux/about-disks-and-vhds.md).

## <a name="step-by-step-instructions"></a>Instructions pas à pas

les étapes suivantes de Hello parcours vous aide à télécharger un disque dur virtuel du fichier tooAzure DevTest Labs, à l’aide de PowerShell. 

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.

1. Dans liste hello labs, sélectionnez lab souhaité de hello.  

1. Dans le panneau de hello lab, sélectionnez **Configuration**. 

1. Atelier de hello **Configuration** panneau, sélectionnez **les images personnalisées (VHD)**.

1. Sur hello **les images personnalisées** panneau, sélectionnez **+ ajouter**. 

1. Sur hello **image personnalisée** panneau, sélectionnez **disque dur virtuel**.

1. Sur hello **VHD** panneau, sélectionnez **télécharger un disque dur virtuel à l’aide de PowerShell**.

    ![Télécharger un disque dur virtuel à l’aide de PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. Sur hello **télécharger une image à l’aide de PowerShell** panneau copie hello généré PowerShell script tooa et éditeur de texte.

1. Modifier hello **LocalFilePath** paramètre Hello **Add-AzureVhd** applet de commande toopoint toohello emplacement de fichier de disque dur virtuel souhaité tooupload de hello.

1. À l’invite de PowerShell, exécutez hello **Add-AzureVhd** applet de commande (avec hello modifié **LocalFilePath** paramètre).

> [!WARNING] 
> 
> processus Hello de téléchargement d’un fichier de disque dur virtuel peut être longue, en fonction de la taille de hello du fichier de disque dur virtuel hello et votre vitesse de connexion.

## <a name="next-steps"></a>Étapes suivantes

- [Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de hello portail Azure](devtest-lab-create-template.md)
- [Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
