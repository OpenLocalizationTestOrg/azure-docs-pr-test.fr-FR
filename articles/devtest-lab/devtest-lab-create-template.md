---
title: "Créer une image personnalisée Azure DevTest Labs à partir d’un fichier de disque dur virtuel | Microsoft Docs"
description: "Apprenez à créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide du portail Azure"
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
ms.openlocfilehash: 9983ea9b847f44ed18a6169a4bdb224b63626a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a>Créer une image personnalisée à partir d’un fichier de disque dur virtuel

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Instructions pas à pas

La procédure suivante décrit comment créer une image personnalisée à partir d’un fichier de disque dur virtuel avec le portail Azure :

1. Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Sélectionnez **Plus de services**, puis **DevTest Labs** dans la liste.

1. Sélectionnez le laboratoire souhaité dans la liste des laboratoires.  

1. Dans le panneau du laboratoire, sélectionnez **Configuration**. 

1. Dans le panneau **Configuration** du laboratoire, sélectionnez **Custom images (VHDs)** (Images personnalisées (disques durs virtuels)).

1. Dans le panneau **Images personnalisées**, sélectionnez **+Ajouter**.

    ![Ajouter une image personnalisée](./media/devtest-lab-create-template/add-custom-image.png)

1. Entrez le nom de l’image personnalisée. Ce nom s’affiche dans la liste des images de base quand vous créez une machine virtuelle.

1. Entrez la description de l’image personnalisée. Cette description s’affiche dans la liste des images de base quand vous créez une machine virtuelle.

1. Sélectionnez **VHD**.

1. Dans le panneau **VHD**, sélectionnez le fichier de disque dur virtuel souhaité.

1. Cliquez sur **OK** pour fermer le panneau **VHD**.

1. Sélectionnez **Configuration du système d’exploitation**.

1. Sous l’onglet **Configuration du système d’exploitation**, sélectionnez **Windows** ou **Linux**.

1. Si vous sélectionnez **Windows** , cochez la case pour indiquer si *Sysprep* a été exécuté sur la machine. 

1. Cliquez sur **OK** pour fermer le panneau **Configuration du système d’exploitation**.

1. Cliquez sur **OK** pour créer l’image personnalisée.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Billets de blog connexes

- [Custom images or formulas? (Images personnalisées ou formules ?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Copie d’images personnalisées entre plusieurs Azure DevTest Labs)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Étapes suivantes

- [Ajout d’une machine virtuelle à votre laboratoire](./devtest-lab-add-vm-with-artifacts.md)
