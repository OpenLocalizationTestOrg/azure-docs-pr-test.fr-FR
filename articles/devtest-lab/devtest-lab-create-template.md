---
title: "aaaCreate une image personnalisée de Azure DevTest Labs à partir d’un fichier de disque dur virtuel | Documents Microsoft"
description: "Découvrez comment une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de toocreate hello portail Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a>Créer une image personnalisée à partir d’un fichier de disque dur virtuel

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Instructions pas à pas

Hello étapes suivantes vous aider à créer une image personnalisée à partir d’un fichier de disque dur virtuel à l’aide de hello portail Azure :

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.

1. Dans liste hello labs, sélectionnez lab souhaité de hello.  

1. Dans le panneau de hello lab, sélectionnez **Configuration**. 

1. Atelier de hello **Configuration** panneau, sélectionnez **les images personnalisées (VHD)**.

1. Sur hello **les images personnalisées** panneau, sélectionnez **+ ajouter**.

    ![Ajouter une image personnalisée](./media/devtest-lab-create-template/add-custom-image.png)

1. Entrez le nom hello d’image personnalisée de hello. Ce nom s’affiche dans la liste hello des images de base lors de la création d’une machine virtuelle.

1. Entrez la description hello d’image personnalisée de hello. Cette description s’affiche dans la liste hello des images de base lors de la création d’une machine virtuelle.

1. Sélectionnez **VHD**.

1. À partir de hello **VHD** panneau, un fichier de disque dur virtuel sélectionnez hello souhaité.

1. Sélectionnez **OK** tooclose hello **VHD** panneau.

1. Sélectionnez **Configuration du système d’exploitation**.

1. Sur hello **configuration du système d’exploitation** , sélectionnez soit **Windows** ou **Linux**.

1. Si **Windows** est sélectionnée, spécifiez via la case à cocher hello si *Sysprep* a été exécuté sur l’ordinateur de hello. 

1. Sélectionnez **OK** tooclose hello **configuration du système d’exploitation** panneau.

1. Sélectionnez **OK** image personnalisée de toocreate hello.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Billets de blog connexes

- [Custom images or formulas? (Images personnalisées ou formules ?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Copie d’images personnalisées entre plusieurs Azure DevTest Labs)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Étapes suivantes

- [Ajouter un laboratoire tooyour de machine virtuelle](./devtest-lab-add-vm-with-artifacts.md)
