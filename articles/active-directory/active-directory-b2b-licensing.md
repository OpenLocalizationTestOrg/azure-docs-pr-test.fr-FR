---
title: collaboration aaaAzure Active Directory B2B Gestionnaire de licences des conseils | Documents Microsoft
description: "Azure Active Directory B2B Collaboration ne nécessite pas de licences Azure AD payées, mais vous pouvez également obtenir des fonctionnalités payantes pour les utilisateurs invités B2B."
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
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: sasubram
ms.custom: it-pro
ms.openlocfilehash: 8e15d66209b090bff210674ecdacc88cd642dcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a>Guide d’attribution de licences pour Azure Active Directory B2B Collaboration

Vous pouvez utiliser Azure AD B2B collaboration fonctionnalités tooinvite invité aux utilisateurs dans votre tooallow de locataire Azure AD les tooaccess services Azure AD et autres ressources de votre organisation. Si vous souhaitez que les fonctionnalités de tooprovide accès toopaid Azure AD, B2B les utilisateurs invités de collaboration doivent disposer d’une licence avec appropriées des licences Azure AD. 

Plus précisément :
* Les fonctionnalités Azure AD Free sont disponibles pour les utilisateurs invités sans licence supplémentaire.
* Si vous souhaitez que les utilisateurs Azure AD fonctionnalités tooB2B tooprovide accès toopaid, vous devez disposer de suffisamment toosupport licences ces invités B2B.
* Un locataire invitant à une annonce Azure payé licence avec B2B collaboration utilisation droits tooan supplémentaires cinq B2B invité utilisateurs invités toohello client.
* client Hello propriétaire hello inviter locataire doit être hello un toodetermine combien d’utilisateurs collaboration B2B devez payée les fonctionnalités d’Azure AD. Hello payé Azure AD en fonction de fonctionnalités que vous souhaitez pour les utilisateurs invités, vous devez disposer de suffisamment d’Azure AD payant licences aux utilisateurs de toocover B2B collaboration Bonjour même rapport 5:1.

Un utilisateur invité de la collaboration B2B est ajouté en tant qu’utilisateur d’une société partenaire, et pas un employé de votre organisation ou un employé d’une autre entreprise dans votre conglomérat. Un utilisateur invité B2B peut se connecter avec des informations d’identification externes ou détenues par votre organisation, comme décrit dans cet article. 

En d’autres termes, le Gestionnaire de licences B2B est définir pas par comment hello utilisateur s’authentifie mais par relation hello de l’organisation tooyour hello utilisateur. Si ces utilisateurs ne sont pas des partenaires, ils sont traités différemment selon les conditions de licence. Ils ne sont pas considérés comme toobe un utilisateur de collaboration B2B pour l’accord de licence, même si leur UserType est marqué comme « Invité ». Ils doivent disposer normalement d’une licence et une licence par utilisateur. Ces utilisateurs sont les suivants :
* vos employés
* le personnel connecté à l’aide d’identités externes
* un employé d’une autre entreprise dans votre conglomérat


## <a name="licensing-examples"></a>Exemples d’attribution de licences
- Un client souhaite tooinvite 100 B2B collaboration utilisateurs tooits locataire Azure AD. client de Hello affecte la gestion de l’accès et de configuration pour tous les utilisateurs, mais 50 utilisateurs requièrent également l’authentification Multifacteur et l’accès conditionnel. Ce client doit acheter des licences Azure AD Basic 10 et 10 toocover de licences Azure AD Premium P1 ces utilisateurs B2B correctement. Si le client de hello prévoit des fonctionnalités de Protection de l’identité de toouse avec des utilisateurs B2B, elles doivent avoir les utilisateurs de Azure AD Premium P2 licences toocover hello invité dans hello même rapport 5:1.
- Un client a 10 employés qui disposent tous d’une licence Premium P1 Azure AD. Ils veulent désormais tooinvite 60 B2B les utilisateurs qui nécessitent l’authentification multifacteur (MFA). Sous la règle de gestion des licences de 5:1 hello, les clients de hello doit avoir au moins 12 toocover de licences Azure AD Premium P1 tous les utilisateurs de collaboration B2B 60. Car ils ont déjà 10 licences Premium P1 pour leurs 10 employés, ils ont des droits tooinvite 50 B2B utilisateurs avec les fonctionnalités Premium P1 telles que l’authentification Multifacteur. Dans cet exemple, puis, il doit acheter 2 licences Premium P1 supplémentaires toocover hello 10 B2B collaboration utilisateurs restants.

