---
title: "bibliothèques d’authentification v2.0 aaaAzure Active Directory | Documents Microsoft"
description: "Les bibliothèques clientes compatible et bibliothèques intergiciel (middleware) du serveur et bibliothèque connexe, source et liens d’exemples, pour le point de terminaison v2.0 hello Azure Active Directory."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 19cec615-e51f-4141-9f8c-aaf38ff9f746
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7affdaac3a087b951d54d96fa68edde2a065172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-authentication-libraries"></a>Bibliothèques d’authentification Azure Active Directory v2.0
point de terminaison v2.0 Hello Azure Active Directory (Azure AD) prend en charge les protocoles de OAuth 2.0 et OpenID Connect 1.0 hello standard. Vous pouvez utiliser différentes bibliothèques à partir de Microsoft et d’autres organisations avec point de terminaison hello v2.0.

Lorsque vous générez une application qui utilise le point de terminaison hello v2.0, nous vous recommandons d’utiliser les bibliothèques qui sont écrits par des experts de domaine de protocole qui suivent une méthodologie de cycle de vie de développement de sécurité (SDL), comme [hello un suivi par Microsoft] [Microsoft-SDL]. Si vous décidez de prise en charge de code toohand de protocoles de hello, nous vous recommandons de suivre la méthodologie SDL et d’accorder une attention toohello considérations sur la sécurité dans les spécifications de normes hello pour chaque protocole.

## <a name="types-of-libraries"></a>Types de bibliothèques
Azure AD v2.0 prend en charge deux types de bibliothèques :

* **Bibliothèques clientes**. Serveurs et clients natifs utilisent des jetons d’accès client bibliothèques tooget pour l’appel d’une ressource, telles que Microsoft Graph.
* **Bibliothèques de middleware de serveur**. Les applications web utilisent des bibliothèques de middleware de serveur pour la connexion des utilisateurs. API Web utilisent le serveur intergiciel (middleware) bibliothèques toovalidate jetons qui sont envoyés par des clients natifs ou par d’autres serveurs.

## <a name="library-support"></a>Prise en charge de la bibliothèque
Vous pouvez choisir n’importe quelle bibliothèque conforme aux normes lorsque vous utilisez le point de terminaison hello v2.0, il est important tooknow où toogo pour la prise en charge. Pour les problèmes et les demandes de fonctionnalités dans le code de bibliothèque, contactez le propriétaire de la bibliothèque hello. Pour les problèmes et les demandes de fonctionnalités dans l’implémentation du protocole côté service hello, contactez Microsoft.

Les bibliothèques sont classées en deux catégories de prise en charge :

* **Pris en charge par Microsoft**. Microsoft fournit des correctifs de ces bibliothèques, auxquelles il a appliqué la méthodologie SDL standard.
* **Compatible**. Microsoft a testé ces bibliothèques dans les scénarios de base et confirmé qu’ils fonctionnent avec le point de terminaison hello v2.0. Microsoft ne fournit pas de correctifs pour ces bibliothèques et n’a pas vérifié ces bibliothèques. Problèmes et des demandes de fonctionnalités doivent être projet open source de la bibliothèque toohello dirigée.

Pour obtenir la liste des bibliothèques qui fonctionnent avec le point de terminaison hello v2.0, consultez hello sections suivantes présentées dans cet article.


## <a name="microsoft-supported-client-libraries"></a>Bibliothèques clientes prises en charge par Microsoft

> [!IMPORTANT]
> bibliothèques d’aperçu Hello MSAL conviennent pour une utilisation dans un environnement de production. Nous fournissons hello même support de niveau de production de ces bibliothèques, comme nous le faisons nos bibliothèques de production en cours (ADAL). Version préliminaire hello que nous pouvons opérer des modifications toohello MSAL API, format de cache interne, et autres mécanismes de ces bibliothèques sans préavis, qui vous sera nécessaire tootake, ainsi que des correctifs de bogues ou des améliorations des fonctionnalités. Cela peut avoir un impact sur votre application. Par exemple, un toohello modifier le format du cache peut avoir un impact sur vos utilisateurs, telles que leur demandant de toosign de nouveau. Une modification de l’API peut nécessiter vous tooupdate votre code. Lorsque nous fournissez hello version en disponibilité générale en nous nécessitera tooupdate toohello disponibilité générale version dans les six mois, que les applications écrites à l’aide d’une version d’évaluation version de bibliothèque peut ne plus fonctionner.

