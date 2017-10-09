---
title: "Contrôle d’accès basé sur les aaaRole Bonjour portail Azure | Documents Microsoft"
description: "Prise en main de la gestion de l’accès en fonction du rôle hello Azure Portal de contrôle d’accès. Utiliser les ressources de rôle affectations tooassign autorisations tooyour."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a>Utiliser les ressources de contrôle d’accès en fonction du rôle toomanage accès tooyour abonnement Azure
> [!div class="op_single_selector"]
> * [Gérer l’accès par utilisateur ou par groupe](role-based-access-control-manage-assignments.md)
> * [Gérer l’accès par ressource](role-based-access-control-configure.md)

Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour Azure. À l’aide de RBAC, vous pouvez accorder uniquement les quantité hello d’accès que les utilisateurs doivent tooperform leur travail. Cet article vous aidera à obtenir en cours d’exécution avec RBAC Bonjour portail Azure. Si vous souhaitez plus d’informations sur la gestion des droits d’accès avec RBAC, consultez [Prise en main de la gestion des accès dans le portail Azure](role-based-access-control-what-is.md).

Dans chaque abonnement, vous pouvez accorder des attributions de rôles too2000. 

## <a name="view-access"></a>Voir l’accès
Vous pouvez voir qui a accès tooa ressource, un groupe de ressources ou abonnement depuis son panneau principal Bonjour [portail Azure](https://portal.azure.com). Par exemple, nous souhaitons toosee ayant tooone accès notre des groupes de ressources :

1. Sélectionnez **groupes de ressources** dans la barre de navigation hello sur hello gauche.  
    ![Groupes de ressources - icône](./media/role-based-access-control-configure/resourcegroups_icon.png)
2. Nom hello sélectionnez hello du groupe de ressources à partir de hello **groupes de ressources** panneau.
3. Sélectionnez **(IAM) de contrôle d’accès** à partir du menu de gauche hello.  
4. Panneau de contrôle d’accès Hello répertorie tous les utilisateurs, les groupes et les applications qui ont été accordées à groupe de ressources toohello accès.  
   
    ![Panneau Utilisateurs - comparaison Accès hérité et accès affecté (capture d’écran)](./media/role-based-access-control-configure/view-access.png)

Notez que certains rôles sont trop limitées**cette ressource** tandis que d’autres sont **Inherited** à partir d’une autre étendue. L’accès est attribué spécifiquement le groupe de ressources toohello ou hérité d’un abonnement de parent toohello affectation.

> [!NOTE]
> Les administrateurs d’abonnements classique et coadministrateurs sont considérés comme des propriétaires d’abonnement de hello dans le nouveau modèle RBAC hello.

## <a name="add-access"></a>Ajout d’un accès
Vous accordez l’accès à partir de hello ressource, un groupe de ressources ou abonnement est étendue hello d’attribution de rôle hello.

1. Sélectionnez **ajouter** sur le panneau de contrôle d’accès hello.  
2. Rôle hello SELECT que vous souhaitez tooassign de hello **sélectionner un rôle** panneau.
3. Sélectionnez hello utilisateur, groupe ou application dans le répertoire que vous souhaitez accéder toogrant à. Vous pouvez rechercher le répertoire hello avec des noms complets, les adresses de messagerie et les identificateurs d’objet.  
   
    ![Panneau Ajouter des utilisateurs - rechercher (capture d’écran)](./media/role-based-access-control-configure/grant-access2.png)
4. Sélectionnez **OK** toocreate l’attribution hello. Hello **Ajout utilisateur** popup hello de progression.  
    ![Barre de progression Ajout d’utilisateur - capture d’écran](./media/role-based-access-control-configure/addinguser_popup.png)

Après avoir ajouté avec succès une attribution de rôle, il apparaîtra sur hello **utilisateurs** panneau.

## <a name="remove-access"></a>Supprimer un accès
1. Pointez votre curseur sur nom hello d’assignation hello que vous souhaitez tooremove. Une case à cocher s’affiche le nom de toohello suivant.
2. Utilisez tooselect de cases à cocher hello une ou plusieurs attributions de rôle.
2. Sélectionnez **Supprimer**.  
3. Sélectionnez **Oui** la suppression de tooconfirm hello.

Les attributions héritées ne peuvent pas être supprimées. Si vous devez tooremove une affectation héritée, vous devez toodo à hello étendue où l’attribution de rôle hello a été créée. Bonjour **étendue** colonne, en regard trop**Inherited** il existe un lien qui vous toohello ressources où ce rôle a été attribué. Accédez ressource toohello figure attribution de rôle tooremove hello.

![Panneau Utilisateurs - l’accès hérité désactive le bouton (capture d’écran)](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a>Accès toomanage des autres outils
Vous pouvez attribuer des rôles et gérer l’accès avec les commandes Azure RBAC dans outils autres que hello portail Azure.  Suivez les toolearn de liens hello plus d’informations sur les conditions préalables de hello et prise en main avec les commandes de Azure RBAC hello.

* [Azure PowerShell](role-based-access-control-manage-access-powershell.md)
* [Interface de ligne de commande Azure](role-based-access-control-manage-access-azure-cli.md)
* [API REST](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a>Étapes suivantes
* [Créer un rapport d’historique des modifications d’accès](role-based-access-control-access-change-history-report.md)
* Consultez hello [rôles intégrés RBAC](role-based-access-built-in-roles.md)
* Définissez vos propres [rôles personnalisés dans Azure RBAC](role-based-access-control-custom-roles.md)

