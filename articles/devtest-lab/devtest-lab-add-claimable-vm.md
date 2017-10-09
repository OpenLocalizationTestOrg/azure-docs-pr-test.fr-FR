---
title: "aaaAdd un laboratoire de tooa de machine virtuelle qui peuvent être réclamé dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment tooadd un laboratoire de tooa qui peuvent être réclamés machine virtuelle dans Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Ajouter un laboratoire tooa de machine virtuelle qui peuvent être réclamé dans Azure DevTest Labs
Vous ajoutez un laboratoire tooa de machine virtuelle qui peuvent être réclamé dans un toohow de manière similaire vous [ajouter une machine virtuelle standard](devtest-lab-add-vm.md) – dans un *base* qui est soit un [image personnalisée](devtest-lab-create-template.md), [formule](devtest-lab-manage-formulas.md), ou [une image Marketplace](devtest-lab-configure-marketplace-images.md). Ce didacticiel vous guide à l’aide de hello tooadd portail Azure un laboratoire de tooa de machine virtuelle qui peuvent être réclamé dans DevTest Labs et présente le processus de hello qu'un utilisateur suit tooclaim hello machine virtuelle.

> [!NOTE]
> Si vous déployez des ordinateurs virtuels de lab via [modèles Azure Resource Manager](devtest-lab-create-environment-from-arm.md), vous pouvez créer des machines virtuelles qui peuvent être réclamés en définissant un hello **allowClaim** tootrue de propriété dans la section des propriétés hello.
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Étapes tooadd un laboratoire de tooa de machine virtuelle qui peuvent être réclamé dans Azure DevTest Labs
1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
1. À partir de la liste hello de labs, sélectionnez le laboratoire de hello dans lequel vous voulez toocreate hello qui peuvent être réclamé machine virtuelle.  
1. Sur du laboratoire hello **vue d’ensemble** panneau, sélectionnez **+ ajouter**.  

    ![Ajout du bouton de machine virtuelle](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Sur hello **choisir une base** panneau, sélectionnez une base de hello machine virtuelle.
1. Sur hello **virtuels** panneau, entrez un nom pour la machine virtuelle hello Bonjour **nom de machine virtuelle** zone de texte.

    ![Panneau Machine virtuelle de laboratoire](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Entrez un **nom d’utilisateur** qui dispose des privilèges d’administrateur sur l’ordinateur virtuel de hello.  
1. Si vous voulez toouse un mot de passe stockés dans votre [magasin des secrets](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), sélectionnez **utiliser une clé secrète enregistrée**et spécifiez une valeur clée correspondant tooyour secret (mot de passe). Dans le cas contraire, entrez un mot de passe dans le champ de texte hello étiqueté **une valeur de Type**.
1. Hello **type de disque de machine virtuelle** détermine le type de disque de stockage est autorisé pour les ordinateurs virtuels de hello dans le laboratoire de hello.
1. Sélectionnez **taille de machine virtuelle** et sélectionnez une des hello prédéfinis des éléments qui spécifient les cœurs de processeur hello, la taille de mémoire RAM et taille du disque dur de hello VM toocreate hello.
1. Sélectionnez **artefacts** liste hello des artefacts, sélectionner et configurer les artefacts hello que vous souhaitez l’image de base tooadd toohello. Si vous les nouveaux laboratoires tooDevTest ou configuration des artefacts, consultez toohello [ajouter un tooa d’artefact existant VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, puis revenez ici une fois.
1. Sélectionnez **paramètres avancés** options d’expiration et les options de réseau de tooconfigure hello machine virtuelle. Sous **revendication options**, choisissez **Oui** machine de hello toomake qui peuvent être réclamé.

  ![Choisissez toomake hello qui peuvent être réclamé machine virtuelle.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. Si vous souhaitez tooview ou copiez le modèle de hello Azure Resource Manager, consultez toohello [modèle Enregistrer Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) section et revenez ici une fois.
1. Sélectionnez **créer** tooadd hello spécifié lab toohello de machine virtuelle.
1. Panneau de laboratoire Hello affiche hello statut de la création de la machine virtuelle hello - tout d’abord **création**, puis en tant que **en cours d’exécution** après hello machine virtuelle a été démarré.


## <a name="using-a-claimable-vm"></a>Utilisation d’une machine virtuelle exigible

Un utilisateur peut demander toutes les machines virtuelles à partir de la liste hello de « Ordinateurs virtuels qui peuvent être réclamés » en effectuant l’une de ces étapes :

* À partir de la liste de hello des « Ordinateurs virtuels qui peuvent être réclamés » en bas de hello du Panneau de vue d’ensemble du laboratoire hello, avec le bouton droit sur l’un des hello machines virtuelles dans la liste de hello et choisissez **machine de revendication**.

 ![Demandez une machine virtuelle exigible spécifique.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* En haut de hello Hello **vue d’ensemble** panneau, choisissez **demander une**. Un ordinateur virtuel aléatoire est attribué à partir de la liste de hello de machines virtuelles qui peuvent être réclamés.

 ![Demandez n’importe quelle machine virtuelle exigible.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


Une fois que l’utilisateur revendique une machine virtuelle, cette dernière est placée dans la liste « Mes machines virtuelles » et n’est plus exigible par un autre utilisateur.

## <a name="next-steps"></a>Étapes suivantes
* Une fois hello machine virtuelle a été créé, vous pouvez vous connecter toohello machine virtuelle en sélectionnant **Connect** sur le panneau de la machine virtuelle hello.
* Explorer hello [galerie de modèles de DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)
