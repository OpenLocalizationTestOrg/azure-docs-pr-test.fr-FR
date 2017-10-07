---
title: invitations aaaDelegate pour Azure Active Directory B2B collaboration | Documents Microsoft
description: "Les propriétés de l’utilisateur Azure Active Directory B2B Collaboration sont configurables"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Déléguer des invitations pour Azure Active Directory B2B Collaboration

À la collaboration d’entreprise-entreprise (B2B) Azure Active Directory (Azure AD), il est inutile toobe un toosend les invitations administrateur global. Au lieu de cela, vous pouvez utiliser des stratégies et déléguer toousers invitations dont les rôles et les autorisent les invitations toosend. Un important nouvelle façon toodelegate invité utilisateur invitations est via le rôle d’invité Inviter hello.

## <a name="guest-inviter-role"></a>Rôle Inviteur d’invités
Nous pouvons attribuer hello utilisateur tooGuest invitations de toosend Inviter rôle. Vous n’êtes pas membre de toobe des invitations à participer à toosend de rôle d’administrateur global hello. Par défaut, les utilisateurs standard peuvent également appeler hello invitation API, sauf si un administrateur global désactivé invitations pour les utilisateurs normaux. Un utilisateur peut également appeler des API hello à l’aide de hello portail Azure ou PowerShell.

Voici un exemple qui montre comment toouse PowerShell tooadd un rôle d’invité Inviter toohello utilisateur :

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>Contrôler qui peut inviter

![Contrôle comment tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Avec Azure AD B2B collaboration, un administrateur client peut définir hello suivant des stratégies de l’invitation :

- Désactiver les invitations
- Seuls les administrateurs et les utilisateurs dans le rôle d’invité Inviter hello peuvent inviter
- Administrateurs, le rôle d’invité Inviter hello et membres peuvent inviter
- Tous les utilisateurs, notamment les invités, peuvent inviter

Par défaut, les clients sont définis trop n° 4. Tous les utilisateurs, notamment les invités, peuvent inviter des utilisateurs B2B.

## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriétés de l’utilisateur B2B Collaboration](active-directory-b2b-user-properties.md)
* [Ajout d’un rôle tooa B2B collaboration](active-directory-b2b-add-guest-to-role.md)
* [Groupes dynamiques et B2B Collaboration](active-directory-b2b-dynamic-groups.md)
* [Code B2B Collaboration et exemples PowerShell](active-directory-b2b-code-samples.md)
* [Configurer des applications SaaS pour B2B Collaboration](active-directory-b2b-configure-saas-apps.md)
* [Jetons utilisateur B2B Collaboration](active-directory-b2b-user-token.md)
* [Mappage des revendications utilisateur B2B Collaboration](active-directory-b2b-claims-mapping.md)
* [Partage externe d’Office 365](active-directory-b2b-o365-external-user.md)
* [Limitations actuelles de B2B Collaboration](active-directory-b2b-current-limitations.md)
