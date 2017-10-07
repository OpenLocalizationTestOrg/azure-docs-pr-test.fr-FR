---
title: aaaAdd B2B collaboration utilisateurs tooAzure Active Directory sans invitation | Documents Microsoft
description: "Vous pouvez permettre à un utilisateur invité d’ajouter d’autres tooyour d’utilisateurs invités Azure AD sans échange une invitation dans Azure Active Directory B2B collaboration."
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a>Ajouter des utilisateurs invités B2B Collaboration sans invitation

Vous pouvez autoriser un utilisateur, par exemple un partenaire représentatif, tooadd les utilisateurs de hello partenaire tooyour organisation sans avoir besoin de toobe invitations échangé. Il vous suffit est lui accorder les privilèges d’énumération dans le répertoire de hello vous utilisez pour l’organisation du partenaire hello 

Accordez ces privilèges lorsque :

1. Un utilisateur d’organisation d’hôte hello (par exemple, WoodGrove) invite un utilisateur à partir de l’organisation partenaire de hello (par exemple, Sam@litware.com) en tant qu’invité.
2. admin Hello dans l’organisation d’hôte hello définit les stratégies qui permettent de Sam tooidentify et ajouter d’autres utilisateurs de l’organisation partenaire de hello (Litware).
3. Maintenant Sam peut ajouter d’autres utilisateurs d’annuaire de Litware toohello WoodGrove, des groupes ou des applications sans avoir besoin de toobe des invitations à participer à échanger. Si Sam dispose de privilèges d’énumération appropriée de hello dans Litware, il se produit automatiquement.

### <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-admin-add-users.md)
* [Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-iw-add-users.md)
* [éléments Hello Hello e-mail d’invitation B2B collaboration](active-directory-b2b-invitation-email.md)
* [Utilisation d’une invitation B2B Collaboration](active-directory-b2b-redemption-experience.md)
* [Attribution de licences Azure AD B2B Collaboration](active-directory-b2b-licensing.md)
* [Résolution des problèmes d’Azure Active Directory B2B Collaboration](active-directory-b2b-troubleshooting.md)
* [Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration](active-directory-b2b-faq.md)
* [API et personnalisation d’Azure Active Directory B2B Collaboration](active-directory-b2b-api.md)
* [Authentification multifacteur pour les utilisateurs B2B Collaboration](active-directory-b2b-mfa-instructions.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)