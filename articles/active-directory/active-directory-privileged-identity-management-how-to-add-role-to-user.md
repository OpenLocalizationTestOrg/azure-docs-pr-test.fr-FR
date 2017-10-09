---
title: "aaaHow tooadd ou supprimer un rôle d’utilisateur | Documents Microsoft"
description: "Découvrez comment les identités de tooprivileged tooadd rôles avec hello application d’Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a>Azure AD Privileged Identity Management : Comment tooadd ou supprimer un rôle d’utilisateur
Avec Azure Active Directory (AD), un administrateur global (ou l’administrateur de la société) peut mettre à jour les utilisateurs qui **définitivement** assigné tooroles dans Azure AD. Cette opération s’effectue avec les applets de commande PowerShell, telles que `Add-MsolRoleMember` et `Remove-MsolRoleMember`. Ou ils peuvent utiliser le portail Azure classic de hello comme décrit dans [attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles.md).

Hello application Azure AD Privileged Identity Management permet aux administrateurs de rôle privilégié toomake permanente attributions de rôles, ainsi. En outre, les administrateurs de rôle privilégié peuvent rendre les utilisateurs **éligibles** pour les rôles d’administrateur. Un administrateur éligible peut activer le rôle de hello lorsqu’ils en ont besoin, et ensuite leurs autorisations expirent une fois qu’ils ont terminé.

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a>Gérer les rôles avec PIM Bonjour portail Azure
Dans votre organisation, vous pouvez affecter des utilisateurs toodifferent les rôles d’administrateur dans Azure AD, Office 365 et d’autres services et applications Microsoft.  Vous trouverez plus d’informations sur les rôles disponibles hello à [rôles dans Azure AD PIM](active-directory-privileged-identity-management-roles.md).

tooadd ou supprimer un utilisateur dans un rôle à l’aide de Privileged Identity Management, affiche le tableau de bord de hello PIM. Puis cliquez sur hello **les utilisateurs des rôles d’administrateur** ou pour sélectionner un rôle spécifique (par exemple, l’administrateur Global) à partir de la table de rôles hello.

> [!NOTE]
> Si vous n’avez pas encore activée PIM Bonjour portail Azure, passez trop[prise en main Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) pour plus d’informations.

Si vous voulez toogive un autre utilisateur tooPIM accès lui-même, les rôles hello qui nécessite de PIM hello utilisateur toohave sont décrites dans [comment toogive aux tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="add-a-user-tooa-role"></a>Ajouter un rôle d’utilisateur tooa
1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez hello **Azure AD Privileged Identity Management** vignette sur le tableau de bord hello.
2. Sélectionnez **Gérer les rôles privilégiés**.
3. Bonjour **résumé du rôle** table, sélectionnez hello rôle de toomanage.
4. Dans le panneau de rôle hello, sélectionnez **ajouter**.
5. Cliquez sur **sélectionnez utilisateurs** et rechercher un utilisateur hello sur hello **sélectionnez utilisateurs** panneau.  
6. Sélectionnez un utilisateur de hello à partir de la liste des résultats hello, puis cliquez sur **fait**.
7. Cliquez sur **OK** toosave votre sélection. utilisateur Hello que vous avez sélectionné s’affiche dans la liste hello comme éligibles pour le rôle de hello.

> [!NOTE]
> Nouveaux utilisateurs dans un rôle ne sont pas éligibles pour le rôle hello par défaut. Si vous souhaitez le rôle de hello toomake permanente, cliquez sur utilisateur hello dans la liste de hello. les informations de l’utilisateur Hello s’affichent dans un nouveau panneau. Sélectionnez **l’autorisation de création** dans le menu d’informations utilisateur hello.  
> Si un utilisateur ne peut pas inscrire pour Azure multi-Factor Authentication (MFA), ou qu’il utilise un compte Microsoft (généralement @outlook.com), vous devez toomake les permanente de leurs rôles. Administrateurs éligibles demande tooregister pour l’authentification Multifacteur lors de l’activation.

Maintenant que hello utilisateur est éligible pour un rôle, indiquez-leur qu’ils peuvent activer il selon les instructions de toohello de [comment tooactivate ou désactiver un rôle](active-directory-privileged-identity-management-how-to-activate-role.md).

## <a name="remove-a-user-from-a-role"></a>Supprimer un utilisateur d’un rôle
Vous pouvez supprimer des utilisateurs des attributions de rôle éligible, mais assurez-vous qu’il reste toujours au moins un administrateur général permanent.

Suivez ces étapes de tooremove un utilisateur spécifique à partir d’un rôle :

1. Accédez rôle toohello dans la liste des rôles hello en sélectionnant un rôle dans le tableau de bord Azure AD PIM hello ou en cliquant sur hello **les utilisateurs des rôles d’administrateur** bouton.
2. Cliquez sur l’utilisateur hello dans la liste des utilisateurs hello.
3. Cliquez sur **Supprimer**. Un message vous demande tooconfirm.
4. Cliquez sur **Oui** rôle de hello tooremove à partir de l’utilisateur de hello.

Si vous ne savez pas quels utilisateurs ont toujours besoin de leurs attributions de rôles, vous pouvez [démarrer une vérification de l’accès pour le rôle de hello](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

