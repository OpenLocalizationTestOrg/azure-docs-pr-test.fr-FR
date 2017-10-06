---
title: "aaaHow toogive accès tooPrivileged Identity Management - Azure | Documents Microsoft"
description: "Découvrez comment toousers de rôles tooadd avec hello extension d’Azure Active Directory Privileged Identity Management afin de pouvoir gérer PIM."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a>En donnant accès toomanage Azure AD Privileged Identity Management
administrateur général de Hello qui permet à Azure AD Privileged Identity Management (PIM) pour une organisation automatiquement les attributions de rôle et accédez aux tooPIM. Aucune autre personne ne dispose d’un accès en écriture par défaut, y compris les autres administrateurs généraux. Autres administrateurs globaux, les administrateurs de sécurité et les lecteurs de sécurité ont accès en lecture seule tooAzure AD PIM. toogive accès tooPIM, hello premier utilisateur peut assigner à d’autres toohello **administrateur du rôle privilégié** rôle. Cette affectation doit être effectuée depuis PIM proprement dit et ne peut pas être modifiée via PowerShell ou d’autres portails.

> [!NOTE]
> La gestion d’Azure AD PIM requiert l’authentification Azure MFA. Les comptes Microsoft ne pouvant pas s’inscrire pour l’authentification Azure MFA, un utilisateur qui se connecte avec un compte Microsoft ne peut pas accéder à Azure AD PIM.
> 
> 

Vérifiez qu’il y a toujours au moins deux utilisateurs dans un rôle d’administrateur de rôle privilégié, au cas où un utilisateur serait verrouillé ou son compte supprimé.

## <a name="give-another-user-access-toomanage-pim"></a>Permettre à un autre utilisateur de l’accès toomanage PIM
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) et sélectionnez hello **Azure AD Privileged Identity Management** application sur le tableau de bord hello.
2. Sélectionnez **Gérer les rôles privilégiés** > **Administrateur de rôle privilégié** > **Ajouter**.
   
    ![Ajout d’administrateur de rôle privilégié - capture d’écran][1]
3. Sur le panneau de hello ajouter les utilisateurs gérés, l’étape 1 est déjà terminée. L’étape 2, sélectionnez **sélectionnez utilisateurs** et de recherche pour l’utilisateur de hello souhaité tooadd.
   
    ![Sélection des utilisateurs - capture d’écran][2]
4. Sélectionnez un utilisateur de hello hello résultats de recherche, puis cliquez sur **fait**.
5. Cliquez sur **OK** toosave votre sélection. utilisateur Hello que vous avez sélectionné s’affiche dans la liste hello des administrateurs de rôle privilégié.
   
   * Chaque fois que vous affectez une nouvelle toosomeone de rôle, ils sont automatiquement configurés en tant que rôle de hello tooactivate éligible. Si vous souhaitez toomake permanentes dans le rôle de hello, cliquez sur utilisateur hello dans la liste de hello. Sélectionnez **rendre l’autorisation** dans le menu d’informations utilisateur hello.
6. Envoyer à un lien utilisateur de hello trop[prise en main d’Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).

## <a name="remove-another-users-access-rights-for-managing-pim"></a>Supprimez les droits d'accès d'un autre utilisateur pour la gestion de PIM
Avant de supprimer un utilisateur du rôle d’administrateur hello rôle privilégié, assurez-vous toujours qu’il y aura toujours deux utilisateurs affectés tooit.

1. Dans le tableau de bord PIM hello, cliquez sur le rôle de hello **administrateur du rôle privilégié**.  liste Hello d’utilisateurs actuellement dans ce rôle s’affiche.
2. Cliquez sur l’utilisateur hello dans la liste des utilisateurs hello.
3. Cliquez sur **Supprimer**.  Un message de confirmation s’affiche.
4. Cliquez sur **Oui** utilisateur de hello tooremove du rôle de hello.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
