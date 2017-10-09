---
title: "aaaLearn sur les protocoles d’autorisation hello pris en charge par Azure AD v2.0 | Documents Microsoft"
description: Un guide tooprotocols pris en charge par le point de terminaison v2.0 hello Azure AD.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f90511b1880ff223f725c1f79df9f79bddccc7bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Protocoles v2.0 - OAuth 2.0 et OpenID Connect
point de terminaison Hello v2.0 permettre utiliser Azure AD pour l’identité-as-a-service avec des protocoles standard, OpenID Connect et OAuth 2.0.  Alors que le service de hello est conforme aux normes, il peut y avoir des différences subtiles entre les deux implémentations de ces protocoles.  informations Hello ici sera utiles si vous choisissez toowrite votre code en envoyant directement et la gestion des requêtes HTTP ou utilisez un 3e partie ouvrir la bibliothèque de source, au lieu d’utiliser un de nos bibliothèques open source.
<!-- TODO: Need link toolibraries above -->

> [!NOTE]
> Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.  toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
>
>

## Hello notions de base
Dans presque tous les flux OAuth et OpenID Connect, il existe quatre parties impliquées dans l’échange de hello :

![Rôles OAuth 2.0](../../media/active-directory-v2-flows/protocols_roles.png)

* Hello **serveur d’autorisation** est le point de terminaison hello v2.0.  Il est chargé de garantir l’identité de l’utilisateur hello, octroi et révocation d’accès tooresources émission de jetons.  Il est également connue sous le fournisseur d’identité hello - elle traite de manière sécurisée tout élément toodo avec l’utilisateur hello plus d’informations, leur accès et des relations d’approbation entre les parties dans un flux hello.
* Hello **propriétaire de la ressource** est généralement l’utilisateur final hello.  Il s’agit de tiers hello qui possède les données hello et a hello power tooallow tiers tooaccess ces données, ou la ressource.
* Hello **OAuth Client** est votre application, identifiée par son ID d’Application.  Il est généralement hello tiers que l’utilisateur final hello interagit avec, et elle demande des jetons hello serveur d’autorisation.  client de Hello doit pouvoir autorisation tooaccess hello ressource par le propriétaire de la ressource hello.
* Hello **serveur de ressources** où réside hello ressource ou données.  Il approuve hello serveur d’autorisation toosecurely authentifier et autoriser des hello OAuth Client et utilise le support tooensure access_tokens qui accèdent aux ressources de tooa peut être accordée.

## Inscription d’application
Chaque application qui utilise le point de terminaison hello v2.0 doit toobe enregistré auprès de [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) avant qu’elle peut interagir à l’aide d’OAuth ou OpenID Connect.  processus d’inscription d’application Hello collecter & affecter l’application de tooyour quelques valeurs :

* un **ID d’application** qui identifie de manière unique votre application ;
* A **URI de redirection** ou **identificateur de Package** qui peut être utilisé toodirect réponses arrière tooyour application
* quelques valeurs spécifiques au scénario.

Pour plus d’informations, découvrez comment trop[inscrire une application](active-directory-v2-app-registration.md).

## Points de terminaison
Une fois inscrit, application hello communique avec Azure AD en envoyant des requêtes toohello v2.0 point de terminaison :

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Où hello `{tenant}` peut prendre une des quatre valeurs différentes :

| Valeur | Description |
| --- | --- |
| `common` |Permet aux utilisateurs avec des comptes personnels Microsoft et comptes de travail/school à partir d’Azure Active Directory toosign dans l’application hello. |
| `organizations` |Autorise uniquement les utilisateurs avec des comptes de travail/school à partir d’Azure Active Directory toosign dans l’application hello. |
| `consumers` |Autorise uniquement les utilisateurs avec personnel toosign de comptes (MSA) de Microsoft dans l’application hello. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` |Autorise uniquement les utilisateurs avec des comptes de travail/school à partir d’un toosign de locataire Azure Active Directory particulier dans une application hello.  Nom de domaine convivial hello de hello locataire Azure AD ou identificateur de guid du locataire hello peut être utilisé. |

Pour plus d’informations sur la façon de toointeract avec ces points de terminaison, choisissez un type particulier d’application ci-dessous.

## Jetons
implémentation de v2.0 Hello de OAuth 2.0 et OpenID Connect utilisent beaucoup de jetons de support, y compris les jetons de support représentés comme jetons Web JSON. Un jeton de support est un jeton de sécurité léger qu’accorde hello tooa d’accès « support » une ressource protégée. Dans ce sens, hello « support » est une partie capable de présenter le jeton de hello. Si un tiers doit s’authentifier avec un jeton de support pour Azure AD tooreceive hello, si nécessaire de hello étapes ne sont pas prises jeton de hello toosecure de transmission et de stockage, il peut être interceptée et utilisée par une partie indésirable. Bien que certains jetons de sécurité intègrent un mécanisme de protection contre l’utilisation par des parties non autorisées, les jetons porteurs n’en sont pas dotés et doivent donc être acheminés sur un canal sécurisé, par exemple à l’aide du protocole TLS (HTTPS). Si un jeton de support est transmis en clair de hello, une attaque hello man-in peut être utilisé par un jeton de hello tooacquire partie malveillante et l’utiliser pour une ressource tooa protégée de tout accès non autorisé. Bonjour les mêmes principes de sécurité s’appliquent lors du stockage ou la mise en cache des jetons de support pour une utilisation ultérieure. Veillez systématiquement à ce que votre application transmette et stocke les jetons porteurs de manière sécurisée. Pour en savoir plus sur les aspects de sécurité des jetons porteurs, consultez [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750).

En savoir plus sur différents types de jetons sont utilisés dans le point de terminaison hello v2.0 est disponible dans [hello référence de jeton de point de terminaison v2.0](active-directory-v2-tokens.md).

## Protocoles
Si vous êtes prêt toosee quelques exemples de demandes, prise en main une Hello ci-dessous didacticiels.  Chacun d’eux correspond scénario d’authentification particulier tooa.  Si vous avez besoin d’aide pour déterminer ce qui est le flux de droite hello pour vous, consultez [hello des types d’applications que vous pouvez générer avec hello v2.0](active-directory-v2-flows.md).

* [Génération d’une application mobile et native avec OAuth 2.0](active-directory-v2-protocols-oauth-code.md)
* [Génération d’applications web avec Open ID Connect](active-directory-v2-protocols-oidc.md)
* [Créer des applications de Page unique avec hello flux implicite d’OAuth 2.0](active-directory-v2-protocols-implicit.md)
* [Générer les démons ou processus du côté serveur avec hello flux d’informations d’identification Client OAuth 2.0](active-directory-v2-protocols-oauth-client-creds.md)
* [Obtenir des jetons dans une API Web avec hello OAuth 2.0 de la part de flux](active-directory-v2-protocols-oauth-on-behalf-of.md)