| Plateforme | Bibliothèque | Télécharger | Code source | Exemple | Référence
| --- | --- | --- | --- | --- | --- |
| .NET Client, Windows Store, UWP, Xamarin iOS et Android | MSAL .NET (préversion) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Application de bureau](guidedsetups/active-directory-mobileanddesktopapp-windowsdesktop-intro.md) |  |
| JavaScript | MSAL.js (préversion) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Application à page unique](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2) |  |
| iOS, macOS | MSAL (préversion) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [Application iOS](https://github.com/Azure-Samples/active-directory-msal-ios-swift) |  |
| Android | MSAL (préversion) | [Hello référentiel Central](https://repo1.maven.org/maven2/com/microsoft/identity/client/msal/) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Application Android](guidedsetups/active-directory-mobileanddesktopapp-android-intro.md) | [JavaDocs](http://javadoc.io/doc/com.microsoft.identity.client/msal) |

## <a name="microsoft-supported-server-middleware-libraries"></a>Bibliothèques de middleware de serveur prises en charge par Microsoft

| Plateforme | Bibliothèque | Télécharger | Code source | Exemple | Référence
| --- | --- | --- | --- | --- | --- |
| .NET 4.x | Intergiciel OWIN OpenID Connect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[Application MVC](guidedsetups/active-directory-serversidewebapp-aspnetwebappowin-intro.md) | |
| .NET 4.x | Intergiciel OWIN OAuth Bearer pour Azure AD |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |  | |
| .NET 4.x | Gestionnaire JWT pour .NET 4.5 | [NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/4.0.4.403061554) | [GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET Core | Intergiciel ASP.NET OpenID Connect |[Microsoft.AspNetCore.Authentication.OpenIdConnect (NuGet)][ServerLib-NetCore-Owin-Oidc-Lib] |[Sécurité ASP.NET (GitHub)][ServerLib-NetCore-Owin-Oidc-Repo] |[Application MVC](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2) |
| .NET Core | Intergiciel ASP.NET OAuth Bearer |[Microsoft.AspNetCore.Authentication.OAuth (NuGet)][ServerLib-NetCore-Owin-Oauth-Lib] |[Sécurité ASP.NET (GitHub)][ServerLib-NetCore-Owin-Oauth-Repo] |  |
| .NET Core | Gestionnaire JWT pour .NET Core  |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Application web](active-directory-v2-devquickstarts-node-web.md)| |

## <a name="compatible-client-libraries"></a>Bibliothèques clientes compatibles
| Plateforme | Nom de la bibliothèque | Version testée | Code source | Exemple |
|:---:|:---:|:---:|:---:|:---:|
| Android |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib/wiki) |0.2.1 |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib) |[Exemple d’application native](active-directory-v2-devquickstarts-android.md) |
| iOS |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |1.2.8 |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |[Exemple d’application native](active-directory-v2-devquickstarts-ios.md) |
| JavaScript |[Hello.js](https://adodson.com/hello.js/) |1.13.5 |[Hello.js](https://github.com/MrSwitch/hello.js) |[SPA](https://github.com/Azure-Samples/active-directory-javascript-graphapi-web-v2) |

## <a name="compatible-server-middleware-libraries"></a>Bibliothèques de middleware de serveur compatibles
| Plateforme | Nom de la bibliothèque | Version testée | Code source | Exemple |
|:---:|:---:|:---:|:---:|:---:|
| Java | [Scribe Java scribejava](https://github.com/scribejava/scribejava) | [Version 3.2.0](https://github.com/scribejava/scribejava/releases/tag/scribejava-3.2.0) | [Scribe Java](https://github.com/scribejava/scribejava/archive/scribejava-3.2.0.zip) | |
| PHP | [Hello PHP et la ligue oauth2-client](https://github.com/thephpleague/oauth2-client) | [Version 1.4.2](https://github.com/thephpleague/oauth2-client/releases/tag/1.4.2) | [oauth2-client](https://github.com/thephpleague/oauth2-client/archive/1.4.2.zip) | |
| Python-Flask |[Flask-OAuthlib](https://github.com/lepture/flask-oauthlib) |0.9.3 |[Flask-OAuthlib](https://github.com/lepture/flask-oauthlib) |[Application web](https://github.com/Azure-Samples/active-directory-python-flask-graphapi-web-v2) |
| Ruby |[OmniAuth](https://github.com/omniauth/omniauth/wiki) |omniauth:1.3.1</br>omniauth-oauth2:1.4.0 |[OmniAuth](https://github.com/omniauth/omniauth)</br>[OmniAuth OAuth2](https://github.com/intridea/omniauth-oauth2) |  |

## <a name="related-content"></a>Contenu connexe
Pour plus d’informations sur le point de terminaison v2.0 hello Azure AD, consultez hello [vue d’ensemble du v2.0 de modèle d’application Azure AD][AAD-App-Model-V2-Overview].

<!--Image references-->

<!--Reference style links -->
[AAD-App-Model-V2-Overview]: ../active-directory-appmodel-v2-overview.md
[ClientLib-NET-Lib]: http://www.nuget.org/packages/Microsoft.Identity.Client
[ClientLib-NET-Repo]: https://github.com/AzureAD/microsoft-authentication-library-for-dotnet
[ClientLib-NET-Sample]: active-directory-v2-devquickstarts-wpf.md
[ClientLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ClientLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad
[ClientLib-Node-Sample]:/
[ClientLib-Iosmac-Lib]:/
[ClientLib-Iosmac-Repo]:/
[ClientLib-Iosmac-Sample]:/
[ClientLib-Android-Lib]:/
[ClientLib-Android-Repo]:/
[ClientLib-Android-Sample]:/
[ClientLib-Js-Lib]:/
[ClientLib-Js-Repo]:/
[ClientLib-Js-Sample]:/

[Microsoft-SDL]: http://www.microsoft.com/sdl/default.aspx
[ServerLib-Net4-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/
[ServerLib-Net4-Owin-Oidc-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oidc-Sample]: active-directory-v2-devquickstarts-dotnet-web.md
[ServerLib-Net4-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OAuth/
[ServerLib-Net4-Owin-Oauth-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oauth-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-dotnet-api/
[ServerLib-Net-Jwt-Lib]: https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt
[ServerLib-Net-Jwt-Repo]: https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet
[ServerLib-Net-Jwt-Sample]:/
[ServerLib-NetCore-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect/
[ServerLib-NetCore-Owin-Oidc-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oidc-Sample]: https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2
[ServerLib-NetCore-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OAuth/
[ServerLib-NetCore-Owin-Oauth-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oauth-Sample]:/
[ServerLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ServerLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad/
[ServerLib-Node-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-node-web/
