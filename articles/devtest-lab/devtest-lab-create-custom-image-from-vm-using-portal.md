---
title: "aaaCreate une image personnalisée de Azure DevTest Labs à partir d’une machine virtuelle | Documents Microsoft"
description: "Découvrez comment une image personnalisée dans Azure DevTest Labs à partir d’une machine virtuelle configurés à l’aide de toocreate hello portail Azure"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a>Créer une image personnalisée à partir d’une machine virtuelle

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>Instructions pas à pas

Vous pouvez créer une image personnalisée à partir d’une machine virtuelle configurée et ensuite utiliser cette image personnalisée de toocreate machines virtuelles identiques. Hello suit illustre comment toocreate personnalisé de l’image à partir d’une machine virtuelle :

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.

1. Dans liste hello labs, sélectionnez lab souhaité de hello.  

1. Dans le panneau de hello lab, sélectionnez **mes machines virtuelles**.
 
1. Sur hello **mes machines virtuelles** panneau, sélectionnez hello machine virtuelle à partir de laquelle image personnalisée de toocreate hello.

1. Dans le panneau de la machine virtuelle de hello, sélectionnez **créer une image personnalisée (VHD)**.

    ![Élément de menu Créer une image personnalisée](./media/devtest-lab-create-template/create-custom-image.png)

1. Sur hello **créer une image** panneau, entrez un nom et une description pour votre image personnalisée. Ces informations s’affichent dans la liste hello des bases lorsque vous créez une machine virtuelle.

    ![Panneau Créer une image personnalisée](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. Déterminez si sysprep a été exécutée sur la machine virtuelle de hello. Si sysprep de hello n’a pas été exécutée sur la machine virtuelle de hello, spécifiez si vous souhaitez que sysprep s’exécuter quand une machine virtuelle est créée à partir de cette image personnalisée.

1. Sélectionnez **OK** lorsque toocreate terminé hello image personnalisée.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Billets de blog connexes

- [Custom images or formulas? (Images personnalisées ou formules ?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Copie d’images personnalisées entre plusieurs Azure DevTest Labs)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Étapes suivantes

- [Ajouter un laboratoire tooyour de machine virtuelle](./devtest-lab-add-vm-with-artifacts.md)
