---
title: "aaaAzure bibliothèques d’authentification Active Directory | Documents Microsoft"
description: "Hello bibliothèque d’authentification Azure AD (ADAL) permet aux développeurs d’applications à client tooeasily authentifier les utilisateurs toocloud ou Active Directory (AD) local et puis d’obtenir des jetons d’accès pour sécuriser les appels d’API."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: mbaldwin
ms.assetid: 2e4fc79a-0285-40be-8c77-65edee408a22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 20fae18807ef03463ab1bc218e5f3548b5bd5717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-authentication-libraries"></a>Bibliothèques d’authentification d’Azure Active Directory
Bonjour Azure Active Directory Authentication Library (ADAL) permet aux clients application développeurs tooeasily authentifier les utilisateurs toocloud ou Active Directory (AD) local et obtenir des jetons d’accès pour sécuriser les appels d’API. La bibliothèque ADAL facilite l’authentification pour les développeurs grâce à des fonctionnalités comme :
 - La prise en charge des appels de méthode asynchrones
 - Un cache de jeton configurable qui stocke les jetons d’accès et les jetons d’actualisation
 - L’actualisation automatique des jetons lorsqu’un jeton d’accès expire et qu’un jeton d’actualisation est disponible
 - Et bien plus...
 
En gérant la plupart de complexité de hello, ADAL permet aux développeurs de se concentrer sur la logique métier et sécuriser facilement les ressources, sans être un expert en sécurité.

La bibliothèque ADAL est disponible sur diverses plateformes.

### <a name="client-libraries"></a>Bibliothèques clientes

