---
title: "aaaUpload disque dur virtuel du fichier tooAzure DevTest Labs, à l’aide de AzCopy | Documents Microsoft"
description: "Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide d’AzCopy"
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
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a>Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide d’AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

Dans Azure DevTest Labs, les fichiers de disque dur virtuel peuvent être utilisé toocreate des images personnalisées, qui sont des ordinateurs virtuels tooprovision utilisé. Hello suit vous guide à l’aide de tooupload d’utilitaire de ligne de commande hello AzCopy compte de stockage d’un disque dur virtuel fichier tooa du laboratoire. Une fois que vous avez téléchargé votre fichier de disque dur virtuel, hello [étapes section](#next-steps) répertorie certains articles qui expliquent comment toocreate une image personnalisée à partir de hello téléchargé le fichier de disque dur virtuel. Pour plus d’informations sur les disques et les disques durs virtuels dans Azure, consultez [À propos des disques et des VHD pour les machines virtuelles Azure](../virtual-machines/linux/about-disks-and-vhds.md).

> [!NOTE] 
>  
> L’utilitaire de ligne de commande AzCopy fonctionne exclusivement sur Windows.

## <a name="step-by-step-instructions"></a>Instructions pas à pas

Hello après le parcours des étapes vous aide à télécharger un disque dur virtuel du fichier à l’aide de tooAzure DevTest Labs [AzCopy](http://aka.ms/downloadazcopy). 

1. Obtenir le nom de hello de du laboratoire hello compte de stockage à l’aide de hello portail Azure :

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.

1. Dans liste hello labs, sélectionnez lab souhaité de hello.  

1. Dans le panneau de hello lab, sélectionnez **Configuration**. 

1. Atelier de hello **Configuration** panneau, sélectionnez **les images personnalisées (VHD)**.

1. Sur hello **les images personnalisées** panneau, sélectionnez **+ ajouter**. 

1. Sur hello **image personnalisée** panneau, sélectionnez **disque dur virtuel**.

1. Sur hello **VHD** panneau, sélectionnez **télécharger un disque dur virtuel à l’aide de PowerShell**.

    ![Télécharger un disque dur virtuel à l’aide de PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. Hello **télécharger une image à l’aide de PowerShell** panneau affiche un appel toohello **Add-AzureVhd** applet de commande. Hello du premier paramètre (*Destination*) contient hello URI pour un conteneur d’objets blob (*télécharge*) Bonjour suivant le format :

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Prenez note de hello complet des URI qu’il est utilisé dans les étapes ultérieures.

1. Téléchargez le fichier de disque dur virtuel de hello à l’aide de AzCopy :
 
1. [Téléchargez et installez la version la plus récente de AzCopy hello](http://aka.ms/downloadazcopy).

1. Ouvrez une fenêtre de commande et accédez de répertoire d’installation toohello AzCopy. Si vous le souhaitez, vous pouvez ajouter le chemin d’accès de hello AzCopy installation emplacement tooyour système. Par défaut, AzCopy est installé toohello suivant active :

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. À l’aide de hello conteneur compte de stockage blob et de clé URI, exécutez hello suivant de commande à l’invite de commandes hello. Hello *vhdFileName* valeur doit toobe entre guillemets. processus Hello de téléchargement d’un fichier de disque dur virtuel peut être longue, en fonction de la taille de hello du fichier de disque dur virtuel hello et votre vitesse de connexion.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Étapes suivantes

- [Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de hello portail Azure](devtest-lab-create-template.md)
- [Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)