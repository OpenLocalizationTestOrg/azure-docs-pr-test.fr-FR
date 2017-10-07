---
title: aaaAdd nouveaux utilisateurs tooAzure Active Directory | Documents Microsoft
description: Explique comment tooadd nouveaux utilisateurs ou modifier les informations utilisateur dans Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a>Ajouter de nouveaux utilisateurs ou utilisateurs avec tooAzure de comptes Microsoft Active Directory
Ajoutez les utilisateurs toopopulate votre répertoire. Cet article explique comment tooadd les nouveaux utilisateurs de votre organisation et comment tooadd les utilisateurs qui disposent de comptes Microsoft. Pour en savoir plus sur l’ajout d’utilisateurs à partir d’autres répertoires dans Azure Active Directory, ou sur l’ajout d’utilisateurs à partir d’entreprises partenaires, voir [Ajouter des utilisateurs à partir d’autres répertoires ou entreprises partenaires dans Azure Active Directory](active-directory-create-users-external.md). Les utilisateurs ajoutés ne disposent pas des autorisations d’administrateur par défaut, mais vous pouvez attribuer des rôles toothem à tout moment.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Pour tooadd un utilisateur dans le centre d’administration hello Azure AD, voir [ajouter de nouveaux utilisateurs tooAzure Active Directory](active-directory-users-create-azure-portal.md).

## <a name="add-a-user"></a>Ajouter un utilisateur
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **Active Directory**, puis sélectionnez le nom hello du répertoire de votre organisation.
3. Sélectionnez hello **utilisateurs** et puis, dans la barre de commandes hello, sélectionnez **ajouter un utilisateur**.
4. Sur hello **faites-nous part de cet utilisateur** sous **Type d’utilisateur**, sélectionnez :

   * **Nouvel utilisateur dans votre organisation** : permet d’ajouter un nouveau compte d’utilisateur dans votre répertoire.
   * **Utilisateur avec un compte Microsoft existant** – ajoute un annuaire Microsoft existant consommateur compte tooyour (par exemple, un compte Outlook)
5. En fonction de la valeur du champ **Type d’utilisateur**, saisissez un nom d’utilisateur (pour un nouvel utilisateur) ou une adresse e-mail (pour un utilisateur doté d’un compte Microsoft).
6. Utilisateur de hello **profil** , fournissez un nom et prénom, un nom convivial et un rôle d’utilisateur à partir de hello **rôles** liste. Pour plus d’informations sur les utilisateurs et les rôles d’administrateur, consultez la page [Attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md). Spécifiez si trop**activer l’authentification multifacteur** pour l’utilisateur de hello.
7. Sur hello **mot de passe temporaire Get** page, sélectionnez **créer**.

> [!IMPORTANT]
> Si votre organisation utilise plusieurs domaines, vous devez savoir sur hello suivants lorsque vous ajoutez un compte d’utilisateur :
>
> * comptes d’utilisateur tooadd avec hello même nom d’utilisateur principal (UPN) sur plusieurs domaines, **première** ajouter, par exemple, geoffgrisso@contoso.onmicrosoft.com, **suivie** geoffgrisso@contoso.com.
> * **N’ajoutez pas**geoffgrisso@contoso.com avant d’avoir ajouté geoffgrisso@contoso.onmicrosoft.com. Cet ordre est important et peut être fastidieuse tooundo.
>
>

## <a name="change-user-information"></a>Modification des informations utilisateur
Vous pouvez modifier n’importe quel attribut utilisateur à l’exception des ID d’objet hello.

1. Ouvrez votre annuaire.
2. Sélectionnez hello **utilisateurs** onglet et puis sélectionnez hello de hello utilisateur toochange.
3. Apportez les modifications nécessaires, puis cliquez sur **Enregistrer**.

Si l’utilisateur hello que vous êtes en train de modifier est synchronisé avec votre service d’Active Directory local, vous ne pouvez modifier hello utilisateur à l’aide de cette procédure. utilisateur de hello toochange, utilisez vos outils de gestion Active Directory local.

## <a name="guest-user-management-and-limitations"></a>Gestion des utilisateurs invités et limitations
Les comptes Invité sont les utilisateurs à partir d’autres annuaires qui ont été invités tooyour Active tooaccess SharePoint documents, d’applications ou d’autres ressources Windows Azure. Un compte invité dans votre annuaire a son attribut UserType sous-jacent défini trop « Guest ». Utilisateurs habituels (plus précisément, les membres de votre annuaire) est attribut UserType de hello « Membre ».

Invités ont un ensemble limité de droits dans le répertoire de hello. Ces droits limitent hello pour plus d’informations invités toodiscover sur les autres utilisateurs dans le répertoire de hello. Toutefois, les utilisateurs invités peuvent toujours interagir avec les utilisateurs de hello et associées aux ressources hello sur qu'ils travaillent des groupes. Les utilisateurs invités peuvent :

* Voir les autres utilisateurs et les groupes associés à un toowhich d’abonnement Azure qu'auquel elles sont affectées
* Afficher les membres de hello de toowhich de groupes qu’ils appartiennent.
* Rechercher d’autres utilisateurs dans le répertoire de hello, s’ils ne connaissent l’adresse de messagerie complète hello d’utilisateur de hello
* Voir qu’un ensemble limité d’attributs d’utilisateurs hello qu’ils recherchent--toodisplay limité nom, adresse de messagerie, nom d’utilisateur principal (UPN) et la photo miniature
* Obtenir la liste des domaines vérifiés dans le répertoire de hello
* Tooapplications de consentement, leur octroyer hello même accès des membres de votre annuaire

## <a name="set-guest-user-access-policies"></a>Définir les stratégies d’accès utilisateur
Hello **configurer** onglet d’un répertoire contient des options toocontrol accès pour les utilisateurs invités. Ces options peuvent uniquement être modifiées dans le portail Azure Classic par un administrateur général du répertoire. Pour le moment, il n’existe aucune méthode PowerShell ou API.

tooopen hello **configurer** onglet hello sélectionnez de portail classique Azure **Active Directory**, puis sélectionnez le nom hello du répertoire de hello.

![Onglet Configurer d’Azure Active Directory][1]

Vous pouvez ensuite modifier hello options toocontrol accès pour les utilisateurs invités.

![Options de contrôle d’accès des utilisateurs invités][2]

## <a name="whats-next"></a>Étapes suivantes
* [Ajouter des utilisateurs à partir d’autres répertoires ou entreprises partenaires dans Azure Active Directory](active-directory-create-users-external.md)
* [Administration d’Azure AD](active-directory-administer.md)
* [Gestion des mots de passe dans Azure AD](active-directory-manage-passwords.md)
* [Gestion des groupes dans Azure AD](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
