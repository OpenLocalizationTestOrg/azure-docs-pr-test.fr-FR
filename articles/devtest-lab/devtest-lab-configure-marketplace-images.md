---
title: "paramètres d’image aaaConfigure Azure Marketplace dans Azure DevTest Labs | Documents Microsoft"
description: "Configurer quelles images Azure Marketplace peuvent être utilisées lors de la création d’une machine virtuelle dans Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a>Configuration des paramètres d’image Azure Marketplace dans Azure DevTest Labs
DevTest Labs prend en charge la création de machines virtuelles basées sur des images Azure Marketplace en fonction de la façon dont vous avez configuré toobe d’images Azure Marketplace utilisé dans votre laboratoire. Cet article vous montre comment toospecify qui, le cas échéant, les images Azure Marketplace peuvent être utilisés lors de la création de machines virtuelles dans un laboratoire. Cela garantit que votre équipe dispose uniquement des images de Marketplace toohello accès que dont ils ont besoin. 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a>Sélection des images Azure Marketplace autorisées lors de la création d’une machine virtuelle
1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
3. Dans liste hello labs, sélectionnez lab souhaité de hello. 
4. Dans le panneau de hello lab, sélectionnez **stratégies de Configuration et**.
5. Dans le panneau **Configuration et stratégies** du laboratoire, sous **Bases de machine virtuelle**, sélectionnez **Images de la Place de marché**.
6. Spécifiez si vous souhaitez que tous les hello qualifié toobe images Azure Marketplace disponible pour une utilisation comme base d’une nouvelle machine virtuelle. Si vous sélectionnez **Oui**, puis toutes les images d’Azure Marketplace hello qui remplissent toutes hello après les critères sont autorisés dans le laboratoire de hello :
   
   * image de Hello crée une seule machine virtuelle, **et**
   * image de Hello utilise les machines virtuelles Azure Resource Manager tooprovision, **et**
   * image de Hello ne nécessite pas d’achat d’un régime de licences supplémentaires
     
    Si vous ne souhaitez aucun toobe images autorisé, ou vous souhaitez toospecify images qui peuvent être utilisées, sélectionnez **non**.
     
     ![Option tooallow toobe d’images Marketplace tous les utilisé en tant qu’images de base pour les machines virtuelles](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. Si vous sélectionnez **non** toohello précédente étape, hello **autorisées images/sélectionner tous les** case à cocher est activée. 
   Vous pouvez utiliser cette option avec recherche hello tooquickly Sélectionnez ou désélectionnez tous les éléments de hello affichés dans la liste de hello.
   * Sélectionnez hello Azure Marketplace images tooallow pour la création de la machine virtuelle individuellement en activant les cases à cocher correspondantes de chaque image.
   * N’effectuez aucune sélection à partir de la liste de hello si vous ne souhaitez pas tooallow tout toobe d’images Azure Marketplace utilisé dans le laboratoire de hello.
   
    ![Vous pouvez spécifier les images Azure Marketplace pouvant être utilisées en tant qu’images de base pour des machines virtuelles](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez configuré la façon dont les images Azure Marketplace sont autorisés lors de la création d’une machine virtuelle, étape suivante de hello est trop[ajouter un laboratoire tooyour de machine virtuelle](devtest-lab-add-vm-with-artifacts.md).

