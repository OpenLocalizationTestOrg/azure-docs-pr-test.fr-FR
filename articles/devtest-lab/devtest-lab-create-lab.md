---
title: aaaCreate un laboratoire dans Azure DevTest Labs | Documents Microsoft
description: "Créer un laboratoire dans Azure DevTest Labs pour les machines virtuelles"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Créer un laboratoire dans Azure DevTest Labs
Un laboratoire dans Azure DevTest Labs est infrastructure hello englobe un groupe de ressources, telles que les Machines virtuelles (VM), qui vous permet de mieux gérer ces ressources en spécifiant des limites et quotas. Cet article vous guide tout au long des processus de hello de création d’un laboratoire à l’aide de hello portail Azure.

## <a name="prerequisites"></a>Composants requis
toocreate un laboratoire, vous devez :

* Un abonnement Azure. toolearn sur les options d’achat d’Azure, consultez [comment toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) ou [version d’évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/). Vous devez être propriétaire de hello du laboratoire de hello abonnement toocreate hello.

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>Étapes toocreate un laboratoire dans Azure DevTest Labs
Hello suit illustre comment toouse hello toocreate portail Azure, un laboratoire dans Azure DevTest Labs. 

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. À partir du menu principal de hello sur le côté gauche de hello, sélectionnez **plus Services** (bas hello de hello liste).

    ![Option de menu Plus de services](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. À partir de la liste de hello des services disponibles, **DevTest Labs**.
1. Sur hello **DevTest Labs** panneau, sélectionnez **ajouter**.
   
    ![Ajouter un laboratoire](./media/devtest-lab-create-lab/add-lab-button.png)

1. Sur hello **créer un laboratoire DevTest** panneau :
   
    1. Entrez un **nom Lab** atelier de nouveau hello.
    2. Sélectionnez hello **abonnement** tooassociate Lab, hello.
    3. Sélectionnez un **emplacement** dans le laboratoire de hello toostore.
    4. Sélectionnez **arrêt automatique** toospecify si vous souhaitez tooenable - et paramètres hello - hello automatique d’arrêt des machines virtuelles de tous les hello lab. fonction d’arrêt automatique Hello est principalement une fonctionnalité de l’enregistrement du coût par laquelle vous pouvez spécifier lorsque vous souhaitez que la machine virtuelle de hello tooautomatically être arrêté. Vous pouvez modifier les paramètres de l’arrêt automatique après avoir créé le laboratoire de hello en suivant les étapes de hello décrites dans l’article hello, [gérer toutes les stratégies pour un atelier de Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    5. Sélectionnez **tooDashboard du code confidentiel** si vous souhaitez un raccourci de tooappear de laboratoire hello sur le tableau de bord de portail hello.
    6. Sélectionnez **options d’automatisation** tooget les modèles Azure Resource Manager pour l’automatisation de la configuration. 
    7. Sélectionnez **Créer**. Après avoir sélectionné **créer**, hello **DevTest Labs** panneau affiche. Vous pouvez surveiller l’état hello du processus de création de laboratoire hello en regardant hello **Notifications** zone. Une fois terminé, actualisez le laboratoire de hello page toosee hello nouvellement créé dans la liste hello des laboratoires.  
    
    ![Créer un panneau de laboratoire](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez créé votre laboratoire, voici quelques tooconsider étapes suivant :

* [Laboratoire tooa de sécuriser l’accès](devtest-lab-add-devtest-user.md).
* [Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md).
* [Créer un modèle de laboratoire](devtest-lab-create-template.md).
* [Créer des artefacts personnalisés pour vos machines virtuelles](devtest-lab-artifact-author.md).
* [Ajouter une machine virtuelle avec lab de tooa artefacts](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).

