---
title: aaaAdd un laboratoire tooa de machine virtuelle dans Azure DevTest Labs | Documents Microsoft
description: "Découvrez comment tooadd un laboratoire tooa de machine virtuelle dans Azure DevTest Labs"
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
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a>Ajouter un laboratoire tooa de machine virtuelle dans Azure DevTest Labs
Si vous avez déjà [créé votre première machine virtuelle](devtest-lab-create-first-vm.md), vous l’avez probablement fait à partir d’une [image de la Place de marché](devtest-lab-configure-marketplace-images.md) préchargée. Maintenant, si vous souhaitez tooadd ultérieures machines virtuelles tooyour lab, vous pouvez également choisir une *base* qui est soit un [image personnalisée](devtest-lab-create-template.md) ou un [formule](devtest-lab-manage-formulas.md). Ce didacticiel vous guide tout au long de l’utilisation de hello tooadd portail Azure un laboratoire tooa de machine virtuelle dans DevTest Labs.

Cet article vous montre également comment toomanage hello artefacts pour une machine virtuelle dans votre laboratoire.

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a>Étapes tooadd un laboratoire tooa de machine virtuelle dans Azure DevTest Labs
1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
1. Dans liste hello labs, sélectionnez lab hello dans lequel vous souhaitez toocreate hello machine virtuelle.  
1. Sur du laboratoire hello **vue d’ensemble** panneau, sélectionnez **+ ajouter**.  

    ![Ajout du bouton de machine virtuelle](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Sur hello **choisir une base** panneau, sélectionnez une base de hello machine virtuelle.
1. Sur hello **virtuels** panneau, entrez un nom pour la machine virtuelle hello Bonjour **nom de machine virtuelle** zone de texte.

    ![Panneau Machine virtuelle de laboratoire](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Entrez un **nom d’utilisateur** qui dispose des privilèges d’administrateur sur l’ordinateur virtuel de hello.  
1. Si vous voulez toouse un mot de passe stockés dans votre [magasin des secrets](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), sélectionnez **utiliser une clé secrète enregistrée**et spécifiez une valeur clée correspondant tooyour secret (mot de passe). Dans le cas contraire, entrez un mot de passe dans le champ de texte hello étiqueté **une valeur de Type**.
1. Hello **type de disque de machine virtuelle** détermine le type de disque de stockage est autorisé pour les ordinateurs virtuels de hello dans le laboratoire de hello.
1. Sélectionnez **taille de machine virtuelle** et sélectionnez une des hello prédéfinis des éléments qui spécifient les cœurs de processeur hello, la taille de mémoire RAM et taille du disque dur de hello VM toocreate hello.
1. Sélectionnez **artefacts** - liste hello d’artefacts - sélectionner et configurer les artefacts hello que vous souhaitez l’image de base tooadd toohello.
    **Remarque :** si vous nouveaux laboratoires tooDevTest ou configuration des artefacts, consultez toohello [ajouter un tooa d’artefact existant VM](#add-an-existing-artifact-to-a-vm) section, puis revenez ici une fois.
1. Sélectionnez **paramètres avancés** options d’expiration et les options de réseau de tooconfigure hello machine virtuelle. 

   tooset une option d’expiration, choisissez toospecify d’icône de calendrier hello une date sur laquelle hello machine virtuelle est automatiquement supprimée.  Par défaut, hello VM n’expirera jamais. 
1. Si vous souhaitez tooview ou copiez le modèle de hello Azure Resource Manager, consultez toohello [modèle Enregistrer Azure Resource Manager](#save-azure-resource-manager-template) section et revenez ici une fois.
1. Sélectionnez **créer** tooadd hello spécifié lab toohello de machine virtuelle.
1. Panneau de laboratoire Hello affiche hello statut de la création de la machine virtuelle hello - tout d’abord **création**, puis en tant que **en cours d’exécution** après hello machine virtuelle a été démarré.

> [!NOTE]
> [Ajouter une machine virtuelle qui peuvent être réclamée](devtest-lab-add-claimable-vm.md) vous montre comment toomake hello des ordinateurs virtuels qui peuvent être réclamés afin qu’il soit disponible pour une utilisation par un utilisateur dans le laboratoire de hello.
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a>Ajouter un tooa d’artefact existant machine virtuelle
Au cours de la création d’une machine virtuelle, vous pouvez ajouter des artefacts existants. Chaque laboratoire comprend des artefacts à partir de hello publique référentiel d’artefacts DevTest Labs, ainsi que les artefacts que vous avez créé et ajouté tooyour propre référentiel d’artefacts.

* Azure DevTest Labs *artefacts* vous permettent de spécifier *actions* qui sont effectuées lors de la configuration de hello machine virtuelle, par exemple en cours d’exécution de scripts Windows PowerShell, l’exécution des commandes de l’interpréteur de commandes et installation du logiciel.
* Artefact *paramètres* vous permettent de personnaliser l’artefact hello pour votre scénario particulier

toodiscover toocreate artefacts, voir hello article, [Apprenez tooauthor vos propres artefacts pour utilisent avec DevTest Labs](devtest-lab-artifact-author.md).

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
1. Dans liste hello labs, sélectionnez lab hello contenant VM hello avec laquelle vous souhaitez toowork.  
1. Sélectionnez **Mes machines virtuelles**.
1. Sélectionnez hello souhaité de machine virtuelle.
1. Sélectionnez **Artefacts**. 
1. Sélectionnez **Appliquer des artefacts**.
1. Sur hello **appliquer les artefacts** panneau, artefact hello sélectionnez vous souhaitez tooadd toohello machine virtuelle.
1. Sur hello **ajouter artefact** panneau, entrez les valeurs de paramètre hello requis et tous les paramètres facultatifs que vous avez besoin.  
1. Sélectionnez **ajouter** tooadd hello artefact et retourner les toohello **appliquer les artefacts** panneau.
1. Continuez à ajouter des artefacts en fonction des besoins de votre machine virtuelle.
1. Une fois que vous avez ajouté vos artefacts, vous pouvez [modifier ordre hello dans le hello artefacts sont exécutés](#change-the-order-in-which-artifacts-are-run). Vous pouvez également revenir en arrière trop[afficher ou modifier un artefact](#view-or-modify-an-artifact).
1. Lorsque vous avez terminé d’ajouter des artefacts, sélectionnez **Appliquer**.

## <a name="change-hello-order-in-which-artifacts-are-run"></a>Modifier l’ordre hello dans lequel sont exécutés les artefacts
Par défaut, les actions de hello d’artefacts de hello sont exécutées dans l’ordre de hello dans lequel ils sont ajoutés toohello machine virtuelle. Hello étapes suivantes illustrent comment toochange hello ordre les Bonjour artefacts sont exécutés.

1. En haut de hello Hello **appliquer les artefacts** panneau, lien hello sélectionnez indiquant le nombre de hello d’artefacts qui ont été ajoutés toohello machine virtuelle.
   
    ![Nombre d’artefacts ajouté tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Sur hello **sélectionné les artefacts** panneau, glisser -déplacer des artefacts de hello en hello souhaité ordre. **Remarque :** si vous avez des difficultés à faire glisser les artefacts hello, assurez-vous que vous faites glisser à partir de hello à gauche de l’artefact de hello. 
1. Cliquez sur **OK** quand vous avez terminé.  

## <a name="view-or-modify-an-artifact"></a>Afficher ou modifier un artefact
Hello étapes suivantes illustrent comment tooview ou modifier les paramètres de hello d’un artefact :

1. En haut de hello Hello **appliquer les artefacts** panneau, lien hello sélectionnez indiquant le nombre de hello d’artefacts qui ont été ajoutés toohello machine virtuelle.
   
    ![Nombre d’artefacts ajouté tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Sur hello **sélectionné les artefacts** panneau, artefact hello select que vous souhaitez tooview ou modifiez.  
1. Sur hello **ajouter artefact** panneau, assurez-vous que les modifications nécessaires, puis sélectionnez **OK** tooclose hello **ajouter artefact** panneau.
1. Sélectionnez **OK** tooclose hello **sélectionné les artefacts** panneau.

## <a name="save-azure-resource-manager-template"></a>Enregistrer un modèle Azure Resource Manager
Un modèle Azure Resource Manager fournit un toodefine de façon déclarative un déploiement reproductible. Hello suit explique comment toosave hello modèle Azure Resource Manager pour hello machine virtuelle en cours de création.
Une fois enregistré, vous pouvez utiliser un modèle de gestionnaire de ressources Azure hello trop[déployer de nouvelles machines virtuelles avec Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).

1. Sur hello **virtuels** panneau, sélectionnez **afficher le modèle ARM**.
2. Sur hello **modèle vue Azure Resource Manager** panneau, sélectionnez hello modèle du texte.
3. Copiez le Presse-papiers de toohello hello texte sélectionné.
4. Sélectionnez **OK** tooclose hello **Panneau de modèle de vue Azure Resource Manager**.
5. Ouvrez un éditeur de texte.
6. Collez le texte hello du modèle à partir du Presse-papiers de hello.
7. Enregistrez le fichier hello pour une utilisation ultérieure.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Étapes suivantes
* Une fois hello machine virtuelle a été créé, vous pouvez vous connecter toohello machine virtuelle en sélectionnant **Connect** sur le panneau de la machine virtuelle hello.
* Découvrez comment trop[créer des artefacts personnalisés pour votre machine de virtuelle DevTest Labs](devtest-lab-artifact-author.md).
* Explorer hello [galerie de modèles de DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
