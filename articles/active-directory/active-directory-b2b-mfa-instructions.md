---
title: "l’accès pour les utilisateurs Azure Active Directory B2B collaboration aaaConditional | Documents Microsoft"
description: "Azure Active Directory B2B collaboration prend en charge l’authentification multifacteur (MFA) pour les applications d’entreprise un accès sélectif tooyour"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a>Accès conditionnel pour les utilisateurs de B2B Collaboration

## <a name="multi-factor-authentication-for-b2b-users"></a>Authentification MFA pour utilisateurs B2B
Avec Azure AD B2B Collaboration, les organisations peuvent appliquer des stratégies d’authentification multifacteur (MFA) pour les utilisateurs B2B. Ces stratégies peuvent être appliquées au client de hello, application ou au niveau utilisateur individuel, hello même façon qu’ils sont activés pour les employés à plein temps et les membres de l’organisation de hello. Stratégies d’authentification Multifacteur sont appliquées au niveau de l’organisation de ressource hello.

Exemple :
1. Travail d’administrateur ou des informations dans la société A invite l’utilisateur à partir de l’application de la société B tooan *Foo* dans la société A.
2. Application *Foo* dans la société A est toorequire configuré l’authentification Multifacteur sur l’accès.
3. Lorsque les utilisateur hello à partir de la société B tente de tooaccess application *Foo* entreprise hello un client, ils sont demandé toocomplete une stimulation d’authentification Multifacteur.
4. Hello utilisateur permettre définir leur MFA avec la société A et choisit l’option de l’authentification Multifacteur.
5. Ce scénario fonctionne pour n’importe quelle identité (Azure AD ou MSA, par exemple, si les utilisateurs dans la société B s’authentifient à l’aide de leur ID social)
6. La société A doit avoir suffisamment de licences Azure AD Premium qui prennent en charge l’authentification multifacteur. utilisateur Hello à partir de la société B utilise cette licence à partir de la société A.

architecture mutualisée invitant à Hello est toujours chargée pour l’authentification Multifacteur pour les utilisateurs à partir de l’organisation partenaire de hello, même si l’organisation partenaire de hello possède des fonctionnalités d’authentification Multifacteur.

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a>Configuration de MFA pour les utilisateurs de B2B Collaboration
toodiscover facilement se tooset de l’authentification Multifacteur pour les utilisateurs de collaboration B2B, consultez Comment procéder hello suite vidéo :

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a>Expérience MFA d'utilisation de l'invitation par des utilisateurs B2B
Passez en revue hello suivant l’expérience de remboursement animation toosee hello :

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a>Réinitialisation de l'authentification MFA pour les utilisateurs de B2B de Collaboration
Actuellement, hello admin peut requérir B2B collaboration utilisateurs tooproof place à nouveau uniquement à l’aide de hello suivant d’applets de commande PowerShell :

1. Se connecter tooAzure AD

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. Obtenir tous les utilisateurs avec des méthodes d'authentification

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  Voici un exemple :

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. Redéfinir la méthode d’authentification Multifacteur hello pour un utilisateur spécifique toorequire hello B2B collaboration utilisateur tooset preuve méthodes. Exemple :

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a>Pourquoi effectuer l’authentification Multifacteur à l’architecture mutualisée de ressource hello ?

Dans la version actuelle de hello, l’authentification Multifacteur est toujours dans l’architecture mutualisée de ressource hello, pour des raisons de prévisibilité. Par exemple, un utilisateur de Contoso (Sarah) est tooFabrikam invité et Fabrikam a activé l’authentification Multifacteur pour les utilisateurs de B2B.

Si Contoso utilise la stratégie d’authentification Multifacteur activée pour App1 mais pas App2, puis si nous examinons hello revendication Contoso MFA dans le jeton de hello, nous pouvons voir hello suivant le problème :

* Jour 1 : un utilisateur dispose de l’authentification multifacteur dans Contoso et accède à App1, mais aucune invite MFA supplémentaire ne s’affiche dans Fabrikam.

* Le jour 2 : hello accès utilisateur 2 application chez Contoso, maintenant lorsque vous accédez à Fabrikam, ils doivent s’inscrire pour l’authentification Multifacteur il.

Ce processus peut prêter à confusion et risque de toodrop de connexion réussies.

En outre, même si Contoso possède la capacité de l’authentification Multifacteur, il n'est pas toujours Bonjour cas Bonjour Fabrikam serait confiance hello stratégie Contoso MFA.

Enfin, l’authentification MFA du locataire de la ressource fonctionne également pour les MSA et les ID sociaux ainsi que pour les organisations partenaires au sein desquelles l’authentification MFA n’est pas configurée.

Par conséquent, la recommandation hello pour l’authentification Multifacteur pour les utilisateurs de B2B est tooalways exiger l’authentification Multifacteur Bonjour inviter les clients. Cette exigence peut entraîner des toodouble l’authentification Multifacteur dans certains cas, mais chaque fois que l’accès aux locataires d’invitation hello, l’expérience des utilisateurs finaux hello est prévisible : Catherine doit inscrire pour l’authentification Multifacteur avec le client d’invitation hello.

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a>Accès conditionnel en fonction des appareils, des emplacements et des risques pour les utilisateurs B2B

Lorsque Contoso Active des stratégies d’accès conditionnel basés sur un appareil pour leurs données d’entreprise, l’accès est bloqué dans les appareils qui ne sont pas gérés par Contoso et non conformes avec les stratégies d’appareil Contoso hello.

Si l’appareil de l’utilisateur hello B2B n’est pas géré par Contoso, l’accès des utilisateurs B2B des organisations partenaires de hello est bloquée dans le contexte de ces stratégies sont appliquées. Toutefois, Contoso peut créer d’exclusion listes contenant partenaire utilisateurs tooexclude de hello stratégie d’accès conditionnel basés sur l’appareil.

#### <a name="location-based-conditional-access-for-b2b"></a>Accès conditionnel en fonction des emplacements pour B2B

Stratégies d’accès conditionnel emplacement peuvent être appliquées pour les utilisateurs de B2B si l’organisation d’invitation hello est en mesure de toocreate une plage d’adresses IP approuvée qui définit leurs organisations partenaires.

#### <a name="risk-based-conditional-access-for-b2b"></a>Accès conditionnel en fonction des risques pour B2B

Actuellement, des risques connectez-vous stratégies ne peut pas être appliqué tooB2B utilisateurs, car l’évaluation des risques hello est effectuée au niveau de l’organisation d’origine de l’utilisateur hello B2B.

## <a name="next-steps"></a>Étapes suivantes

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
* [Ajouter des utilisateurs B2B Collaboration sans invitation](active-directory-b2b-add-user-without-invite.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
