---
title: "aaaAdd propriétaires et les utilisateurs dans Azure DevTest Labs | Documents Microsoft"
description: "Ajouter des propriétaires et les utilisateurs dans Azure DevTest Labs, à l’aide de hello portail Azure ou PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Ajouter des propriétaires et des utilisateurs dans Azure DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

L’accès à Azure DevTest Labs est contrôlé par le [contrôle d’accès en fonction du rôle (RBAC) Azure](../active-directory/role-based-access-control-what-is.md). À l’aide de RBAC, vous pouvez séparer les droits au sein de votre équipe dans *rôles* où vous quantité d’allocation uniquement hello d’accès nécessaires toousers tooperform leur travail. Trois de ces rôles RBAC sont *Propriétaire*, *Utilisateur de DevTest Labs* et *Collaborateur*. Dans cet article, vous Découvrez quelles actions peuvent être effectuées dans chacun des trois rôles RBAC principales hello. À partir de là, vous apprendrez comment atelier de tooa tooadd utilisateurs : les deux via hello portail et via un script PowerShell et comment les utilisateurs tooadd à hello niveau d’abonnement.

## <a name="actions-that-can-be-performed-in-each-role"></a>Actions qui peuvent être effectuées dans chaque rôle
Il existe trois rôles principaux que vous pouvez attribuer à un utilisateur :

* Propriétaire
* Utilisateur de DevTest Labs
* Collaborateur

Hello tableau suivant décrit les actions hello qui peuvent être effectuées par les utilisateurs dans chacun de ces rôles :

| **Actions que les utilisateurs dans ce rôle peuvent effectuer** | **Utilisateur de DevTest Labs** | **Propriétaire** | **Collaborateur** |
| --- | --- | --- | --- |
| **Tâches de laboratoire** | | | |
| Ajouter le laboratoire de tooa utilisateurs |Non |Oui |Non |
| Mettre à jour les paramètres de coût |Non |Oui |Oui |
| **Tâches de base de machine virtuelle** | | | |
| Ajouter et supprimer des images personnalisées |Non |Oui |Oui |
| Ajouter, mettre à jour et supprimer des formules |Oui |Oui |Oui |
| Images Place de marché Azure de liste blanche |Non |Oui |Oui |
| **Tâches de machine virtuelle** | | | |
| Créer des machines virtuelles |Oui |Oui |Oui |
| Démarrer, arrêter et supprimer des machines virtuelles |Seuls les ordinateurs virtuels créés par l’utilisateur de hello |Oui |Oui |
| Mettre à jour les stratégies de machine virtuelle |Non |Oui |Oui |
| Ajouter des disques de données à des machines virtuelles ou en supprimer de celles-ci |Seuls les ordinateurs virtuels créés par l’utilisateur de hello |Oui |Oui |
| **Tâches d’artefact** | | | |
| Ajouter et supprimer des référentiels d’artefact |Non |Oui |Oui |
| Appliquer des artefacts |Oui |Oui |Oui |

