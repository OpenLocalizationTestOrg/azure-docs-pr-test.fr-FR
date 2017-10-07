---
title: "domaine personnalisé tooa utilisateurs aaaAssign dans Azure Active Directory | Documents Microsoft"
description: "Comment toopopulate un domaine personnalisé dans Azure Active Directory avec des comptes d’utilisateur."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a>Affecter les utilisateurs domaine personnalisé tooa
Après avoir ajouté votre tooAzure personnalisé de domaine Active Directory, vous devez ajouter les comptes d’utilisateur hello pour ce domaine afin que vous puissiez commencer à authentifier les.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Pour comment toomanage vos noms de domaine dans le centre d’administration hello Azure AD, consultez [la gestion des noms de domaines personnalisés dans Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Utilisateurs synchronisés à partir d’un répertoire local
Si vous avez déjà configuré une connexion entre votre service Active Directory et Azure Active Directory, synchronisation peut remplir les comptes hello. Pour plus d’informations sur comment toosynchronize Azure Active Directory avec votre Active Directory local, consultez [intégrer vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-hello-cloud"></a>Les utilisateurs ajoutés et gérés dans le cloud de hello
domaine de hello toochange pour un compte d’utilisateur :

1. Ouvrez hello portail Azure classic à l’aide d’un compte qui est un administrateur global ou un administrateur de l’utilisateur.
2. Ouvrez votre annuaire.
3. Sélectionnez hello **utilisateurs** onglet.
4. Sélectionnez l’utilisateur de hello à partir de la liste de hello.
5. Modifier le domaine hello pour l’utilisateur de hello et sélectionnez **enregistrer**.

Cela peut également être effectuée à l’aide [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) ou hello [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Sélectionner un domaine personnalisé lors de la création d'un nouvel utilisateur
1. Ouvrez hello portail Azure classic à l’aide d’un compte qui est un administrateur global ou un administrateur de l’utilisateur.
2. Ouvrez votre annuaire.
3. Sélectionnez hello **utilisateurs** onglet.
4. Dans la barre de commandes hello, sélectionnez **ajouter**.
5. Lorsque vous ajoutez le nom d’utilisateur hello, choisissez le domaine personnalisé de hello à partir de la liste des domaines hello.
6. Sélectionnez **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
* [À l’aide du domaine personnalisé noms toosimplify hello expérience de connexion pour vos utilisateurs](active-directory-add-domain.md)
* [Gérer les noms de domaine personnalisés](active-directory-add-manage-domain-names.md)
* [En savoir plus sur les concepts de gestion de domaine dans Azure AD](active-directory-add-domain-concepts.md)

