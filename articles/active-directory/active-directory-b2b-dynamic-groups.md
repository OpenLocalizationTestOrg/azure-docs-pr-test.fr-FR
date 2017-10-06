---
title: aaaDynamic groupes et Azure Active Directory B2B collaboration | Documents Microsoft
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
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>Groupes dynamiques et Azure Active Directory B2B Collaboration

## <a name="what-are-dynamic-groups"></a>Qu'est-ce-que les groupes dynamiques ?
Configuration dynamique de l’appartenance au groupe de sécurité pour Azure Active Directory (Azure AD) est disponible dans [hello Azure portal](https://portal.azure.com). Les administrateurs peuvent définir des règles toopopulate groupes qui sont créés dans Azure Active Directory basées sur les attributs de l’utilisateur (par exemple, userType, département ou pays). Les membres peuvent être ajoutées automatiquement tooor supprimé d’un groupe de sécurité en fonction de leurs attributs. Ces groupes peuvent fournir des accès des ressources cloud ou tooapplications (les sites SharePoint, des documents) et tooassign toomembers de licences. En savoir plus sur les groupes dynamiques dans [Groupes dédiés dans Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).

Hello approprié [licence Azure AD Premium P1 ou P2](https://azure.microsoft.com/pricing/details/active-directory/) est requis toocreate et l’utilisation des groupes dynamiques. En savoir plus, consultez l’article de hello [créer des règles d’attribut pour l’appartenance aux groupes dynamiques dans Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).

## <a name="what-are-hello-built-in-dynamic-groups"></a>Quelles sont les groupes dynamiques intégrés hello ?
Hello **tous les utilisateurs** permet à toocreate d’administrateurs client cliquez sur le groupe contenant tous les utilisateurs de client hello avec un seul groupe dynamique. Par défaut, hello **tous les utilisateurs** groupe comprend tous les utilisateurs de répertoire hello, y compris les membres et invités.
Dans le portail d’administration hello nouveau Azure Active Directory, vous pouvez choisir tooenable hello **tous les utilisateurs** groupe hello afficher les paramètres de groupe.

![groupes intégrés](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a>Sécurisation renforcée hello groupe dynamique de tous les utilisateurs
Par défaut, hello **tous les utilisateurs** groupe contient également les utilisateurs de collaboration (invité) B2B. Vous pouvez sécuriser davantage votre **tous les utilisateurs** groupe à l’aide d’une règle d’utilisateurs invités tooremove. Hello l’illustration suivante hello **tous les utilisateurs** groupe modifié tooexclude invités.

![activer le groupe Tous les utilisateurs](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

Il peut également s’avérer utile toocreate un nouveau groupe dynamique qui contient uniquement les utilisateurs invités, afin que vous pouvez appliquer des stratégies (telles que les stratégies d’accès conditionnel de Azure AD) toothem.
Ce groupe pourrait ressembler à ceci :

![exclure les utilisateurs invités](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriétés de l’utilisateur B2B Collaboration](active-directory-b2b-user-properties.md)
* [Ajout d’un rôle tooa B2B collaboration](active-directory-b2b-add-guest-to-role.md)
* [Déléguer des invitations B2B Collaboration](active-directory-b2b-delegate-invitations.md)
* [Code B2B Collaboration et exemples PowerShell](active-directory-b2b-code-samples.md)
* [Configurer des applications SaaS pour B2B Collaboration](active-directory-b2b-configure-saas-apps.md)
* [Jetons utilisateur B2B Collaboration](active-directory-b2b-user-token.md)
* [Mappage des revendications utilisateur B2B Collaboration](active-directory-b2b-claims-mapping.md)
* [Partage externe d’Office 365](active-directory-b2b-o365-external-user.md)
* [Limitations actuelles de B2B Collaboration](active-directory-b2b-current-limitations.md)
