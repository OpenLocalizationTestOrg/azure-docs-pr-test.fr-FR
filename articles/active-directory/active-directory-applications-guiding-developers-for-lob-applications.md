---
title: les applications pour Azure AD aaaDevelop | Des documents Microsoft
description: "Rédigée pour les professionnels de l’informatique de hello, cet article fournit des instructions pour l’intégration d’applications Azure avec Active Directory."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a>Développer des applications métier pour Azure Active Directory
Ce guide fournit une vue d’ensemble du développement d’applications line-of-business (LoB) Azure Active Directory (AD) .hello destinée audience est un administrateur global Active Directory/Office 365.

## <a name="overview"></a>Vue d'ensemble
La création d’applications intégrées à Azure AD permet aux utilisateurs de votre organisation de bénéficier de l’authentification unique avec Office 365. Ayant l’application hello dans Azure AD vous permet de que contrôler la stratégie d’authentification pour l’application hello hello. toolearn plus d’informations sur l’accès conditionnel et comment les applications tooprotect avec l’authentification multifacteur (MFA), consultez [règles d’accès de configuration](active-directory-conditional-access-azuread-connected-apps.md).

Inscrire votre toouse application Azure Active Directory. L’inscription d’application hello signifie que les développeurs peuvent utiliser Azure AD tooauthenticate utilisateurs et demander des ressources de toouser d’accès telles que la messagerie, de calendrier et de documents.

Tout membre de votre annuaire (pas les invités) peut inscrire une application, procédé également appelé *création d’un objet d’application*.

Inscription d’une application permet à toutes les de hello toodo utilisateur :

* Obtenir pour son application une identité reconnue par Azure AD.
* Obtenir un ou plusieurs secrets/clés hello application peut utiliser tooauthenticate lui-même tooAD
* Application hello marque dans le portail Azure avec un nom personnalisé, le logo, etc. de hello.
* Appliquer l’application de tootheir fonctionnalités Azure AD d’autorisation, y compris :

  * Contrôle d’accès en fonction du rôle
  * Azure Active Directory en tant que serveur d’autorisation oAuth (sécuriser une API exposée par l’application hello)
* Déclarer les autorisations requises nécessaires pour hello application toofunction comme prévu, y compris :

      - Autorisations de l’application (administrateurs généraux uniquement). Par exemple : l’appartenance au rôle dans un autre Azure Active Directory application ou du rôle d’appartenance relative tooan ressource, groupe de ressources Azure, ou un abonnement
      - Autorisations déléguées (tout utilisateur). Par exemple : Azure AD, connexion et lecture de profil

> [!NOTE]
> Par défaut, tout membre peut inscrire une application. toolearn toorestrict les autorisations pour l’inscription des membres de toospecific d’applications, voir [comment les applications sont ajoutées tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).
>
>

Voici ce que vous, administrateur global de hello, doivent toodo toohelp les développeurs rendre leur application prête pour la production :

* Configurer des règles d’accès (stratégie d’accès/MFA)
* Configurer l’affectation d’utilisateurs toorequire application hello et affecter des utilisateurs
* Supprimer l’expérience de consentement utilisateur hello par défaut

## <a name="configure-access-rules"></a>Configurer des règles d’accès
Configurer l’accès par application règles tooyour SaaS applications. Par exemple, vous pouvez exiger l’authentification Multifacteur ou autoriser uniquement les accès toousers sur des réseaux approuvés. Détails de Hello pour ce sont disponibles dans le document de hello [règles d’accès de configuration](active-directory-conditional-access-azuread-connected-apps.md).

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a>Configurer l’affectation d’utilisateurs toorequire application hello et affecter des utilisateurs
Par défaut, les utilisateurs peuvent accéder aux applications sans affectation. Toutefois, si l’application hello expose des rôles, ou si vous souhaitez tooappear d’application hello sur le volet d’accès d’un utilisateur, vous devez demander l’affectation d’utilisateurs.

[Demande de l’affectation de l’utilisateur](active-directory-applications-guiding-developers-requiring-user-assignment.md)

Si vous êtes abonné à Azure AD Premium ou Enterprise Mobility Suite (EMS), nous vous recommandons fortement d’utiliser les groupes. Affectation de groupes toohello application vous permet de propriétaire de toohello toodelegate accès permanent de gestion de groupe de hello. Vous pouvez créer le groupe de hello ou demander la partie responsable de hello dans votre organisation toocreate hello du groupe à l’aide du centre de gestion de groupe.

[Affectation d’utilisateurs tooan application](active-directory-applications-guiding-developers-assigning-users.md)  
[Affectation de groupes tooan application](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a>Supprimer le consentement de l’utilisateur
Par défaut, chaque utilisateur traverse un toosign d’expérience de consentement dans. expérience de consentement Hello, demandant aux utilisateurs des autorisations toogrant tooan application, peut être déconcertant pour les utilisateurs qui ne sont pas familiarisés avec ces décisions.

Pour les applications de confiance, vous pouvez simplifier l’expérience utilisateur hello par terme autorisation toohello application pour votre organisation.

Pour plus d’informations sur le consentement de l’utilisateur et de consentement de hello expérience dans Azure, consultez [intégration d’Applications avec Azure Active Directory](active-directory-integrating-applications.md).

## <a name="related-articles"></a>Articles connexes
* [Permettre aux applications tooon local de sécuriser l’accès à distance avec le Proxy d’Application Azure AD](active-directory-application-proxy-get-started.md)
* [Vue d’ensemble de l’accès conditionnel Azure pour les applications SaaS](active-directory-conditional-access-azuread-connected-apps.md)
* [Gestion des tooapps d’accès auprès d’Azure AD](active-directory-managing-access-to-apps.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
