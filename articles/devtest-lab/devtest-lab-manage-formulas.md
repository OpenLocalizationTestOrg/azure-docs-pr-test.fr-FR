---
title: formules aaaManage dans Azure DevTest Labs toocreate machines virtuelles | Documents Microsoft
description: "Découvrez comment tooupdate et supprimez les formules Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a>Gérer les formules Azure DevTest Labs

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

Cet article explique comment toocreate une formule à partir d’une base (image personnalisée, une image Marketplace ou un autre formule) ou sur une machine virtuelle existante. Cet article vous guide aussi dans la gestion des formules existantes.

## <a name="create-a-formula"></a>Créer une formule
Toute personne ayant DevTest Labs *utilisateurs* autorisations est VMs toocreate en mesure d’à l’aide d’une formule comme base. Il existe deux façons de toocreate formules : 

* À partir d’une base - Utilisez toodefine toutes les caractéristiques de hello de formule de hello.
* À partir d’un laboratoire existant VM - à utiliser toocreate une formule en fonction des paramètres de hello d’une machine virtuelle existante.

Pour plus d’informations sur l’ajout des utilisateurs et des autorisations, consultez [Ajouter des propriétaires et des utilisateurs dans Azure DevTest Labs](./devtest-lab-add-devtest-user.md).

### <a name="create-a-formula-from-a-base"></a>Créer une formule à partir d’une base
Hello comme suit vous guide tout au long des processus hello de création d’une formule à partir d’une image personnalisée, une image Marketplace ou une autre formule.

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

2. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.

3. Dans liste hello labs, sélectionnez lab souhaité de hello.  

