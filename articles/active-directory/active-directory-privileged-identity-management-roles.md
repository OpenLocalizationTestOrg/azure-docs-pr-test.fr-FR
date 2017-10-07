---
title: aaaRoles dans Azure AD Privileged Identity Management | Documents Microsoft
description: "Découvrez les rôles sont utilisés pour les identités privilégiées avec hello extension d’Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: dc58d005489e3b51b3b3dbea4bf35bd795dbdfb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Rôle d’administrateur différent dans Azure Active Directory PIM
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

Vous pouvez affecter des utilisateurs de votre organisation toodifferent des rôles d’administrateur dans Azure AD. Ces attributions de contrôlent les tâches, telles que l’ajout ou la suppression d’utilisateurs ou modifier des paramètres de service, les utilisateurs de hello sont tooperform en mesure de sur Azure AD, Office 365 et d’autres services Microsoft Online Services et applications connectées.  

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.

Un administrateur global peut mettre à jour les utilisateurs qui **définitivement** assigné tooroles dans Azure AD, à l’aide des applets de commande PowerShell comme `Add-MsolRoleMember` et `Remove-MsolRoleMember`, ou via le portail classique de hello comme décrit dans [ attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles.md).

Azure AD Privileged Identity Management (PIM) gère les stratégies pour l’accès privilégié des utilisateurs dans Azure AD. PIM assigne tooone d’utilisateurs ou de plusieurs rôles dans Azure AD, et vous pouvez affecter une personne toobe définitivement dans le rôle de hello ou éligibles pour le rôle de hello. Lorsqu’un utilisateur est définitivement rôle tooa ou Active une attribution de rôle éligibles, puis ils peuvent gérer Azure Active Directory, Office 365 et autres applications avec des autorisations hello tootheir rôles attribuées.

Il n’existe aucune différence dans access hello donné toosomeone avec un permanente ou une attribution de rôle éligible. Hello seule différence est que certaines personnes n’avez pas besoin que l’accès tout le temps hello. Ils deviennent éligibles pour le rôle de hello et que vous peuvent l’activer et désactiver chaque fois qu’ils ont besoin pour.

## <a name="roles-managed-in-pim"></a>Rôles gérés dans PIM
Privileged Identity Management vous permet d’attribuer des rôles d’administrateur toocommon les utilisateurs, y compris :

* **Administrateur général** (également appelé administrateur de la société) a des fonctionnalités d’administration de l’accès tooall. Vous pouvez avoir plus d’un administrateur général dans votre organisation. personne Hello qui s’inscrit automatiquement toopurchase Office 365 devient un administrateur général.
* **Administrateur de rôle privilégié** : gère Azure AD PIM et met à jour les attributions de rôles pour d’autres utilisateurs.  
* **Administrateur de facturation** : effectue des achats, gère les abonnements, gère les tickets de support et surveille l’état des services.
* **Administrateur de mots de passe** : réinitialise les mots de passe, gère les demandes de service et surveille l’état des services. Les administrateurs de mot de passe sont tooresetting limité de mots de passe des utilisateurs.
* **Administrateur de services fédérés** : gère les demandes de service et surveille l’état des services.
  
  > [!NOTE]
  > Si vous utilisez Office 365, puis avant de lui assigner hello admin rôle tooa utilisateur, tout d’abord affecter des hello utilisateur autorisations administratives tooa service, comme Exchange Online.
  > 
  > 
* **Administrateur de gestion des utilisateurs** : réinitialise les mots de passe, surveille l’état des services et gère les comptes d’utilisateur, les groupes d’utilisateurs et les demandes de service. administration de la gestion utilisateur Hello ne peut pas supprimer un administrateur global, créer d’autres rôles d’administrateur ou réinitialiser les mots de passe pour la facturation, généraux et les administrateurs de service.
* **Administrateur Exchange** a tooExchange d’un accès administratif en ligne via le centre d’administration Exchange hello (EAC) et peuvent effectuer presque n’importe quelle tâche dans Exchange Online.
* **L’administrateur SharePoint** a tooSharePoint d’un accès administratif en ligne via le centre d’administration SharePoint Online hello et peuvent effectuer presque n’importe quelle tâche dans SharePoint Online.
* **Skype pour l’administrateur d’entreprise** a un accès administratif tooSkype for Business via hello Skype pour le centre d’administration métier et peut effectuer presque n’importe quelle tâche dans Skype entreprise Online.

Consultez les articles suivants pour plus d’informations sur l’[attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md) et sur l’[attribution de rôles d’administrateur dans Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


À partir de PIM, vous pouvez [affecter ces utilisateur tooa de rôles](active-directory-privileged-identity-management-how-to-add-role-to-user.md) afin que hello utilisateur peut [activer rôle hello lorsque nécessaire](active-directory-privileged-identity-management-how-to-activate-role.md).

Si vous voulez toogive un autre toomanage d’accès utilisateur dans PIM lui-même, les rôles hello PIM nécessite hello utilisateur toohave sont décrites dans [comment toogive aux tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>Rôles non gérés dans PIM
Les rôles dans Exchange Online ou SharePoint Online, à l’exception de ceux mentionnés ci-dessus, ne sont pas représentés dans Azure AD et par conséquent, ne sont pas visibles dans PIM. Pour plus d’informations sur la modification des affectations de rôles affinées dans ces services Office 365, consultez [Autorisations dans Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).

Les groupes de ressources et les abonnements Azure ne sont pas représentés non plus dans Azure AD. toomanage Azure abonnements, consultez [comment tooadd ou modifier les rôles administrateur Azure](../billing/billing-add-change-azure-subscription-administrator.md) et pour plus d’informations sur, consultez Azure RBAC [du contrôle d’accès](role-based-access-control-configure.md).

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>Rôles d’utilisateur et connexion
Pour certains services et applications Microsoft, affectation d’un rôle d’utilisateur tooa ne peut être suffisamment tooenable que toobe d’utilisateur administrateur.

Nécessite l’accès toohello portail Azure classic hello utilisateur être un administrateur de service ou un coadministrateur sur un abonnement Azure, même si l’utilisateur de hello n’avez besoin de toomanage hello abonnements Azure.  Par exemple, les paramètres de configuration toomanage pour Azure AD dans le portail classique hello, un utilisateur doivent être un administrateur global dans Azure AD et un coadministrateur abonnement sur un abonnement Azure.  toolearn tooadd les abonnements tooAzure les utilisateurs, voir [comment tooadd ou modifier les rôles administrateur Azure](../billing/billing-add-change-azure-subscription-administrator.md).

TooMicrosoft d’accès aux Services en ligne peuvent requérir hello utilisateur également avoir une licence avant de pouvoir ouvrir le portail du service de hello ou effectuer des tâches administratives.

## <a name="assign-a-license-tooa-user-in-azure-ad"></a>Affecter un utilisateur tooa de licence dans Azure AD
1. Connectez-vous à toohello [portail Azure classic](http://manage.windowsazure.com) avec un compte d’administrateur général ou un compte de coadministrateur.
2. Sélectionnez **tous les éléments** à partir du menu principal de hello.
3. Sélectionnez hello répertoire toowork avec et que les licences associée.
4. Sélectionnez **Licences**. liste Hello de licences disponibles s’affiche.
5. Sélectionnez le plan de licence hello qui contient des licences hello que vous souhaitez toodistribute.
6. Sélectionnez **Affecter des utilisateurs**.
7. Utilisateur hello SELECT que vous souhaitez tooassign une licence à.
8. Cliquez sur hello **affecter** bouton.  utilisateur de Hello peut maintenant se connecter tooAzure.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

