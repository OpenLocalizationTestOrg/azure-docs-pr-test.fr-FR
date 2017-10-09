---
title: "applications de tooon local aaaHow tooprovide sécuriser l’accès à distance"
description: "Décrit comment toouse Proxy d’Application Azure AD tooprovide sécuriser l’accès à distance tooyour localement les applications."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 289e970ed0596fcd06ccf6b2ad92203366fbb494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprovide-secure-remote-access-tooon-premises-applications"></a>Comment tooprovide sécuriser l’accès à distance des applications tooon-site

Les employés aujourd'hui veulent toobe productifs en tout lieu, à tout moment et à partir de n’importe quel appareil. Ils veulent toowork sur leurs propres appareils, qu’elle soit tablettes, téléphones portables ou des ordinateurs portables. Et ils envisagent tooaccess en mesure de toobe toutes leurs applications, les applications SaaS dans le cloud de hello et applications d’entreprise en local. En fournissant l’accès des applications tooon site implique en général des réseaux privés virtuels (VPN) ou des zones de démilitarisée (DMZ). Non seulement ces toomake complexe et difficile de solutions ne sont sécurisés, mais ils sont coûteux tooset et gérer.

Il y a une meilleure solution.

Un personnel modern dans mobile-first-hello, world de cloud en premier doit une solution d’accès à distance modernes. Le Proxy d’application Azure AD est une fonctionnalité d’Azure Active Directory qui fournit un accès à distance en tant que service. Cela signifie qu’il est facile toodeploy, utiliser et gérer.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a>Présentation du Proxy d’application Azure Active Directory
Le Proxy d’application Azure AD offre une authentification unique (SSO) et un accès à distance sécurisé pour les applications web hébergées en local. Certaines applications toopublish souhaité incluent des sites SharePoint, Outlook Web Access ou autres applications web métier que vous disposez. Ces web localement les applications sont intégrées à Azure AD, hello même identité et contrôle de plateforme qui est utilisé par Office 365. Les utilisateurs finaux peuvent accéder à votre hello d’applications local même façon de qu'accéder à Office 365 et autres applications SaaS intégrée à Azure AD. Vous ne devez infrastructure de réseau toochange hello ou VPN tooprovide cette solution pour vos utilisateurs.

## <a name="why-is-application-proxy-a-better-solution"></a>Pourquoi le proxy d’application est-il une meilleure solution ?
Proxy d’Application Azure AD fournit un tooall de solution rentable, sécurisée et simple accès à distance vos applications sur site.

Le Proxy d’application Azure AD est :

* **Simple**
   * Vous ne devez toochange ou mettre à jour votre toowork d’applications avec Proxy d’Application. 
   * Vos utilisateurs bénéficient d’une expérience d’authentification cohérente. Ils peuvent utiliser les applications SaaS tooboth hello MyApps tooget portail de l’authentification unique dans le cloud de hello et vos applications locales. 
* **Sécuriser**
   * Lorsque vous publiez vos applications à l’aide du Proxy d’Application Azure AD, vous pouvez tirer parti de contrôles d’autorisation riche hello et analytique de sécurité dans Azure. Vous obtenez une sécurité à l’échelle du cloud et des fonctionnalités de sécurité Azure, telles que l’accès conditionnel et la vérification en deux étapes.
   * Vous n’avez pas tooopen toutes les connexions entrantes via votre toogive pare-feu vos utilisateurs un accès à distance. 
* **Économique**
   * Le Proxy d’application fonctionnant dans le cloud de hello, vous pouvez gagner du temps et argent. En général, solutions locales nécessitent tooset des et maintenir des DMZ, serveurs edge ou autres infrastructures complexes.  

## <a name="what-kind-of-applications-work-with-application-proxy"></a>Quels types d’applications fonctionnent avec le Proxy d’application ?
Avec le Proxy d’application Azure AD, vous pouvez accéder à différents types d’applications internes :

* Applications web qui utilisent [l’authentification Windows intégrée](active-directory-application-proxy-sso-using-kcd.md) pour l’authentification  
* Applications web qui utilisent l’accès [basé sur un en-tête](application-proxy-ping-access.md) ou sur un formulaire  
* Web API que vous voulez que les applications de toorich tooexpose sur différents périphériques  
* Applications hébergées derrière une [passerelle Bureau à distance](application-proxy-publish-remote-desktop.md)  
* Applications clientes riches qui sont intégrées à hello Active Directory Authentication Library (ADAL)