> [!NOTE]
> Il n’existe aucun moyen encore tooassign licences directement toohello B2B utilisateurs tooenable ces droits d’utilisateur B2B collaboration.

client Hello propriétaire hello inviter locataire doit être hello un toodetermine combien d’utilisateurs collaboration B2B devez payée les fonctionnalités d’Azure AD. Selon lequel payé fonctionnalités d’Azure AD que vous souhaitez pour vos utilisateurs invités, vous devez disposer de suffisamment de Azure AD payé aux utilisateurs de licences toocover B2B collaboration dans le rapport de 5:1 hello. 

## <a name="additional-licensing-details"></a>Informations supplémentaires sur l’attribution de licences
- Il est inutile de comptes d’utilisateur tooB2B tooactually attribuer des licences. En fonction de rapport de 5:1 hello, Gestionnaire de licences est automatiquement calculée et indiquée.
- Si aucune payé licence Azure AD existe dans le locataire hello, tous droits hello Obtient l’utilisateur invité hello Azure AD gratuit offres d’édition.
- Si un B2B collaboration utilisateur possède une publicité Azure payante concéder sous licence à partir de leur organisation, ils n’utilisent pas une des licences de collaboration hello B2B de client d’invitation hello.

## <a name="advanced-discussion-what-are-hello-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a>Advanced discussion : quelles sont les considérations relatives aux licences hello lorsque nous ajouter des utilisateurs à partir d’une organisation conglomérat comme « membres » à l’aide de votre API ?
Utilisateur invité B2B est celle qui est invitée à partir d’un toowork d’organisation partenaire avec l’organisation d’hôte hello. En règle générale, aucun autre cas n’est considéré comme B2B, même s’il utilise des fonctionnalités B2B. Nous allons examiner deux cas en particulier :

1. Si un hôte invite un employé à l’aide d’une adresse client
  * Ce scénario n’est pas conforme à nos stratégies de gestion des licences et n’est actuellement pas recommandé.

2. Si une organisation hôte ajoute un utilisateur à partir d’un autre conglomérat
  1. Dans ce cas, les utilisateurs hello sont invitée à l’aide des API de B2B, mais ce cas n’est pas généralement B2B. Dans l’idéal, nous devrions obtenir ces organisations invitation hello d’autres utilisateurs des organisations en tant que membres (notre API qui permet). Dans ce cas, les licences ont toobe affecté toothese des membres pour les ressources tooaccess Bonjour invitation d’organisation.

  2. Certaines organisations peuvent choisir tooadd hello toobe d’utilisateurs d’autres org. ajouté en tant que « Invité » en tant que stratégie. Il existe deux cas :
      * Hello conglomérat organisation utilise déjà Azure AD et les utilisateurs de hello invité sont concédés sous licence Bonjour autre organisation : dans ce cas, nous ne pensons pas hello de toofollow tooneed utilisateurs invités 1:5 formule présenté précédemment dans ce document. 

      * Hello conglomérat organisation n’utilise pas d’Azure AD ou ne dispose pas des licences appropriées : dans ce cas, suivez hello 1:5 formule présenté précédemment dans ce document.

## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-admin-add-users.md)
* [Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-iw-add-users.md)
* [éléments Hello Hello e-mail d’invitation B2B collaboration](active-directory-b2b-invitation-email.md)
* [Utilisation d’une invitation B2B Collaboration](active-directory-b2b-redemption-experience.md)
* [Résolution des problèmes d’Azure Active Directory B2B Collaboration](active-directory-b2b-troubleshooting.md)
* [Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration](active-directory-b2b-faq.md)
* [API et personnalisation d’Azure Active Directory B2B Collaboration](active-directory-b2b-api.md)
* [Authentification multifacteur pour les utilisateurs B2B Collaboration](active-directory-b2b-mfa-instructions.md)
* [Ajouter des utilisateurs B2B Collaboration sans invitation](active-directory-b2b-add-user-without-invite.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
