---
title: "utilisateurs aaaAdd d’autres répertoires ou les partenaires dans Azure Active Directory | Documents Microsoft"
description: "Explique comment les utilisateurs tooadd ou modifier les informations utilisateur dans Azure Active Directory, y compris les utilisateurs externes et l’invité."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a>Ajouter des utilisateurs à partir d’autres répertoires ou entreprises partenaires dans Azure Active Directory

Cet article explique comment les utilisateurs tooadd à partir d’autres annuaires dans Azure Active Directory ou ajouter des utilisateurs à partir des sociétés partenaires. Pour plus d’informations sur l’ajout de nouveaux utilisateurs dans votre organisation et ajout d’utilisateurs qui disposent de comptes Microsoft, consultez [ajouter de nouveaux utilisateurs tooAzure Active Directory](active-directory-create-users.md). 

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Pour comment les utilisateurs invités de collaboration tooadd B2B dans hello Azure AD admin center, consultez [Nouveautés d’Azure AD B2B collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)

Les utilisateurs ajoutés ne disposent pas des autorisations d’administrateur par défaut, mais vous pouvez attribuer des rôles toothem à tout moment.

## <a name="add-a-user"></a>Ajouter un utilisateur
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **Active Directory**, puis ouvrez votre répertoire.
3. Sélectionnez hello **utilisateurs** et puis, dans la barre de commandes hello, sélectionnez **ajouter un utilisateur**.
4. Sur hello **faites-nous part de cet utilisateur** sous **Type d’utilisateur**, sélectionnez :

   * **Utilisateur dans un autre annuaire Azure AD** – ajoute un annuaire tooyour de comptes d’utilisateur en provenance d’un autre annuaire Azure AD. Vous pouvez sélectionner un utilisateur dans un autre répertoire uniquement si vous êtes également membre de ce répertoire.
   * **Les utilisateurs dans les entreprises partenaires** -tooinvite et autoriser des partenaires de tooyour entreprise aux utilisateurs (voir [Azure Active Directory B2B collaboration](active-directory-b2b-what-is-azure-ad-b2b.md)). Vous devez trop[charger un fichier CSV en spécifiant les adresses de messagerie](active-directory-b2b-references-csv-file-format.md).
5. Utilisateur de hello **profil** , fournissez un nom et prénom, un nom convivial et un rôle d’utilisateur à partir de hello **rôles** liste. Pour plus d’informations sur les utilisateurs et les rôles d’administrateur, consultez la page [Attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md). Spécifiez si trop**activer l’authentification multifacteur** pour l’utilisateur de hello.
6. Sur hello **mot de passe temporaire Get** page, sélectionnez **créer**.

> [!IMPORTANT]
> Si votre organisation utilise plusieurs domaines, vous devez savoir sur hello suivants lorsque vous ajoutez un compte d’utilisateur :
>
> * comptes d’utilisateur tooadd avec hello même nom d’utilisateur principal (UPN) sur plusieurs domaines, **première** ajouter, par exemple, geoffgrisso@contoso.onmicrosoft.com, **suivie** geoffgrisso@contoso.com.
> * **N’ajoutez pas**geoffgrisso@contoso.com avant d’avoir ajouté geoffgrisso@contoso.onmicrosoft.com.
>

Si vous modifiez les informations d’un utilisateur dont l’identité est synchronisée avec votre service d’Active Directory local, vous ne pouvez modifier les informations utilisateur de hello Bonjour portail Azure classic. toochange hello des informations sur l’utilisateur, utilisez vos outils de gestion Active Directory local.

## <a name="add-external-users"></a>Ajouter des utilisateurs externes
Vous pouvez également ajouter des utilisateurs à partir d’un autre toowhich de répertoire Azure AD qu'auxquels vous appartenez ou sociétés partenaires en téléchargeant un fichier CSV. tooadd un utilisateur externe, pour **Type d’utilisateur**, spécifiez **utilisateur dans un autre annuaire Microsoft Azure AD** ou **les utilisateurs dans les entreprises partenaires**.

Les deux types d’utilisateurs proviennent d’un autre répertoire et sont ajoutés en tant **qu’utilisateurs externes**. Les utilisateurs externes peuvent collaborer avec d’autres utilisateurs dans un répertoire sans les nouveaux comptes d’exigence tooadd et les informations d’identification. Les utilisateurs externes s’authentifier avec leur répertoire de base lorsqu’ils se connectent et que l’authentification fonctionne pour n’importe quel autre toowhich répertoires qu’ils ont été ajoutés.

## <a name="external-user-management-and-limitations"></a>Gestion des utilisateurs externes et limitations
Lorsque vous ajoutez un utilisateur à partir d’un autre répertoire de tooyour, cet utilisateur est un utilisateur externe dans votre annuaire. nom d’utilisateur et le nom d’affichage Hello sont copiés à partir de leur répertoire de base et utilisés pour l’utilisateur externe de hello dans votre annuaire. Dès lors, les propriétés de compte d’utilisateur externe hello sont entièrement indépendantes. Si des modifications de propriété sont apportées toohello utilisateur dans leur répertoire de base, ces modifications ne sont pas propagées toohello compte d’utilisateur externe dans votre annuaire.

Hello seul lien entre deux comptes de hello est que l’utilisateur hello s’authentifie toujours auprès de leur annuaire principal ou avec leur compte Microsoft. C’est pourquoi vous ne les voyez un mot de passe option tooreset hello ou activer l’authentification multifacteur pour un utilisateur externe. Actuellement, la stratégie d’authentification de compte Microsoft ou de répertoire hello hello est hello seule évaluée lorsque hello utilisateur se connecte.

> [!NOTE]
> Vous pouvez toujours désactiver utilisateur externe de hello dans répertoire hello, ce qui bloque l’accès à tooyour directory.
>
>

Si un utilisateur est supprimé de son annuaire principal ou elles annulent son compte Microsoft, les utilisateurs externes hello existe toujours dans votre annuaire. Toutefois, utilisateur hello dans votre annuaire ne peut pas accéder aux ressources, car ils ne peuvent pas s’authentifier avec un répertoire de base ou d’un compte Microsoft.

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a>Services auxquels peuvent avoir accès les utilisateurs externes Azure AD
* **Portail Azure classic**: permet à un utilisateur externe qui est un administrateur de plusieurs répertoires toomanage chaque de ces répertoires.
* **SharePoint Online**: si le partage externe est activé, permet une tooaccess utilisateur externe de ressources SharePoint Online autorisé.
* **Dynamics CRM**: si l’utilisateur de hello est concédé sous licence via PowerShell, permet à un utilisateur externe de tooaccess autorisé ressources dans Dynamics CRM.
* **Dynamics AX**: si l’utilisateur de hello est concédé sous licence via PowerShell, permet à un utilisateur externe de tooaccess autorisé ressources dans Dynamics AX. Hello limitations pour [aux utilisateurs externes d’Azure AD](#known-limitations-of-azure-ad-external-users) appliquer tooexternal les utilisateurs de Dynamics AX ainsi.

## <a name="next-steps"></a>Étapes suivantes
* [Ajouter de nouveaux utilisateurs tooAzure Active Directory](active-directory-create-users.md)
* [Administration d’Azure AD](active-directory-administer.md)
* [Gestion des mots de passe dans Azure AD](active-directory-manage-passwords.md)
* [Gestion des groupes dans Azure AD](active-directory-manage-groups.md)
