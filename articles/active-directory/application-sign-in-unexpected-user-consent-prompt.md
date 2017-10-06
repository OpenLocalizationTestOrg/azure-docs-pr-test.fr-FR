---
title: "invite de consentement aaaUnexpected pour se connecter à l’application de tooan | Documents Microsoft"
description: "Comment tootroubleshoot lorsqu’un utilisateur voit une invite de consentement pour une application que vous avez intégré à Azure AD que vous n’avez pas prévues"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>Invite de consentement inattendue lors de la connexion tooan application

De nombreuses applications qui s’intègrent à Azure Active Directory nécessitent des ressources autorisations toovarious toorun d’ordre. Lorsque ces ressources sont également intégrées dans Azure Active Directory, tooaccess autorisations leur est demandé à l’aide d’Azure AD de hello consentement framework. 

Cela entraîne une invite de consentement affichée hello première fois, qu'une application est utilisée, ce qui est souvent une opération unique. 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>Scénarios dans lesquels des invites de consentement sont présentées aux utilisateurs

Divers scénarios entraînent l’affichage d’invites supplémentaires :

* ensemble de Hello des autorisations requises par l’application hello ont été modifiés.

* utilisateur Hello qui a donné son consentement à l’origine des toohello application n’était pas un administrateur, et désormais un utilisateur différent (non-admin) utilise application hello pour hello première fois.

* utilisateur Hello qui a donné son consentement à l’origine des toohello application était un administrateur, mais elles ne pas consentement à la place de l’ensemble de l’organisation hello.

* à l’aide d’application Hello [consentement incrémentielle et dynamique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest des autorisations supplémentaires une fois le consentement a été initialement accordé. Ce cas de figure se présente souvent quand les fonctionnalités facultatives d’une application nécessitent des autorisations au-delà de celles exigées pour les fonctionnalités de base.

* Le consentement, bien qu’initialement accordé, a été révoqué.

* développeur de Hello a configuré hello application toorequire une invite de consentement chaque fois qu’elle est utilisée (Remarque : cela n’est pas recommandé).

## <a name="next-steps"></a>Étapes suivantes

-   [Applications, autorisations et consentement dans Azure Active Directory (point de terminaison v1.0)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [Les étendues, les autorisations et consentement Bonjour Azure Active Directory (point de terminaison v2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