4. Dans le panneau de hello lab, sélectionnez **formules (réutilisables bases)**.
   
    ![Menu de formule](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. Sur hello **formules** panneau, sélectionnez **+ ajouter**.
   
    ![Ajouter une formule](./media/devtest-lab-create-formulas/add-formula.png)

6. Sur hello **choisir une base** panneau, base hello select (image personnalisée, une image Marketplace ou formule) à partir de laquelle vous souhaitez que la formule de hello de toocreate.
   
    ![Liste de base](./media/devtest-lab-create-formulas/base-list.png)

7. Sur hello **créer formule** panneau, spécifiez hello valeurs suivantes :
   
    * **Nom de la formule** : entrez un nom pour votre formule. Cette valeur est affichée dans la liste hello des images de base lorsque vous créez une machine virtuelle. nom de Hello est validé comme vous le tapez, et si elle est non valide, un message indique exigences hello d’un nom valide.
    * **Description** : entrez une description significative pour votre formule. Cette valeur est disponible à partir du menu contextuel de la formule hello lorsque vous créez une machine virtuelle.
    * **Nom d’utilisateur** - Entrez un nom d’utilisateur qui obtient les privilèges d’administrateur.
    * **Mot de passe** - Entrez - ou sélectionnez dans la liste déroulante de hello - une valeur qui est associée à hello mot de passe que vous souhaitez toouse pour l’utilisateur spécifié de hello. Pour plus d’informations sur les secrets hello, consultez [Azure DevTest Labs : magasin des secrets personnel](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).
    * **Type de disque de machine virtuelle** - spécifier un disque dur (lecteur de disque dur) ou tooindicate SSD (disque SSD) type de disque de stockage est autorisée pour les ordinateurs virtuels de hello configurés à l’aide de cette image de base.
    * ** De machine virtuelle taille ** : sélectionnez un des éléments de hello prédéfini qui spécifient les hello cœurs de processeur, mémoire RAM et taille du disque dur de hello VM toocreate hello. 
    * **Artefacts** -tooopen sélectionnez hello **ajouter des artefacts** panneau, dans lequel vous sélectionnez et configurez les artefacts hello que vous souhaitez l’image de base tooadd toohello. Pour plus d’informations sur les artefacts, consultez [Gérer les artefacts de machine virtuelle dans Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).
    * **Paramètres avancés** -tooopen sélectionnez hello **avancé** panneau où vous configurez hello suivant les paramètres :
        * **Réseau virtuel** -spécifiez hello souhaité de réseau virtuel.
        * **Sous-réseau** -spécifiez le sous-réseau de hello souhaité.    
        * **Configuration d’adresse IP** -Spécifie que les adresses publiques, privées ou IP partagé hello. Pour plus d’informations sur les adresses IP partagées, consultez [Comprendre les adresses IP partagées dans Azure DevTest Labs](./devtest-lab-shared-ip.md).
        * **Rendre cet ordinateur qui peuvent être réclamés** -effectue une machine « qui peuvent être réclamés » signifie qu’il ne sera pas attribué la propriété au moment de la création de hello. Au lieu de cela, les utilisateurs du laboratoire sera machine de hello tootake en mesure de la propriété (« revendications ») dans le panneau de laboratoire hello.     
    * **Image** -ce champ affiche le nom de l’image de base hello sélectionnée sur le panneau précédent de hello. 
     
       ![Créer une formule](./media/devtest-lab-create-formulas/create-formula.png)

8. Sélectionnez **créer** formule de hello toocreate.

9. Lors de la formule de hello a été créé, il s’affiche dans la liste hello sur hello **formules** panneau.

### <a name="create-a-formula-from-a-vm"></a>Créer une formule depuis une machine virtuelle
Hello étapes suivantes vous guident hello de création d’une formule basée sur une machine virtuelle existante. 

> [!NOTE]
> toocreate une formule d’une machine virtuelle, hello machine virtuelle doit avoir été créé après le 30 mars 2016. 
> 
> 

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
3. Dans liste hello labs, sélectionnez lab souhaité de hello.  
4. Sur du laboratoire hello **vue d’ensemble** panneau, VM hello select à partir de laquelle vous souhaitez formule de hello toocreate.
   
    ![Machines virtuelles de labo](./media/devtest-lab-create-formulas/my-vms.png)
5. Dans le panneau de la machine virtuelle de hello, sélectionnez **créer la formule (base réutilisable)**.
   
    ![Créer une formule](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. Sur hello **créer formule** panneau, entrez un **nom** et **Description** pour votre nouvelle formule.
   
    ![Panneau Créer une formule](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. Sélectionnez **OK** formule de hello toocreate.

## <a name="modify-a-formula"></a>Modifier une formule
toomodify une formule, procédez comme suit :

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
3. Dans liste hello labs, sélectionnez lab souhaité de hello.  
4. Dans le panneau de hello lab, sélectionnez **formules (réutilisables bases)**.
   
    ![Menu de formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Sur hello **les formules Lab** panneau, formule Sélectionnez hello toomodify vous le souhaitez.
6. Sur hello **mise à jour de la formule** panneau, apporter des modifications de hello souhaité, puis sélectionnez **mise à jour**.

## <a name="delete-a-formula"></a>Supprimer une formule
toodelete une formule, procédez comme suit :

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
3. Dans liste hello labs, sélectionnez lab souhaité de hello.  
4. Atelier de hello **paramètres** panneau, sélectionnez **formules**.
   
    ![Menu de formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Sur hello **les formules Lab** panneau, sélectionnez hello des toohello de points de suspension à droite de la formule de hello vous souhaitez toodelete.
   
    ![Menu de formule](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. Dans le menu contextuel de la formule hello, sélectionnez **supprimer**.
   
    ![Menu contextuel de la formule](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. Sélectionnez **Oui** toohello la boîte de dialogue de la confirmation de suppression.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Billets de blog connexes
* [Images personnalisées ou formules ?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez créé une formule à utiliser lors de la création d’une machine virtuelle, étape suivante de hello est trop[ajouter un laboratoire tooyour de machine virtuelle](devtest-lab-add-vm-with-artifacts.md).

