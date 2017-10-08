---
title: aaaAzure des exemples de Code Active Directory | Documents Microsoft
description: "Index des exemples de code Azure Active Directory, organisé par scénario."
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Exemples de code Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Vous pouvez utiliser Microsoft Azure Active Directory (Azure AD) tooadd d’authentification et d’autorisation tooyour des applications web et l’API web. Cette section contient un lien toosamples qui vous montrent le fonctionnement et les extraits de code que vous pouvez utiliser dans vos applications. Sur la page exemple de code hello, vous trouverez détaillées en lecture-me rubriques d’aident à la configuration requise, installation et de configuration. Et hello code commenté toohelp vous comprenez les sections critiques hello.

scénario de base toounderstand hello pour chaque type d’exemple, consultez les scénarios d’authentification pour Azure AD.

Contribuent exemples tooour sur GitHub : [exemples Microsoft Azure Active Directory et la Documentation](https://github.com/Azure-Samples?page=3&query=active-directory).

## <a name="web-browser-tooweb-application"></a>TooWeb de navigateur Web Application
Ces exemples montrent comment une application web qui dirige de toowrite hello toosign de navigateur de l’utilisateur dans tooAzure AD.

| Langue/plateforme | Exemple | Description |
| --- | --- | --- |
| C#/.NET |[WebApp-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Utiliser OpenID Connect (middleware OWIN OpenID Connect ASP.Net) tooauthenticate les utilisateurs d’un locataire Azure AD. |
| C#/.NET |[WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Une application web de MVC .NET mutualisée qui utilise OpenID Connect (middleware OWIN OpenID Connect ASP.Net) tooauthenticate les utilisateurs de plusieurs locataires Azure AD. |
| C#/.NET |[WebApp-WSFederation-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |Utilisez les utilisateurs de tooauthenticate WS-Federation (middleware OWIN de WS-Federation ASP.Net) à partir d’un locataire Azure AD. |

## <a name="single-page-application-spa"></a>Application à page unique (SPA)
Cet exemple montre comment toowrite une application à page unique sécurisée avec Azure AD.  

| Langue/plateforme | Exemple | Description |
| --- | --- | --- |
| JavaScript, C#/.NET |[SinglePageApp-DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |Utiliser l’ADAL pour JavaScript et Azure AD application à page unique toosecure basée sur un AngularJS implémentée avec un principal de l’API web ASP.NET. |

## <a name="native-application-tooweb-api"></a>TooWeb Application native API
Ces exemples de code montrent comment les applications clientes natives toobuild qui appellent des API web sécurisées par Azure AD. Ils utilisent [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) et [OAuth 2.0 dans Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Langue/plateforme | Exemple | Description |
| --- | --- | --- |
| JavaScript |[NativeClient-MultiTarget-Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |Utilisez le plug-in de la bibliothèque ADAL hello pour Apache Cordova toobuild une application Apache Cordova qui appelle une API web et utilise Azure AD pour l’authentification. |
| C#/.NET |[NativeClient-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |Application WPF .NET qui appelle une API web sécurisée à l’aide d’Azure AD. |
| C#/.NET |[NativeClient-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Application Windows Store qui appelle une API web sécurisée avec Azure AD. |
| C#/.NET |[NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Application Windows Store qui appelle une API web mutualisée sécurisée avec Azure AD. |
| C#/.NET |[WebAPI-OnBehalfOf-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |Une application cliente native qui appelle une API web, qui obtient un jeton tooact pour le compte d’utilisateur d’origine de hello et utilise ensuite hello jeton toocall une autre API web. |
| C#/.NET |[NativeClient-WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Application Windows Store pour Windows Phone 8.1 qui appelle une API web sécurisée par Azure AD. |
| ObjC |[NativeClient-iOS](https://github.com/Azure-Samples/active-directory-ios) |Application iOS qui appelle une API web qui nécessite Azure AD pour l’authentification. |
| C#/.NET |[WebAPI-ManuallyValidateJwt-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |Une application cliente native qui inclut la logique tooprocess un jeton JWT dans une API web, au lieu d’utiliser l’intergiciel (middleware) OWIN. |
| C#/Xamarin |[NativeClient-Xamarin-Android](https://github.com/Azure-Samples/active-directory-xamarin-android) |Un Xamarin liaison toohello natif Azure AD Authentication Library (ADAL) pour hello bibliothèque Android. |
| C#/Xamarin |[NativeClient-Xamarin-iOS](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Un toohello de liaison Xamarin native Azure AD Authentication Library (ADAL) pour iOS. |
| C#/Xamarin |[NativeClient-MultiTarget-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |Projet Xamarin qui cible cinq plateformes et appelle une API web sécurisée par Azure AD. |
| C#/.NET |[NativeClient-Headless-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |Application native qui effectue une authentification non interactive et appelle une API web sécurisée par Azure AD. |

## <a name="web-application-tooweb-api"></a>TooWeb d’Application Web API
Ces exemples de code montrent comment utiliser [OAuth 2.0 dans Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) toobuild les applications web qui appellent des API web sécurisées par Azure AD.

| Langue/plateforme | Exemple | Description |
| --- | --- | --- |
| C#/.NET |[WebApp-WebAPI-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |Appeler une API web avec des autorisations hello signé de l’utilisateur. |
| C#/.NET |[WebApp-WebAPI-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |Appeler une API web avec les autorisations de l’application hello. |
| C#/.NET |[WebApp-WebAPI-OAuth2-UserIdentity-Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |Ajouter une autorisation avec [OAuth 2.0 dans Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooan application web existante afin qu’il peut appeler une API web. |
| JavaScript |[WebAPI-Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |Configurer un service API REST intégré à Azure AD pour la protection de l’API. Inclut un serveur Node.js avec une API web. |
| C#/.NET |[WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |MVC mutualisée web application qui utilise OpenID Connect (middleware OWIN OpenID Connect ASP.Net) tooauthenticate les utilisateurs d’un locataire Azure AD. Utilise un hello tooinvoke du code d’autorisation API Graph. |

## <a name="server-or-daemon-application-tooweb-api"></a>Application serveur ou démon tooWeb API
Ces exemples de code montrent comment toobuild un démon ou une application serveur qui obtient des ressources à partir d’une API web à l’aide de [bibliothèque d’authentification Azure AD (ADAL)](active-directory-authentication-libraries.md) et [OAuth 2.0 dans Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Langue/plateforme | Exemple | Description |
| --- | --- | --- |
| C#/.NET |[Daemon-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |Application console qui appelle une API web. informations d’identification du client Hello sont un mot de passe. |
| C#/.NET |[Démon-CertificateCredential-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |Application console qui appelle une API web. informations d’identification du client Hello sont un certificat. |

## <a name="calling-azure-ad-graph-api"></a>Appel de l'API Graph d'Azure AD
Ces exemples de code montrent comment toobuild les applications qui appellent hello les données d’annuaire Azure AD Graph API tooread et en écriture.

| Langue/plateforme | Exemple | Description |
| --- | --- | --- |
| Java |[WebApp-GraphAPI-Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |Une application web qui utilise l’API Graph de hello tooaccess données d’annuaire Azure AD. |
| PHP |[WebApp-GraphAPI-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |Une application web qui utilise l’API Graph de hello tooaccess données d’annuaire Azure AD. |
| C#/.NET |[WebApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Une application web qui utilise l’API Graph de hello tooaccess données d’annuaire Azure AD. |
| C#/.NET |[ConsoleApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |Cette application console montre courants en lecture et écriture appels toohello API Graph et explique comment tooexecute utilisateur attribution de licence et mettre à jour la photo miniature et les liens d’un utilisateur. |
| C#/.NET |[ConsoleApp-GraphAPI-DiffQuery-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |Une application console qui utilise une requête différentielle hello dans tooget de l’API Graph hello périodique modifie des objets toouser dans un locataire Azure AD. |
| C#/.NET |[WebApp-GraphAPI-DirectoryExtensions-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |Une application MVC utilise l’API Graph requêtes toogenerate un organigramme d’entreprise simple. |
| PHP |[WebApp-GraphAPI-DirectoryExtensions-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |Une application PHP qui appelle hello API Graph tooregister une extension puis lire, mettre à jour et supprimer des valeurs dans l’attribut extension hello. |

## <a name="authorization"></a>Autorisation
Ces afficher des exemples de code comment toouse Azure AD pour l’autorisation.

| Langue/plateforme | Exemple | Description |
| --- | --- | --- |
| C#/.NET |[WebApp-GroupClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |Effectuer un contrôle d’accès en fonction du rôle (RBAC) à l’aide de revendications de groupe Active Directory Azure dans une application qui est intégrée avec Azure AD. |
| C#/.NET |[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |Effectuer un contrôle d’accès en fonction du rôle (RBAC) à l’aide de rôles d’application Active Directory Azure dans une application qui est intégrée avec Azure AD. |

## <a name="legacy-walkthroughs"></a>Procédures pas à pas héritées
Ces procédures pas à pas utilisent une technologie légèrement plus ancienne mais peuvent toujours présenter un intérêt.

| Langue/plateforme | Exemple | Description |
| --- | --- | --- |
| C#/.NET |[Autorisation basée sur un rôle et sur une liste de contrôle d’accès dans une application Microsoft Azure AD de Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=331694) |Effectuer une autorisation en fonction du rôle (RBAC) et une autorisation basée sur une liste de contrôle d’accès dans une application qui est intégrée avec Azure AD. |
| C#/.NET |[AAL - du service tooREST d’applications du Windows Store - authentification](http://go.microsoft.com/fwlink/?LinkId=330605) |Utilisez [bibliothèque d’authentification Azure AD (ADAL)](active-directory-authentication-libraries.md) (anciennement AAL) pour la version bêta de Windows Store tooadd utilisateur les fonctionnalités d’authentification tooa application du Windows Store. |
| C#/.NET |[ADAL - service tooREST de l’application Native - authentification avec AAD via une boîte de dialogue navigateur](http://go.microsoft.com/fwlink/?LinkId=259814) |Utilisez [bibliothèque d’authentification Azure AD (ADAL)](active-directory-authentication-libraries.md) client de tooadd utilisateur d’authentification fonctionnalités tooa WPF. |
| C#/.NET |[ADAL - service tooREST de l’application Native - authentification avec ACS via une boîte de dialogue navigateur](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |Utilisez [bibliothèque d’authentification Azure AD (ADAL)](active-directory-authentication-libraries.md) et [Access Control Service 2.0 (ACS)](http://msdn.microsoft.com/library/azure/hh147631.aspx) client de tooadd utilisateur d’authentification fonctionnalités tooa WPF. |
| C#/.NET |[ADAL - tooServer du serveur d’authentification](http://go.microsoft.com/fwlink/?LinkId=259816) |Utilisez [bibliothèque d’authentification Azure AD (ADAL)](active-directory-authentication-libraries.md) toosecure des appels de service à partir d’un tooan de processus serveur côté service MVC4 Web API REST. |
| C#/.NET |[Ajout de l’authentification tooYour à l’aide d’applications Web Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Configurer un .NET application tooperform web SSO par rapport à votre annuaire Azure AD de l’entreprise. |
| C#/.NET |[Développement d’une application web mutualisée avec Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Utilisez Azure AD tooadd toohello l’authentification unique et fonctionnalités d’accès de répertoire d’un toowork d’application .NET dans plusieurs organisations. |
| Java |[Exemple d’application Java pour l’API Azure AD Graph](http://go.microsoft.com/fwlink/?LinkId=263969) |Utilisez hello API Graph tooaccess des données d’annuaire Azure AD. |
| PHP |[Exemple d’application PHP pour l’API Azure AD Graph](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |Utilisez hello API Graph tooaccess des données d’annuaire Azure AD. |
| C#/.NET |[Exemple d’application pour l’API Azure AD Graph](http://go.microsoft.com/fwlink/?LinkID=262648) |Utilisez hello API Graph tooaccess des données d’annuaire Azure AD. |
| C#/.NET |[Exemple d’application pour la requête différentielle d’Azure AD Graph](http://go.microsoft.com/fwlink/?LinkId=275398) |Utilisez une requête différentielle hello hello API Graph tooget des modifications régulières toouser objets dans un locataire Azure AD. |
| C#/.NET |[Exemple d’application pour l’intégration d’une application cloud mutualisée pour Azure AD](http://go.microsoft.com/fwlink/?LinkId=275397) |Intégrer une application mutualisée dans Azure AD. |
| C#/.NET |[Sécurisation d’une application Windows Store et du service web REST avec Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Créer une ressource API web simple et une application cliente de Windows Store à l’aide d’Azure AD et hello [bibliothèque d’authentification Azure AD (ADAL)](active-directory-authentication-libraries.md). |
| C#/.NET |[À l’aide de hello tooQuery de l’API Graph Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Configurer un Bonjour de toouse de l’application Microsoft .NET données tooaccess de l’API Azure AD Graph à partir d’un annuaire de locataire Azure AD. |

## <a name="see-also"></a>Voir aussi
##### <a name="other-resources"></a>Autres ressources
[Guide du développeur Azure Active Directory](active-directory-developers-guide.md)

[Concept et référence de l’API Graph Azure AD](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Bibliothèque d’assistance de l’API Azure AD Graph](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
