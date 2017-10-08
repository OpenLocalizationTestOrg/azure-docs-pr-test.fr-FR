---
title: "Azure Active Directory B2C : Protocoles d’authentification | Microsoft Docs"
description: "Comment les applications toobuild directement à l’aide hello protocoles sont pris en charge par Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5e407d0a-73a2-4d74-ac81-3aa6c31ddcee
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8fa4cbebe711841d410b3ae43b78f893c06d9b63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Azure AD B2C : protocoles d’authentification
Azure Active Directory B2C (Azure AD B2C) fournit l’identité en tant que service pour vos applications en prenant en charge deux protocoles standard, OpenID Connect et OAuth 2.0. service de Hello est conforme aux normes, mais les deux implémentations de ces protocoles peuvent présenter des différences subtiles. 

informations Hello dans ce guide sont utiles si vous écrivez votre code en envoyant directement et en gérant les requêtes HTTP, plutôt qu’à l’aide d’une bibliothèque open source. Nous vous recommandons de lire cette page avant de vous plonger dans les détails de hello de chaque protocole spécifique. Mais si vous êtes déjà familiarisé avec Azure AD B2C, vous pouvez accéder directement trop[hello guides de référence de protocole](#protocols).

<!-- TODO: Need link toolibraries above -->

## principes de base Hello
Chaque application qui utilise Azure AD B2C doit toobe inscrit dans le répertoire B2C hello [portail Azure](https://portal.azure.com). processus d’inscription d’application Hello collecte et affecte l’application de tooyour quelques valeurs :

* un **ID d’application** qui identifie de manière unique votre application ;
* A **URI de redirection** ou **identificateur du package** qui peut être utilisé toodirect réponses arrière tooyour application.
* quelques valeurs spécifiques au scénario. Pour plus d’informations, Découvrez [comment tooregister votre application](active-directory-b2c-app-registration.md).

Après avoir inscrit votre application, il communique avec Azure Active Directory (Azure AD) en envoyant les demandes toohello point de terminaison :

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Dans presque tous les flux OAuth et OpenID Connect, les quatre parties sont impliquées dans l’échange de hello :

![Rôles OAuth 2.0](./media/active-directory-b2c-reference-protocols/protocols_roles.png)

* Hello **serveur d’autorisation** est le point de terminaison hello Azure AD. Il traite de manière sécurisée tout connexes toouser informations et l’accès. Il gère également les relations d’approbation hello entre les parties hello dans un flux. Il est chargé de vérifier l’identité de l’utilisateur hello, accorder et révoquer l’accès tooresources émission de jetons. Il est également connu sous le fournisseur d’identité hello.

* Hello **propriétaire de la ressource** est généralement hello utilisateur final. Il est tiers hello qui possède les données hello, et il a hello power tooallow tiers tooaccess données ou la ressource.

* Hello **client OAuth** est votre application. Il est identifié par son ID d’application. Il est généralement tiers hello interagissant avec les utilisateurs finaux. Il demande également les jetons hello serveur d’autorisation. propriétaire de la ressource Hello doit accorder hello client autorisation tooaccess hello ressource.

* Hello **serveur de ressources** où réside hello ressource ou données. Il fait confiance à l’autorisation de hello server toosecurely authentifier et autoriser des clients OAuth de hello. Il utilise également accès au porteur tooensure de jetons qui accèdent aux ressources de tooa peut être accordée.

## Stratégies
Sans doute, Azure AD B2C stratégies sont hello principales fonctionnalités de service de hello. Azure AD B2C étend hello OAuth 2.0 et OpenID Connect des protocoles standard en introduisant des stratégies. Azure AD B2C tooperform permettent bien plus simple d’authentification et d’autorisation. 

Les stratégies décrivent entièrement les expériences liées à l’identité du consommateur, telles que l’inscription, la connexion et la modification de profil. Elles peuvent être définies dans une interface utilisateur d’administration et exécutées à l’aide d’un paramètre de requête spécial dans les requêtes d’authentification HTTP. 

Les stratégies ne sont pas des fonctionnalités standard de OAuth 2.0 et OpenID Connect, donc vous devez prendre hello temps toounderstand les. Pour plus d’informations, consultez hello [guide de référence de stratégie de Azure AD B2C](active-directory-b2c-reference-policies.md).

## Jetons
implémentation de Hello Azure AD B2C de OAuth 2.0 et OpenID Connect exploite pleinement les jetons de support, y compris les jetons de support représentés comme des jetons web JSON (Jwt). Un jeton de support est un jeton de sécurité léger qu’accorde hello tooa d’accès « support » une ressource protégée.

support de Hello est n’importe quelle partie peut présenter le jeton de hello. Une partie doit d’abord s’authentifier auprès d’Azure AD pour recevoir un jeton du porteur, Mais si hello nécessaire étapes ne sont pas prises jeton de hello toosecure de transmission et de stockage, il peut être intercepté et utilisé par une partie indésirable.

Bien que certains jetons de sécurité intègrent des mécanismes de protection contre l’utilisation par des parties non autorisées, les jetons du porteur n’en sont pas dotés et ils doivent donc être acheminés sur un canal sécurisé, par exemple à l’aide du protocole TLS (HTTPS). 

Si un jeton de support est transmis à l’extérieur d’un canal sécurisé, une personne malveillante peut utiliser un jeton de hello tooacquire attaque de man-in-the-middle et utiliser la ressource de tooa protégé accès toogain non autorisé. Bonjour les mêmes principes de sécurité s’appliquent lorsque des jetons de support sont stockés ou mis en cache pour une utilisation ultérieure. Veillez systématiquement à ce que votre application transmette et stocke les jetons porteurs de manière sécurisée.

Pour connaître d’autres aspects de la sécurité des jetons du porteur, consultez [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750).

Plus d’informations sur hello différents types de jetons qui sont utilisés dans Azure AD B2C sont disponibles dans [hello référence de jeton Azure AD](active-directory-b2c-reference-tokens.md).

## Protocoles
Lorsque vous êtes prêt tooreview quelques exemples des demandes, vous pouvez démarrer avec l’un des hello suivant des didacticiels. Scénario d’authentification particulier tooa correspondent. Si vous avez besoin d’aide pour déterminer le flux vous convient, consultez [hello des types d’applications, vous pouvez créer à l’aide d’Azure AD B2C](active-directory-b2c-apps.md).

* [Génération d’une application mobile et native avec OAuth 2.0](active-directory-b2c-reference-oauth-code.md)
* [Génération d’applications web avec Open ID Connect](active-directory-b2c-reference-oidc.md)
* [Créer des applications de page unique à l’aide de flux implicites de hello OAuth 2.0](active-directory-b2c-reference-spa.md)

