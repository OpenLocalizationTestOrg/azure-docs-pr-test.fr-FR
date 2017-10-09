---
title: "Vue d’ensemble - Azure AD B2C | Microsoft Docs"
description: "Développement d’applications accessibles aux consommateurs avec Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c465dbde-f800-4f2e-8814-0ff5f5dae610
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: saeedakhter-msft
ms.openlocfilehash: abfd742e710458de3193dc5051de7818a112376c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-focus-on-your-app-let-us-worry-about-sign-up-and-sign-in"></a>Azure AD B2C : concentrez-vous sur votre application, nous nous chargeons de l’inscription et de la connexion

Azure AD B2C est une solution de gestion des identités de cloud pour applications web et mobiles. Il est d’une haute disponibilité globale des services qui s’adapte toohundreds de millions d’identités. Basé sur une plateforme sécurisée à l’échelle de l’entreprise, Azure AD B2C protège vos applications, votre entreprise et vos clients.

Avec une configuration minimale, Azure AD B2C permet tooauthenticate de votre application :

* des **comptes de réseaux sociaux** (tels que Facebook, Google, LinkedIn et autres) ;
* des **comptes d’entreprise** (à l’aide de protocoles de standards ouverts, d’OpenID Connect ou de SAML) ;
* des **comptes locaux** (adresse e-mail et mot de passe ou nom d’utilisateur et mot de passe).

## <a name="get-started"></a>Prise en main

Tout d’abord, obtenir votre propre locataire à l’aide de hello étapes [créer un client Azure AD B2C](active-directory-b2c-get-started.md).

Puis, choisissez le scénario de développement de votre application :

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![Applications mobiles et de bureau](../active-directory/develop/media/active-directory-developers-guide/NativeApp_Icon.png)<br />Applications mobiles et de bureau</center> | [Vue d’ensemble](active-directory-b2c-reference-oauth-code.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br /><br />[iOS](https://github.com/Azure-Samples/active-directory-b2c-ios-swift-native-msal)<br /><br />[Android](https://github.com/Azure-Samples/active-directory-b2c-android-native-msal) | [.NET](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop)<br /><br />[Xamarin](https://github.com/Azure-Samples/active-directory-b2c-xamarin-native) |  |
| <center>![Web Apps](../active-directory/develop/media/active-directory-developers-guide/Web_app.png)<br />Web Apps</center> | [Vue d'ensemble](active-directory-b2c-reference-oidc.md)<br /><br />[ASP.NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)<br /><br />[ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapp) | [Node.JS](active-directory-b2c-devquickstarts-web-node.md) |  |
| <center>![Applications à page unique](../active-directory/develop/media/active-directory-developers-guide/SPA.png)<br />Applications à page unique</center> | [Vue d'ensemble](active-directory-b2c-reference-spa.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp)<br /><br /> |  |  |
| <center>![API Web](../active-directory/develop/media/active-directory-developers-guide/Web_API.png)<br />API Web</center> | [ASP.NET](active-directory-b2c-devquickstarts-api-dotnet.md)<br /><br /> [ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)<br /><br /> [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) | [Appeler une API web .NET](active-directory-b2c-devquickstarts-web-api-dotnet.md) |

## <a name="whats-new"></a>Nouveautés

Revenez souvent toolearn sur les futures modifications toohello Azure Active Directory B2C. Nous communiquons également les mises à jour sur Tweeter via @AzureAD.

* En outre trop « Stratégies intégrées » (disponibilité générale), hello [« Stratégies personnalisées »](active-directory-b2c-overview-custom.md) fonctionnalité est désormais disponible en version préliminaire publique.  Les stratégies personnalisées sont pour les professionnels de l’identité que vous avez besoin de contrôler la composition hello de leur expérience de l’identité.
* Hello [jeton d’accès](https://azure.microsoft.com/en-us/blog/azure-ad-b2c-access-tokens-now-in-public-preview) fonctionnalité est désormais disponible en version préliminaire publique.
* [La disponibilité générale des annuaires Azure AD B2C basés en Europe](https://azure.microsoft.com/en-us/blog/azuread-b2c-ga-eu/) a été annoncée.
* Consultez notre bibliothèque croissante [d’exemples de code sur Github](https://github.com/Azure-Samples?q=b2c).

## <a name="how-tooarticles"></a>Tooarticles de procédure

Découvrez comment les fonctionnalités Azure Active Directory B2C spécifiques toouse :

* Configurer des comptes [Facebook](active-directory-b2c-setup-fb-app.md), [Google+](active-directory-b2c-setup-goog-app.md), [Microsoft](active-directory-b2c-setup-msa-app.md), [Amazon](active-directory-b2c-setup-amzn-app.md) et [LinkedIn](active-directory-b2c-setup-li-app.md) à utiliser dans vos applications grand public.
* [Utiliser les informations de toocollect d’attributs personnalisés sur vos consommateurs](active-directory-b2c-reference-custom-attr.md).
* [Activer Azure Multi-Factor Authentication dans vos applications grand public](active-directory-b2c-reference-mfa.md).
* [Configurer une réinitialisation de mot de passe libre-service pour vos consommateurs](active-directory-b2c-reference-sspr.md).
* [Personnaliser hello apparence de l’inscription, vous connecter en et d’autres pages de consommateur](active-directory-b2c-reference-ui-customization.md) qui sont pris en charge par Azure Active Directory B2C.
* [Utilisez hello Azure Active Directory Graph API tooprogrammatically créer, lire, mettre à jour et supprimer les consommateurs](active-directory-b2c-devquickstarts-graph-dotnet.md) dans votre locataire Azure Active Directory B2C.

## <a name="next-steps"></a>Étapes suivantes

Ces liens sont utiles pour l’exploration service hello en profondeur :

* Consultez hello [les informations de tarification Azure Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).
* Consultez notre [exemples de code](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory&term=b2c) pour Azure Active Directory B2C. 
* Obtenir de l’aide de débordement de pile à l’aide de hello [azure-ad-b2c](http://stackoverflow.com/questions/tagged/azure-ad-b2c) balise.
* Faites-nous part de vos idées à l’aide de [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c), nous souhaitons toohear les !
* Hello de révision [Azure AD B2C Protocol Reference](active-directory-b2c-reference-protocols.md).
* Hello de révision [Azure AD B2C jeton référence](active-directory-b2c-reference-tokens.md).
* Hello de lecture [Forum aux questions sur Azure Active Directory B2C](active-directory-b2c-faqs.md).
* [Dépôt de demandes de support pour Azure Active Directory B2C](active-directory-b2c-support.md).

## <a name="get-security-updates-for-our-products"></a>Obtenir les mises à jour de sécurité de nos produits

Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.

