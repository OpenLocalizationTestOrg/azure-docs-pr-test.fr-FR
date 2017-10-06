---
title: "aaaLimitations d’Azure Active Directory B2B collaboration | Documents Microsoft"
description: "Limitations actuelles d’Azure Active Directory B2B Collaboration"
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a>Limitations d’Azure AD B2B Collaboration
Azure Active Directory (Azure AD) B2B collaboration est actuellement les limitations de toohello sujet décrites dans cet article.

## <a name="possible-double-multi-factor-authentication"></a>Risque de redondance de l’authentification multifacteur
Avec Azure AD B2B, vous pouvez appliquer l’authentification multifacteur à l’organisation de ressource hello (hello invitation d’organisation). raisons Hello de cette approche sont détaillées dans [accès conditionnel pour les utilisateurs de collaboration B2B](active-directory-b2b-mfa-instructions.md). Si un partenaire possède déjà plusieurs facteurs d’authentification configuré et appliquée, leurs les utilisateurs peuvent avoir l’authentification hello tooperform qu’une seule fois dans leur organisation d’origine, puis à nouveau dans le vôtre.

## <a name="instant-on"></a>Activation instantanée
Dans le flux de collaboration hello B2B, nous ajouter les utilisateurs toohello répertoire et les mettre à jour dynamiquement pendant l’échange d’invitation, assignation d’application et ainsi de suite. Hello les mises à jour et les écritures normalement se produisent dans une instance d’un répertoire et doivent être répliqués sur toutes les instances. La réplication est terminée une fois toutes les instances mises à jour. Lorsque hello objet est écrit ou mis à jour dans une seule instance et hello appeler tooretrieve cet objet est parfois tooanother instance, des latences de réplication peuvent se produire. Si cela se produit, actualisez ou réessayez toohelp. Si vous écrivez une application à l’aide de notre API, puis les nouvelles tentatives avec certains temporisation est un tooalleviate correct, la pratique ce problème.

## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriétés de l’utilisateur B2B Collaboration](active-directory-b2b-user-properties.md)
* [Ajout d’un rôle tooa B2B collaboration](active-directory-b2b-add-guest-to-role.md)
* [Déléguer des invitations B2B Collaboration](active-directory-b2b-delegate-invitations.md)
* [Groupes dynamiques et B2B Collaboration](active-directory-b2b-dynamic-groups.md)
* [Code B2B Collaboration et exemples PowerShell](active-directory-b2b-code-samples.md)
* [Configurer des applications SaaS pour B2B Collaboration](active-directory-b2b-configure-saas-apps.md)
* [Jetons utilisateur B2B Collaboration](active-directory-b2b-user-token.md)
* [Mappage des revendications utilisateur B2B Collaboration](active-directory-b2b-claims-mapping.md)
* [Partage externe d’Office 365](active-directory-b2b-o365-external-user.md)
