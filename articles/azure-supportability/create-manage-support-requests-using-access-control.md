---
title: "toocontrol de contrôle d’accès en fonction du rôle (RBAC) aaaAzure toocreate de droits d’accès et de gérer les demandes de prise en charge | Documents Microsoft"
description: "Azure toocontrol de contrôle d’accès en fonction du rôle (RBAC) toocreate de droits d’accès et de gérer les demandes de prise en charge"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a>Azure toocontrol de contrôle d’accès en fonction du rôle (RBAC) toocreate de droits d’accès et de gérer les demandes de prise en charge

Le [contrôle d’accès en fonction du rôle (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) permet une gestion précise de l’accès pour Azure.
Prend en charge la création de demande dans le portail Azure, de hello [portal.azure.com](https://portal.azure.com), utilise toodefine de modèle RBAC de Azure qui peut créer et gérer les demandes de prise en charge.
L’accès est accordé en assignant hello toousers du rôle RBAC appropriés, les groupes et les applications à une certaine étendue, qui peut être un abonnement, groupe de ressources ou une ressource.

Prenons un exemple : en tant que propriétaire d’un groupe de ressources avec des autorisations de lecture au niveau de l’étendue de l’abonnement hello, vous pouvez gérer toutes les ressources hello sous le groupe de ressources hello, telles que les sites Web, des ordinateurs virtuels et des sous-réseaux.
Toutefois, lorsque vous essayez de toocreate une demande de support par rapport à la ressource d’ordinateur virtuel hello, vous rencontrez hello l’erreur suivante

![Erreur relative à l’abonnement](./media/create-manage-support-requests-using-access-control/subscription-error.png)

Dans la gestion des demandes de prise en charge, vous devez écrire d’autorisation ou un rôle qui a hello prennent en charge l’action Microsoft.Support/* à hello abonnement étendue toobe en mesure de toocreate et gérer les demandes de prise en charge.

Bonjour à l’article suivant explique comment vous pouvez utiliser toocreate de contrôle d’accès en fonction du rôle (RBAC) de Azure personnalisée et gérer les demandes de prise en charge dans hello portail Azure.

## <a name="getting-started"></a>Mise en route

À l’aide d’exemple hello ci-dessus, vous serez en mesure de toocreate une demande de support pour votre ressource si vous ont été affectés à un rôle RBAC personnalisé sur l’abonnement de hello par le propriétaire de l’abonnement hello.
[Des rôles personnalisés RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) peuvent être créés à l’aide d’Azure PowerShell et hello API REST Azure Interface de ligne de commande (CLI).

propriété d’actions Hello d’un rôle personnalisé spécifie hello opérations Azure toowhich hello rôle accorde un accès.
toocreate un rôle personnalisé pour la gestion des demandes de prise en charge, hello rôle doit disposer d’action de hello Microsoft.Support/*

Voici un exemple d’un rôle personnalisé, vous pouvez utiliser toocreate et gérer prennent en charge des demandes.
Nous avons nommé ce rôle « Contributeur de demande de prise en charge » et qui est la façon dont nous nous référons toohello le rôle personnalisé dans cet article.

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

Suivez les étapes de hello décrites dans [cette vidéo](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn comment toocreate un rôle personnalisé pour votre abonnement.

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a>Créer et gérer des demandes de support Bonjour portail Azure

Prenons un exemple : vous êtes propriétaire hello d’abonnement « Visual Studio abonnement MSDN. »
Joe est votre homologue qui est un toosome de propriétaire de la ressource de groupes de ressources de hello dans cet abonnement et a lu l’abonnement de toohello d’autorisation.
Vous souhaitez toogive accès tooyour homologue, Joe, hello capacité toocreate et gérez les tickets de prise en charge pour les ressources hello sous cet abonnement.

1. première étape de Hello est toogo toohello abonnement et sous « Paramètres », vous voyez une liste d’utilisateurs. Cliquez sur l’utilisateur hello Joe qui a accès en lecture sur hello abonnement et nous allons affecter un nouveau toohim de rôle personnalisé.

    ![Ajouter un rôle](./media/create-manage-support-requests-using-access-control/add-role.png)

2. Cliquez sur « Ajouter » sous le panneau des « Utilisateurs » hello. Sélectionnez le rôle de personnalisé de hello « Contributeur de demande de prise en charge » à partir de la liste de hello des rôles

    ![Ajouter le rôle Collaborateur du support](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. Après avoir sélectionné le nom de rôle hello, cliquez sur « Ajouter des utilisateurs » et entrez les informations d’identification de la messagerie de Jacques hello. Cliquez sur « Sélectionner ».

    ![Ajouter des utilisateurs](./media/create-manage-support-requests-using-access-control/add-users.png)

4. Cliquez sur « Ok » tooproceed

    ![Ajout d'accès](./media/create-manage-support-requests-using-access-control/add-access.png)

5. Vous voyez à présent utilisateur hello avec rôle personnalisé nouvellement ajoutée « Prise en charge de demande contributeur » sous abonnement hello dont vous êtes propriétaire de hello hello

    ![Utilisateur ajouté](./media/create-manage-support-requests-using-access-control/user-added.png)

    Lorsque Joe s’ouvre dans le portail de hello, il voit toowhich d’abonnement hello qu’il a été ajouté.

7. Jean clique sur « Nouvelle demande de Support » à partir du Panneau de « Aide et prise en charge » hello et créer des demandes de prise en charge pour « Visual Studio Ultimate avec MSDN »

    ![Nouvelle demande de support](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. Cliquant sur « Tous en charge les demandes » Joe peut afficher hello liste de demandes de support créé pour cet abonnement ![cas afficher les détails](./media/create-manage-support-requests-using-access-control/case-details-view.png)

## <a name="remove-support-request-access-in-hello-azure-portal"></a>Supprimer l’accès de demande de prise en charge dans hello portail Azure

Comme il est possible de toogrant accès tooa utilisateur toocreate et gérer les demandes de prise en charge, il est tooremove possible l’accès pour l’utilisateur hello ainsi.
tooremove hello toocreate de capacité et gérer les demandes de prise en charge, accédez toohello abonnement, cliquez sur « Paramètres » puis cliquez sur utilisateur hello (dans ce cas, Joe).
Cliquez sur le nom de rôle hello, « Prise en charge de demande contributeur » et cliquez sur « Supprimer »

![Supprimer l’accès aux demandes de support](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

Lorsque Joe toohello portail se connecte et tente de toocreate une demande de support, il rencontre hello l’erreur suivante

![Erreur relative à l’abonnement-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

Jean ne peut pas voir les demandes de support lorsqu’il clique sur « All support requests » (Toutes les demandes de support).

![Vue Détails des cas-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