## <a name="how-does-application-proxy-work"></a>Comment fonctionne le Proxy d’application ?
Il existe deux composants que vous avez besoin de tooconfigure toomake travail de Proxy d’Application : un connecteur et un point de terminaison externe. 

connecteur de Hello est un agent léger qui se trouve sur un serveur Windows à l’intérieur de votre réseau. connecteur de Hello facilite hello le flux de trafic à partir de hello service Proxy d’Application hello cloud tooyour application localement. Il utilise uniquement les connexions sortantes, afin que vous n’avez tooopen de ports entrants ou quoi que ce soit placé dans le réseau de périmètre hello. les connecteurs Hello sont sans état et extraient des informations du cloud hello selon les besoins. Pour savoir comment les connecteurs équilibrent la charge ou s’authentifient, voir [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md). 

point de terminaison externe Hello est la façon dont vos utilisateurs atteint vos applications hors de votre réseau. Ils peuvent visiter directement tooan URL externe que vous déterminez, ou ils peuvent accéder à application hello via le portail de MyApps hello. Lorsque les utilisateurs se tooone de ces points de terminaison, ils s’authentifient dans Azure AD et qui sont ensuite routés via une application locale de hello connecteur toohello.

 ![Diagramme du Proxy d’application Azure AD](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. utilisateur de Hello accède à application hello via hello service Proxy d’Application et est tooauthenticate de page de connexion dirigée toohello Azure AD.
2. Après une réussite sign-in, un jeton est généré et envoyé le périphérique de client toohello.
3. client de Hello envoie hello jeton toohello service Proxy d’Application, qui Récupère le nom d’hello utilisateur principal (UPN) et le nom de principal de sécurité (SPN) à partir du jeton de hello, dirige ensuite le connecteur de Proxy d’Application hello demande toohello.
4. Si vous avez configuré l’authentification unique, le connecteur de hello effectue aucune authentification supplémentaire requise pour le compte d’utilisateur de hello.
5. connecteur de Hello envoie l’application locale de hello demande toohello.  
6. réponse de Hello est envoyé via le Proxy d’Application service et connecteur toohello de l’utilisateur.

### <a name="single-sign-on"></a>Authentification unique
Proxy d’Application Azure AD fournit l’authentification unique (SSO) tooapplications qui utilisent l’authentification Windows (intégrée) ou des applications prenant en charge les revendications. Si votre application utilise IWA, le Proxy d’Application emprunte l’identité utilisateur hello à l’aide de la délégation contrainte Kerberos tooprovide SSO. Si vous avez une application prenant en charge les revendications qui approuve Azure Active Directory, l’authentification unique fonctionne, car l’utilisateur de hello a déjà été authentifié par Azure AD.

Pour plus d’informations sur Kerberos, consultez [vous souhaitez tooknow sur la délégation Kerberos (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

### <a name="managing-apps"></a>Gestion des applications
Votre application est publiée avec le Proxy d’Application, vous pouvez le gérer comme toute autre application d’entreprise Bonjour portail Azure. Vous pouvez utiliser les fonctionnalités de sécurité Azure Active Directory comme conditionnelle vérification d’accès et en deux étapes, contrôler les autorisations d’utilisateur et personnaliser hello marque de votre application. 

## <a name="get-started"></a>Prise en main

Avant de configurer le Proxy d’application, assurez-vous d’être l’administrateur global d’une [édition d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) et d’un annuaire pris en charge.

Prise en main du Proxy d’application en deux étapes :

1. [Activer le Proxy d’Application et de configurer le connecteur de hello](active-directory-application-proxy-enable.md).    
2. [Publier des applications](active-directory-application-proxy-publish.md) -utilisez hello, Assistant simple et rapide tooget vos applications locales publiées et accessibles à distance.

## <a name="whats-next"></a>Et ensuite ?
Une fois votre première application publiée, vous pouvez faire bien d’autres choses encore avec le Proxy d’application :

* [Activer l’authentification unique](active-directory-application-proxy-sso-using-kcd.md)
* [Publier des applications avec votre propre nom de domaine](active-directory-application-proxy-custom-domains.md)
* [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md)
* [Utiliser des serveurs proxy locaux actuels](application-proxy-working-with-proxy-servers.md) 
* [Définir une page d’accueil personnalisée](application-proxy-office365-app-launcher.md)

Pour les informations les plus récentes hello et mises à jour, consultez hello [blog de Proxy d’Application](http://blogs.technet.com/b/applicationproxyblog/)