> [!NOTE]
> Lorsqu’un utilisateur crée une machine virtuelle, cet utilisateur est affecté automatiquement toohello **propriétaire** rôle Hello créé la machine virtuelle.
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>Ajouter un propriétaire ou un utilisateur au niveau de lab hello
Les propriétaires et les utilisateurs peuvent être ajoutés au niveau de lab hello via hello portail Azure. Cela comprend les utilisateurs externes qui disposent d’un [compte Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)valide.
Hello comme suit vous guide tout au long des processus hello d’ajout d’un laboratoire tooa propriétaire ou un utilisateur dans Azure DevTest Labs :

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
3. Dans liste hello labs, sélectionnez lab souhaité de hello.
4. Dans le panneau de hello lab, sélectionnez **Configuration**. 
5. Sur hello **Configuration** panneau, sélectionnez **utilisateurs**.
6. Sur hello **utilisateurs** panneau, sélectionnez **+ ajouter**.
   
    ![Ajouter un utilisateur](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. Sur hello **sélectionner un rôle** panneau, rôle souhaité de hello select. Hello section [les Actions qui peuvent être effectuées dans chaque rôle](#actions-that-can-be-performed-in-each-role) listes hello différentes actions qui peuvent être effectuées par les utilisateurs dans des rôles propriétaire et collaborateur DevTest utilisateur hello.
8. Sur hello **ajouter des utilisateurs** panneau, entrez l’adresse de messagerie hello ou nom d’utilisateur hello tooadd rôle hello spécifié. Si l’utilisateur de hello est introuvable, un message d’erreur explique problème de hello. Si hello utilisateur est trouvé, cet utilisateur est répertorié et sélectionné. 
9. Sélectionnez **Sélectionner**.
10. Sélectionnez **OK** tooclose hello **ajouter un accès** panneau.
11. Lorsque vous retournez toohello **utilisateurs** panneau, hello utilisateur a été ajouté.  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>Ajouter un laboratoire de tooa utilisateur externe à l’aide de PowerShell
En outre les utilisateurs tooadding hello portail Azure, vous pouvez ajouter un laboratoire de tooyour utilisateur externe à l’aide d’un script PowerShell. Bonjour, l’exemple suivant simplement modifier les valeurs de paramètre hello sous hello **toochange de valeurs** commentaire.
Vous pouvez récupérer hello `subscriptionId`, `labResourceGroup`, et `labName` valeurs hello lab du Panneau de hello portail Azure.

> [!NOTE]
> exemple de script Hello suppose que hello spécifié utilisateur a été ajouté comme un toohello invité Active Directory et échoue si ce n’est pas le cas de hello. tooadd un utilisateur n’est pas dans hello lab tooa de Active Directory, utilisez le rôle tooa utilisateur hello tooassign portail Azure hello comme illustré dans la section de hello, [ajouter un propriétaire ou un utilisateur au niveau de lab hello](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>Ajouter un propriétaire ou un utilisateur au niveau d’abonnement hello
Autorisations Azure sont propagées à partir de l’étendue de toochild étendue parente dans Azure. Par conséquent, les propriétaires d’un abonnement Azure qui contient des laboratoires sont automatiquement les propriétaires de ces laboratoires. Ils possèdent également des machines virtuelles de hello et autres ressources créées par les utilisateurs du laboratoire hello et hello service de Azure DevTest Labs. 

Vous pouvez ajouter lab de tooa propriétaire supplémentaire via le panneau de hello lab Bonjour [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Toutefois, hello ajouté l’étendue du propriétaire de l’administration est plus étroite que la portée du propriétaire d’abonnement hello. Par exemple, hello ajoutée propriétaires n’ont pas toosome d’accès complet des ressources hello qui sont créés dans l’abonnement de hello en hello service de DevTest Labs. 

tooadd un tooan propriétaire abonnement Azure, procédez comme suit :

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Sélectionnez **plus Services**, puis sélectionnez **abonnements** à partir de la liste de hello.
3. Sélectionnez l’abonnement de hello souhaité.
4. Sélectionnez l’icône **Accès** . 
   
    ![Accéder aux utilisateurs](./media/devtest-lab-add-devtest-user/access-users.png)
5. Sur hello **utilisateurs** panneau, sélectionnez **ajouter**.
   
    ![Ajouter un utilisateur](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. Sur hello **sélectionner un rôle** panneau, sélectionnez **propriétaire**.
7. Sur hello **ajouter des utilisateurs** panneau, entrez l’adresse de messagerie hello ou le nom d’utilisateur de hello souhaité tooadd en tant que propriétaire. Si l’utilisateur de hello est introuvable, vous obtenez un message d’erreur expliquant le problème de hello. Si l’utilisateur de hello est trouvée, cet utilisateur est répertorié sous hello **utilisateur** zone de texte.
8. Sélectionnez le nom d’utilisateur situé hello.
9. Sélectionnez **Sélectionner**.
10. Sélectionnez **OK** tooclose hello **ajouter un accès** panneau.
11. Lorsque vous retournez toohello **utilisateurs** panneau, utilisateur de hello a été ajouté en tant que propriétaire. Cet utilisateur est désormais un propriétaire de n’importe quel labs créées sous cet abonnement et donc en mesure de tooperform des tâches de propriétaire. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

