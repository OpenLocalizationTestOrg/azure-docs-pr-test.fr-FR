---
title: "flux d’octroi d’aaaUnderstanding hello OAuth2 implicite dans Azure AD | Documents Microsoft"
description: "En savoir plus sur l’implémentation d’Azure Active Directory de flux d’octroi implicite d’hello OAuth2, et s’il est adapté aux besoins de votre application."
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 90e42ff9-43b0-4b4f-a222-51df847b2a8d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/15/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 3402e6619709e1a5b1e790ffd79dc62139552d9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-oauth2-implicit-grant-flow-in-azure-active-directory-ad"></a>Hello de présentation OAuth2 implicite accorder des flux dans Azure Active Directory (AD)
Octroi implicite de Hello OAuth2 est connu pour être grant hello avec liste plus longue de hello de problèmes de sécurité dans la spécification de OAuth2 hello. Et encore, qui est l’approche hello implémentée par ADAL JS et hello une que nous recommandons lors de l’écriture d’applications de SPA. Quelle en est la raison ? Il est une question de compromis : et il s’avère, octroi implicite de hello est hello meilleure approche que vous pouvez poursuivre pour les applications qui utilisent une API Web via JavaScript à partir d’un navigateur.

## <a name="what-is-hello-oauth2-implicit-grant"></a>Nouveautés octroi implicite de hello OAuth2
Hello Finances [octroi d’un code d’autorisation OAuth2](https://tools.ietf.org/html/rfc6749#section-1.3.1) est hello d’autorisation grant, qui utilise deux points de terminaison distincts. point de terminaison d’autorisation Hello est utilisé pour la phase d’interaction utilisateur hello, ce qui entraîne un code d’autorisation. point de terminaison token Hello est ensuite utilisé par les clients hello pour l’échange de code hello pour un jeton d’accès et souvent un jeton d’actualisation. Les applications Web est requis toopresent leur propres informations d’identification toohello jeton point de terminaison application, afin que hello serveur d’autorisation peut authentifier hello client.

Hello [octroi implicite d’OAuth2](https://tools.ietf.org/html/rfc6749#section-1.3.2) est une variante d’autres allocations d’autorisation. Il permet une tooobtain client un jeton d’accès (et id_token, lorsque vous utilisez [OpenId Connect](http://openid.net/specs/openid-connect-core-1_0.html)) directement à partir de hello point de terminaison, sans contacter le point de terminaison token hello ni l’authentification hello client. Cette variante a été spécialement conçue pour les applications qui s’exécutent dans un navigateur Web basé sur JavaScript : dans la spécification d’OAuth2 hello d’origine, les jetons sont retournés dans un fragment d’URI. Qui rend les bits jeton hello toohello disponibles du code JavaScript dans le client de hello, mais elle garantit qu’ils ne seront pas incluses dans les redirections vers le serveur de hello. Retour de jetons via un navigateur redirige directement à partir de point de terminaison d’autorisation hello. Il présente également l’avantage de hello d’éliminer les conditions requises pour des appels d’origine, qui sont nécessaires si hello application JavaScript est le point de terminaison de jeton de hello toocontact requis inter.

Des caractéristiques importantes de la quantité de hello OAuth2 implicite sont faits hello tels flux ne renvoient jamais actualisation jetons toohello client. Comme nous le verrons dans la section suivante de hello, qui n’est pas vraiment nécessaire et est en fait un problème de sécurité.

## <a name="suitable-scenarios-for-hello-oauth2-implicit-grant"></a>Accorder des scénarios pour hello OAuth2 implicite
Comme hello OAuth2 spécification déclare, hello octroi implicite a été tooenable étude agent utilisateur applications – est toosay, les applications JavaScript qui s’exécutent dans un navigateur. Hello définissant les caractéristiques de ces applications est que le code JavaScript est utilisé pour accéder aux ressources du serveur (en général, une API Web) et mise à jour de l’application hello UX en conséquence. Pensez à des applications telles que Gmail ou Outlook Web Access : lorsque vous sélectionnez un message dans votre boîte de réception, le message de type hello seul volet de visualisation change toodisplay hello nouvelle sélection, tandis que hello de page de hello reste inchangé. Ceci est le contraire traditionnel basée sur la redirection des applications Web, où les résultats de chaque interaction utilisateur dans une publication de la page entière et un rendu de page entière de la réponse du serveur nouveau hello.

Les applications qui tirent hello basé sur JavaScript approche tooits extrêmes sont appelées Applications à Page unique, ou SPAs : hello est que ces applications servent uniquement une page HTML initiale et le JavaScript associé, avec toutes les interactions résultantes pilotées par Les appels d’API Web effectués via JavaScript. Toutefois, les approches hybride, où l’application hello est principalement axé sur la publication (postback) mais effectue des appels JS occasionnelles, ne sont pas rares : discussion hello sur l’utilisation de flux implicites ne s’applique à ceux ainsi.

En général, les applications à redirection sécurisent leurs demandes par des cookies. Mais cette approche présente une efficacité limitée pour les applications JavaScript. Les cookies ne fonctionnent par rapport au domaine hello qu'ont été générés, tandis que les appels JavaScript peuvent être dirigés vers d’autres domaines. En fait, qui sera souvent le cas de hello : réflexion d’appel Microsoft Graph API, les API Office, Azure API – résidant tous en dehors du domaine hello où application hello est pris en charge des applications. Tendance pour les applications JavaScript n’est toohave aucun serveur principal, leur fonction d’entreprise de confiance de 100 % 3e tooimplement d’API Web tiers.

Actuellement, hello est préférable d’appels tooa API Web de protection toouse hello OAuth2 PORTEUR jeton approche, où chaque appel est accompagné d’un jeton d’accès OAuth2. Hello Web API examine le jeton d’accès entrant hello et, s’il se trouve dans il hello étendues nécessaires, il accorde un accès toohello l’opération demandée. les flux implicites Hello fournit un mécanisme commode pour les applications JavaScript tooobtain des jetons d’accès pour une API Web, offre de que nombreux avantages dans respectent toocookies :

* Les jetons peuvent être obtenues fiable sans recourir à de cross-origine appels : inscription obligatoire de toowhich d’URI de redirection hello renvoyer des jetons garantit que les jetons ne sont pas déplacées
* Les applications JavaScript peuvent obtenir autant de jetons d’accès que nécessaire, pour un nombre illimité d’API Web ciblées, sans aucune restriction sur les domaines.
* Fonctionnalités HTML5 telles que la session ou de stockage local accorder un contrôle total sur la mise en cache de jeton et de gestion de la durée de vie, tandis que la gestion des cookies est opaque toohello application
* Les jetons d’accès ne sont pas susceptibles d’être tooCross-site demande forgery (CSRF) attaques

flux d’octroi implicite d’Hello n’émet pas de jetons d’actualisation, principalement pour des raisons de sécurité. L’étendue d’un jeton d’actualisation n’est pas aussi étroite que celle des jetons d’accès. Ainsi, un jeton d’actualisation offre une puissance bien supérieure et peut causer des dommages beaucoup plus lourds en cas de fuite. Dans le flux implicite de hello, jetons sont livrés dans l’URL de hello, risque hello d’interception est plus élevé qu’à l’octroi d’un code d’autorisation hello.

Toutefois, notez qu’une application JavaScript a un autre mécanisme à sa disposition pour le renouvellement des jetons d’accès sans demander à plusieurs reprises des informations d’identification utilisateur hello. Hello application peut utiliser un iframe masqué tooperform nouvelles demandes de jeton sur le point de terminaison hello d’autorisation d’Azure AD : tant que navigateur de hello a toujours une session active (lire : a un cookie de session) par rapport au domaine de hello Azure AD, hello demande d’authentification peut se produire avec succès sans aucune intervention de l’utilisateur.

Ce modèle autorise hello JavaScript application hello tooindependently renouvellement des jetons d’accès et acquérir même nouvelles pour une nouvelle API (à condition que hello utilisateur déjà consenti pour eux. Cela évite de hello charge de travail supplémentaire lors de l’acquisition, la maintenance et la protection d’un artefact de valeur élevée comme un jeton d’actualisation. Hello artefact ce qui rend le renouvellement silencieuse hello possible, le cookie de session hello Azure AD est gérée en dehors de l’application hello. Un autre avantage de cette approche est qu'un utilisateur peut se déconnecter d’Azure AD, à l’aide de n’importe quelle application hello connectée à Azure AD, en cours d’exécution dans un des onglets de navigateur hello. Cela entraîne la suppression du cookie de session AD Azure hello hello et hello application JavaScript perdrez automatiquement la possibilité de hello jetons toorenew Pourquoi me déconnecter l’utilisateur.

## <a name="is-hello-implicit-grant-suitable-for-my-app"></a>Convient octroi implicite de hello pour mon application ?
Octroi implicite d’Hello présente des risques plus que d’autres allocations, et les zones hello que vous devez toopay attention tooare est bien documenté. Par exemple, [tooImpersonate utilisation abusive de jeton d’accès propriétaire de la ressource dans le flux implicite] [ OAuth2-Spec-Implicit-Misuse] et [modèle des menaces OAuth 2.0 et les considérations de sécurité] [ OAuth2-Threat-Model-And-Security-Implications]). Toutefois, profil de risque plus élevé hello est en grande partie en raison des faits toohello qui sert de tooenable les applications qui s’exécutent de code active, pris en charge par un navigateur de tooa ressource distante. Si vous prévoyez une architecture SPA, n’avoir aucun composant de serveur principal ou envisagez tooinvoke une API Web via JavaScript, l’utilisation de flux implicites de hello pour l’acquisition de jeton est recommandée.

Si votre application est un client natif, les flux implicites hello n’est pas parfait. absence de Hello de cookie de session hello Azure AD dans le contexte de hello d’un client natif PRIVE votre application à partir de moyens hello de maintenir une session de longue durée. Ce qui signifie que votre application à plusieurs reprises invite hello utilisateur lors de l’obtention des jetons d’accès pour les nouvelles ressources.

Si vous développez une application Web qui inclut un serveur principal et l’utilisation d’une API à partir de son code principal, les flux implicites hello ne sont également pas adapté. D’autres modes d’octroi d’autorisation sont beaucoup plus puissants. Par exemple, hello OAuth2 octroi des informations d’identification du client fournit des jetons tooobtain de capacité hello qui correspondent à celles hello affecté toohello application, comme les délégations toouser exécutée. Cela signifie que les clients hello hello capacité toomaintain l’accès par programme tooresources même lorsqu’un utilisateur n’est pas activement dans une session et ainsi de suite. De plus, ces modes d’octroi offrent de meilleurs gages de sécurité. Par exemple, les jetons d’accès jamais de transit via le navigateur d’utilisateur hello, ils ne sont enregistrées dans l’historique du navigateur hello des risques et ainsi de suite. application cliente de Hello peut également effectuer une authentification forte lors de la demande un jeton.

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir une liste complète des ressources de développement, y compris les informations de référence pour la prise en charge de flux par Azure AD, accordent les protocoles de hello et OAuth2 font référence toohello [Guide du développeur Azure AD][AAD-Developers-Guide]
* Consultez [comment toointegrate une application auprès d’Azure AD] [ ACOM-How-To-Integrate] pour la profondeur supplémentaire sur le processus d’intégration application hello.

<!--Image references-->

<!--Reference style links in use-->
[AAD-Developers-Guide]: active-directory-developers-guide.md
[ACOM-How-And-Why-Apps-Added-To-AAD]: active-directory-how-applications-are-added.md
[ACOM-How-To-Integrate]: active-directory-how-to-integrate.md
[OAuth2-Spec-Implicit-Misuse]: https://tools.ietf.org/html/rfc6749#section-10.16
[OAuth2-Threat-Model-And-Security-Implications]: https://tools.ietf.org/html/rfc6819
