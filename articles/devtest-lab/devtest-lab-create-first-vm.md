---
title: "aaaCreate votre première machine virtuelle dans un laboratoire dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment toocreate votre première machine virtuelle dans un laboratoire dans Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a>Créer votre première machine virtuelle dans un laboratoire dans Azure DevTest Labs

Lorsque vous initialement accéder DevTest Labs et toocreate votre première machine virtuelle, vous serez probablement faire à l’aide d’un préchargé [une image marketplace base](devtest-lab-configure-marketplace-images.md). Vous serez également en mesure de toochoose à partir d’un [image personnalisée et une formule](devtest-lab-add-vm.md) lors de la création de plusieurs machines virtuelles. 

Ce didacticiel vous guide à l’aide de hello tooadd portail Azure votre premier atelier tooa de machine virtuelle DevTest Labs.

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a>Les étapes tooadd votre premier atelier tooa de machine virtuelle dans Azure DevTest Labs
1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
1. Dans liste hello labs, sélectionnez lab hello dans lequel vous souhaitez toocreate hello machine virtuelle.  
1. Sur du laboratoire hello **vue d’ensemble** panneau, sélectionnez **+ ajouter**.  

    ![Ajout du bouton de machine virtuelle](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Sur hello **choisir une base** panneau, sélectionnez l’image d’une place de marché pour hello machine virtuelle.
1. Sur hello **virtuels** panneau, entrez un nom pour la machine virtuelle hello Bonjour **nom de machine virtuelle** zone de texte.

    ![Panneau Machine virtuelle de laboratoire](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. Entrez un **nom d’utilisateur** qui dispose des privilèges d’administrateur sur l’ordinateur virtuel de hello.  
1. Entrez un mot de passe dans le champ de texte hello étiqueté **une valeur de Type**.
1. Hello **type de disque de machine virtuelle** détermine le type de disque de stockage est autorisé pour les ordinateurs virtuels de hello dans le laboratoire de hello.
1. Sélectionnez **taille de machine virtuelle** et sélectionnez une des hello prédéfinis des éléments qui spécifient les cœurs de processeur hello, la taille de mémoire RAM et taille du disque dur de hello VM toocreate hello.
1. Sélectionnez **artefacts** - liste hello d’artefacts - sélectionner et configurer les artefacts hello que vous souhaitez l’image de base tooadd toohello.
    **Remarque :** si vous nouveaux laboratoires tooDevTest ou configuration des artefacts, consultez toohello [ajouter un tooa d’artefact existant VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, puis revenez ici une fois.
1. Sélectionnez **créer** tooadd hello spécifié lab toohello de machine virtuelle.

   Panneau de laboratoire Hello affiche hello statut de la création de la machine virtuelle hello - tout d’abord **création**, puis en tant que **en cours d’exécution** après hello machine virtuelle a été démarré.

## <a name="next-steps"></a>Étapes suivantes
* Une fois hello machine virtuelle a été créé, vous pouvez vous connecter toohello machine virtuelle en sélectionnant **Connect** sur le panneau de la machine virtuelle hello.
* Extraire [ajouter un laboratoire tooa de machine virtuelle](devtest-lab-add-vm.md) pour des informations plus complètes sur l’ajout de machines virtuelles suivantes dans votre laboratoire.
* Explorer hello [galerie de modèles de DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).
