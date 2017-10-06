---
title: "les comptes d’aaaSharing à l’aide d’Azure AD | Documents Microsoft"
description: "Décrit comment Azure Active Directory permet aux organisations toosecurely partager des comptes pour les applications locales et les services de cloud computing de consommateur."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Partage de comptes avec Azure AD
## <a name="overview"></a>Vue d'ensemble
Parfois, les organisations doivent toouse un nom d’utilisateur unique et un mot de passe pour plusieurs personnes. Cela se produit généralement dans deux cas :

* Au moment d’accéder à des applications qui nécessitent un nom d’utilisateur et un mot de passe uniques pour chaque utilisateur, qu’il s’agisse d’applications locales ou de services cloud grand public (tels que les comptes de réseaux sociaux d’entreprise).
* Pendant la création d’environnements multi-utilisateurs. Vous pouvez avoir un compte local qui dispose de privilèges élevés et pouvez être utilisé toodo activités principales le programme d’installation, d’administration et de récupération (par exemple hello local » « compte d’administrateur général pour Office 365 ou hello compte root dans Salesforce).

En règle générale, ces comptes seraient partagés par les bonnes personnes hello informations d’identification (nom d’utilisateur/mot de passe) toohello de distribution ou de les stocker dans un emplacement partagé dans lequel plusieurs approuvé agents peuvent y accéder.

modèle de partage traditionnel Hello présente plusieurs inconvénients :

* Permet aux applications de toonew accès requiert que vous tooeveryone d’informations d’identification toodistribute qui a besoin d’accéder.
* Chaque application partagée peut nécessiter de son propre jeu d’informations d’identification partagées, nécessitant des utilisateurs tooremember plusieurs jeux d’informations d’identification. Lorsque les utilisateurs disposent des informations d’identification de nombreuses tooremember, risque de hello augmente qu’ils seront recours toorisky pratiques. notamment l’écriture des mots de passe.
* Vous ne savez pas qui a accès tooan application.
* Vous ne pouvez pas savoir qui a *accédé* à une application.
* Lorsque vous avez besoin d’application de tooan tooremove access, vous disposer des informations d’identification de tooupdate hello et redistribuer les tooeveryone qui doit accéder à application de toothat.

## <a name="azure-active-directory-account-sharing"></a>Partage de compte Azure Active Directory
Azure AD fournit une nouvelle approche de comptes toousing partagé qui élimine ces inconvénients.

administrateur d’Azure AD Hello configure les applications d’un utilisateur peut accéder à l’aide de hello volet d’accès et en choisissant de type hello de l’authentification unique sur mieux adaptée pour cette application. Un de ces types, *mot de passe d’authentification unique*, Azure AD vous permet d’agir comme une sorte de « broker » au cours du processus hello d’authentification pour cette application.

Les utilisateurs se connectent une fois avec leur compte professionnel. Il s’agit de hello même compte qu’elles utilisent régulièrement tooaccess leur bureau ou un e-mail. Ils peuvent découvrir les applications auxquelles ils sont affectés et accéder uniquement à celles-ci. Grâce aux comptes partagés, cette liste d’applications peut inclure un nombre quelconque d’informations d’identification partagées. utilisateur final de Hello ne devez tooremember ou écrivez hello différents comptes qu’ils peuvent être à l’aide.

Outre accroître la supervision et améliorer la facilité d’utilisation, les comptes partagés renforcent votre sécurité. Mot de passe partagé hello ne voyez pas les utilisateurs disposant des informations d’identification d’autorisations toouse hello, mais au lieu de cela obtenir le mot de passe autorisations toouse hello en tant que partie d’un flux d’authentification orchestré. En outre, avec certaines applications de l’authentification unique de mot de passe, vous avez hello option toohave Azure AD régulièrement substitution (update) hello mot de passe à l’aide de mots de passe complexe, augmenter la sécurité du compte hello. administrateur de Hello peut facilement accorder ou révoquer l’accès tooan application et également de savoir qui a accès toohello compte et qui l’a consulté Bonjour passées.

Azure AD prend en charge les comptes partagés pour tous les utilisateurs détenteurs d’une licence Enterprise Mobility Suite (EMS), Premium ou De base, quel que le soit le type d’applications d’authentification unique avec mot de passe. Vous pouvez partager des comptes pour une des milliers d’applications pré-intégrées dans la galerie d’applications hello et que vous pouvez ajouter votre propre application d’authentification de mot de passe avec [applications SSO personnalisées](active-directory-sso-integrate-saas-apps.md).

Les fonctionnalités Azure AD qui permettent le partage de compte sont les suivantes :

* [Authentification unique avec mot de passe](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Agent d’authentification unique avec mot de passe
* [Affectation de groupe](active-directory-accessmanagement-self-service-group-management.md)
* Applications de mot de passe personnalisé
* [Tableau de bord/rapports d’utilisation des applications](active-directory-passwords-get-insights.md)
* Portails d’accès des utilisateurs finaux
* [Proxy d’application](active-directory-application-proxy-get-started.md)
* [Marketplace Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a>Partage d’un compte
toouse Azure AD tooshare un compte vous devez :

* Ajouter une application à la [galerie d’applications](https://azure.microsoft.com/marketplace/active-directory/) ou aux [applications personnalisées](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).
* Configurer une application hello pour le mot de passe Single Sign-On (SSO)
* Utilisez [affectation basée sur le groupe](active-directory-accessmanagement-group-saasapps.md) et sélectionnez hello tooenter de l’option informations d’identification partagées
* Facultatif : dans certaines applications, tels que Facebook, Twitter et LinkedIn, vous pouvez activer option hello pour [Azure AD automatisée retournement de mot de passe](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

Vous pouvez également sécuriser votre compte partagé avec multi-Factor Authentication (MFA) (en savoir plus sur [sécurisation des applications avec Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) et vous pouvez déléguer toomanage de capacité hello qui a accès à des applications toohello à l’aide [Azure AD libre-service](active-directory-accessmanagement-self-service-group-management.md) gestion de groupe.

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Protection des applications avec accès conditionnel](active-directory-conditional-access.md)
* [Gestion des groupes en libre service/accès aux applications en libre-service](active-directory-accessmanagement-self-service-group-management.md)