| Plateforme | Bibliothèque | Télécharger | Code source | Exemple | Référence
| --- | --- | --- | --- | --- | --- |
| .NET Client, Windows Store, UWP, Xamarin iOS et Android |MSAL pour .NET (préversion) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client/1.1.0-preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Application de bureau](~/articles/active-directory/develop/guidedsetups/active-directory-windesktop.md) |[Référence](https://docs.microsoft.com/dotnet/api/?view=identityclient-1.1.0-preview) | 
| JavaScript |MSAL pour JavaScript (préversion) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Application à page unique](~/articles/active-directory/develop/GuidedSetups/active-directory-javascriptspa.md) | [Référence](https://htmlpreview.github.io/?https://raw.githubusercontent.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/docs/classes/_useragentapplication_.msal.useragentapplication.html) | 
| iOS |MSAL pour iOS (préversion) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [Application iOS](~/articles/active-directory/develop/GuidedSetups/active-directory-ios.md) | [Référence](https://azuread.github.io/docs/objc/) |
| Android |MSAL pour Android (préversion) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Application Android](~/articles/active-directory/develop/GuidedSetups/active-directory-android.md) | [Référence](http://javadoc.io/doc/com.microsoft.identity.client/msal/0.1.1) |
| .NET Client, Windows Store, UWP, Xamarin iOS et Android |ADAL .NET v3 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) | [Application de bureau](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-dotnet) |[Référence](https://docs.microsoft.com/dotnet/api/?view=identitymodelclientsad-3.13.9) | 
| .NET Client, Windows Store, Windows Phone 8.1 |ADAL .NET v2 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.28.4) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/releases/tag/v2.28.4) | [Application de bureau](https://github.com/AzureADQuickStarts/NativeClient-DotNet/releases/tag/v2.X) | | 
| JavaScript |ADAL.js |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[Application à page unique](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) | |
| iOS, macOS |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc) |[Application iOS](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-ios) | [Référence](https://cocoapods.org/pods/ADAL)|
| Android |ADAL |[Hello référentiel Central](http://search.maven.org/remotecontent?filepath=com/microsoft/aad/adal/) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android) |[Application Android](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-android) | [JavaDocs](http://javadoc.io/doc/com.microsoft.aad/adal/)|
| Node.js |ADAL |[npm](https://www.npmjs.com/package/adal-node) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) | | |
| Java |ADAL4J |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[Applications web Java](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-java) | |
| Python |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) | | |
### <a name="server-libraries"></a>Bibliothèques serveur 

| Plateforme | Bibliothèque | Télécharger | Code source | Exemple | Référence
| --- | --- | --- | --- | --- | --- |
| .NET |OWIN pour Azure AD|[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |[Application MVC](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-dotnet) | |
| .NET |OWIN pour OpenIDConnect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[Application web](https://github.com/AzureADSamples/WebApp-OpenIDConnect-DotNet) | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [API Web](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapi-nodejs)| |
| .NET |OWIN pour WS-Federation |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) |[CodePlex](http://katanaproject.codeplex.com) |[Application Web MVC](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) | |
| .NET |Extensions de protocole d’identité pour .NET 4.5 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Protocol.Extensions) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET |Gestionnaire JWT pour .NET 4.5 |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |



## <a name="scenarios"></a>Scénarios

Voici trois scénarios courants dans lesquels ADAL peut être utilisé pour authentifier un utilisateur qui accède à une ressource distante :  

### <a name="authenticating-users-of-a-native-client-application-running-on-a-device"></a>Authentification des utilisateurs d’une application cliente native exécutée sur un appareil 

Dans ce scénario, un développeur a une application cliente WPF, qui doit tooaccess une ressource distante sécurisée par Azure AD, telle qu’une API web. Il dispose d’un abonnement Azure, sait comment tooinvoke hello API web en aval et connaît hello Azure client AD qui hello utilise des API web. Par conséquent, il peut utiliser l’authentification ADAL toofacilitate avec Azure AD, en déléguant complètement hello authentification expérience tooADAL ou en gérant de manière explicite les informations d’identification de l’utilisateur. Utilisateur de hello tooauthenticate facile rend la bibliothèque ADAL, obtenir un jeton d’accès et un jeton d’actualisation d’Azure AD et l’utiliser hello accès jeton toomake demandes toohello web API.

Pour voir un exemple de code illustrant ce scénario à l’aide de l’authentification tooAzure AD, [Application WPF Client Native tooWeb API](https://github.com/azureadsamples/nativeclient-dotnet).

### <a name="authenticating-a-confidential-client-application-running-on-a-web-server"></a>Authentification d’une application cliente confidentielle exécutée sur un serveur web

Dans ce scénario, un développeur dispose d’une application en cours d’exécution sur un serveur qui doit tooaccess une ressource distante sécurisée par Azure AD, telle qu’une API web. Il dispose d’un abonnement Azure, sait comment tooinvoke hello service en aval et connaît le locataire d’Azure AD hello web hello API utilise. Par conséquent, il peut utiliser l’authentification ADAL toofacilitate avec Azure AD en gérant de manière explicite les informations d’identification de l’application hello. La bibliothèque ADAL rend facile tooretrieve un jeton d’Azure AD à l’aide des informations d’identification du client de l’application hello, puis utilisez ce site web de toohello toomake jeton demandes API. La bibliothèque ADAL également handles gestion hello de durée de vie de hello jeton d’accès en mise en cache et en renouvelant si nécessaire. Pour voir un exemple de code illustrant ce scénario, [démon console Application tooWeb API](https://github.com/AzureADSamples/Daemon-DotNet).

### <a name="authenticating-a-confidential-client-application-running-on-a-server-on-behalf-of-a-user"></a>Authentification d’une application cliente confidentielle exécutée sur un serveur, pour le compte d’un utilisateur 

Dans ce scénario, un développeur dispose d’une application en cours d’exécution sur un serveur qui doit tooaccess une ressource distante sécurisée par Azure AD, telle qu’une API web. demande de Hello doit également toobe effectué au nom d’un utilisateur Azure AD. Il dispose d’un abonnement Azure, sait comment tooinvoke hello API web en aval et connaît hello service hello de locataire Azure AD utilise. Une fois authentifié toohello web application, utilisateur de hello application hello peut obtenir un code d’autorisation pour l’utilisateur de hello depuis Azure AD. Hello web application peut ensuite utiliser la bibliothèque ADAL tooobtain un jeton d’accès et un jeton d’actualisation pour le compte d’un utilisateur à l’aide de hello d’autorisation client et le code d’informations d’identification associées application hello d’Azure AD. Une fois que l’application web de hello est en possession du jeton d’accès hello, il peut appeler hello web API jusqu'à expiration du jeton de hello. Lors de l’expiration du jeton de hello, application web de hello permet tooget ADAL un nouveau jeton d’accès à l’aide du jeton d’actualisation hello reçu précédemment. Pour voir un exemple de code illustrant ce scénario, [tooWeb de tooWeb API Native client API](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof).

## <a name="see-also"></a>Voir aussi

- [Hello guide du développeur Azure Active Directory](active-directory-developers-guide.md)
- [Scénarios d’authentification pour Azure Active Directory](active-directory-authentication-scenarios.md)
- [Exemples de code Azure Active Directory](active-directory-code-samples.md)
