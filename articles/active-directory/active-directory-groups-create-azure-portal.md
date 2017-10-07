---
title: "aaaCreate un groupe d’utilisateurs dans Azure Active Directory | Documents Microsoft"
description: Comment toocreate un groupe dans Azure Active Directory et ajouter le groupe de membres toohello
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Créer un groupe et ajouter des membres dans Azure Active Directory
> [!div class="op_single_selector"]
> * [Portail Azure](active-directory-groups-create-azure-portal.md)
> * [Portail Azure Classic](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Cet article explique comment toocreate et remplir un nouveau groupe dans Azure Active Directory. Utilisez une tâche de gestion de tooperform groupe tels que l’attribution des licences ou autorisations nombre tooa d’utilisateurs ou d’appareils à la fois.

## <a name="how-do-i-create-a-group"></a>Comment créer un groupe ?
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **davantage de services**, entrez **utilisateur et les groupes** dans hello de zone de texte, puis sélectionnez **entrée**.

   ![Ouvrir la gestion des utilisateurs](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. Sur hello **utilisateurs et groupes** panneau, sélectionnez **tous les groupes**.

   ![Panneau de groupes hello ouverture](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. Sur hello **utilisateurs et groupes - tous les groupes de** panneau, sélectionnez hello **ajouter** commande.

   ![En sélectionnant Ajouter une commande hello](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. Sur hello **groupe** panneau, ajouter un nom et une description pour le groupe de hello.
6. tooselect membres tooadd toohello groupe, sélectionnez **affecté** Bonjour **type d’appartenance** zone, puis sélectionnez **membres**. Pour plus d’informations sur la façon dont toomanage hello dynamiquement l’appartenance d’un groupe, consultez [à l’aide des attributs toocreate des règles pour l’appartenance au groupe avancées](active-directory-groups-dynamic-membership-azure-portal.md).

   ![Sélection de membres tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. Sur hello **membres** panneau, sélectionnez une ou plus d’utilisateurs ou périphériques tooadd toohello et sélectionnez hello **sélectionnez** bouton bas hello hello panneau tooadd les toohello groupe. Hello **utilisateur** filtres de zone hello affichage en fonction de votre partie de tooany d’entrée d’un nom d’utilisateur ou un périphérique de correspondance. Dans cette zone aucun caractère générique n’est accepté.
8. Lorsque vous avez terminé d’ajouter le groupe de membres toohello, sélectionnez **créer** sur hello **groupe** panneau.    

   ![Confirmation de création du groupe](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>Étapes suivantes
Ces articles fournissent des informations supplémentaires sur Azure Active Directory.

* [Consulter les groupes existants](active-directory-groups-view-azure-portal.md)
* [Gérer les paramètres d’un groupe](active-directory-groups-settings-azure-portal.md)
* [Gérer les membres d’un groupe](active-directory-groups-members-azure-portal.md)
* [Gérer l’appartenance à un groupe](active-directory-groups-membership-azure-portal.md)
* [Gérer les règles dynamiques pour les utilisateurs dans un groupe](active-directory-groups-dynamic-membership-azure-portal.md)
