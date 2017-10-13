---
title: Groupes dynamiques et Azure Active Directory B2B Collaboration | Microsoft Docs
description: "Azure Active Directory B2B Collaboration peut être utilisé avec des groupes dynamiques Azure AD"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: 5818c41610c8c5df89abcb0dcd058bcbe9579ce7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>Groupes dynamiques et Azure Active Directory B2B Collaboration

## <a name="what-are-dynamic-groups"></a>Qu'est-ce-que les groupes dynamiques ?
La configuration dynamique de l’appartenance au groupe de sécurité pour Azure Active Directory (Azure AD) est disponible dans le [portail Azure](https://portal.azure.com). Les administrateurs peuvent définir des règles pour remplir les groupes créés dans Azure Active Directory en fonction d'attributs utilisateur (par exemple, userType, département ou pays). Les membres peuvent être automatiquement ajoutés ou supprimés d’un groupe de sécurité en fonction de leurs attributs. Ces groupes permettent d’accorder l’accès à des applications ou à des ressources cloud (sites SharePoint, documents) et d’attribuer des licences à des utilisateurs. En savoir plus sur les groupes dynamiques dans [Groupes dédiés dans Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).

La [licence Azure AD Premium P1 ou P2](https://azure.microsoft.com/pricing/details/active-directory/) appropriée est nécessaire pour créer et utiliser des groupes dynamiques. Pour en savoir plus, consultez l’article [Créer des règles basées sur les attributs pour l’appartenance à un groupe dynamique dans Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).

## <a name="what-are-the-built-in-dynamic-groups"></a>Que sont les groupes dynamiques intégrés ?
Le groupe dynamique **Tous les utilisateurs** permet à des administrateurs de locataires de créer un groupe contenant tous les utilisateurs dans le locataire en un seul clic. Par défaut, le groupe **Tous les utilisateurs** inclut tous les utilisateurs du répertoire, dont les invités et les utilisateurs externes.
Dans le nouveau portail d’administration Azure Active Directory, vous pouvez choisir d’activer le groupe **Tous les utilisateurs** dans l’affichage des paramètres de groupe.

![groupes intégrés](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-the-all-users-dynamic-group"></a>Renforcement de la sécurité du groupe dynamique Tous les utilisateurs
Par défaut, le groupe **Tous les utilisateurs** contient également vos utilisateurs B2B Collaboration (invités). Vous pouvez sécuriser davantage votre groupe **Tous les utilisateurs** en utilisant une règle pour supprimer les utilisateurs invités. L’illustration suivante montre le groupe **Tous les utilisateurs** modifié de manière à exclure les invités.

![activer le groupe Tous les utilisateurs](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

Vous trouverez peut-être aussi utile de créer un groupe dynamique contenant uniquement les utilisateurs invités, afin de pouvoir leur appliquer des stratégies (telles que des stratégies d’accès conditionnel Azure AD).
Ce groupe pourrait ressembler à ceci :

![exclure les utilisateurs invités](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriétés de l’utilisateur B2B Collaboration](active-directory-b2b-user-properties.md)
* [Ajout d’un utilisateur B2B Collaboration à un rôle](active-directory-b2b-add-guest-to-role.md)
* [Déléguer des invitations B2B Collaboration](active-directory-b2b-delegate-invitations.md)
* [Code B2B Collaboration et exemples PowerShell](active-directory-b2b-code-samples.md)
* [Configurer des applications SaaS pour B2B Collaboration](active-directory-b2b-configure-saas-apps.md)
* [Jetons utilisateur B2B Collaboration](active-directory-b2b-user-token.md)
* [Mappage des revendications utilisateur B2B Collaboration](active-directory-b2b-claims-mapping.md)
* [Partage externe d’Office 365](active-directory-b2b-o365-external-user.md)
* [Limitations actuelles de B2B Collaboration](active-directory-b2b-current-limitations.md)
