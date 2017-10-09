---
title: "aaaAuthentication et d’autorisation dans Azure App Service | Documents Microsoft"
description: "Référence conceptuel et vue d’ensemble de hello d’authentification / autorisation de fonctionnalité pour Azure App Service"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: b7151b57-09e5-4c77-a10c-375a262f17e5
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/29/2016
ms.author: mahender
ms.openlocfilehash: dc2074b16cce47b72b78ea7afeda89dbc4832166
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-app-service"></a>Authentification et autorisation dans Azure App Service
## <a name="what-is-app-service-authentication--authorization"></a>Qu’est-ce que l’authentification/autorisation App Service ?
Application Service authentification / autorisation est une fonctionnalité qui fournit un moyen pour toosign de votre application dans les utilisateurs afin que vous n’avez pas toochange code sur le serveur principal d’application hello. Il fournit un moyen simple de tooprotect votre application et travailler avec des données par l’utilisateur.

App Service utilise l’identité fédérée, dans laquelle un fournisseur d’identité tiers stocke les comptes et authentifie les utilisateurs. application Hello s’appuie sur les informations d’identité du fournisseur hello afin que hello application n’a pas toostore ces informations lui-même. Service d’applications prend en charge cinq fournisseurs d’identité en dehors de la zone de hello : Azure Active Directory, Facebook, Google, Microsoft Account et Twitter. Votre application peut utiliser n’importe quel nombre de ces tooprovide de fournisseurs d’identité vos utilisateurs avec les options de la façon dont ils se connectent. tooexpand hello prise en charge intégrée, vous pouvez intégrer un autre fournisseur d’identité ou [votre propre solution d’identité personnalisé][custom-auth].

Si vous souhaitez tooget démarré immédiatement, consultez hello suivant didacticiels :

* [Ajouter une application de l’authentification tooyour iOS] [ iOS] (ou [Android], [Windows], [Xamarin.iOS], [ Xamarin.Android], [Xamarin.Forms], ou [Cordova])
* [Authentification utilisateur pour API Apps dans Azure App Service][apia-user]
* [Prise en main d’Azure App Service, 2e partie][web-getstarted]

## <a name="how-authentication-works-in-app-service"></a>Fonctionnement de l’authentification dans App Service
Dans tooauthenticate de commande à l’aide d’un des fournisseurs d’identité hello, vous devez d’abord tooconfigure hello identité fournisseur tooknow sur votre application. fournisseur d’identité Hello fournit ensuite les ID et les secrets que vous fournissiez tooApp Service. Relation d’approbation hello est terminée pour que Service d’applications puisse valider les assertions utilisateur, telles que les jetons d’authentification, à partir du fournisseur d’identité hello.

toosign un utilisateur à l’aide d’un de ces fournisseurs, utilisateur de hello doit être redirigé tooan de point de terminaison qui se connecte aux utilisateurs pour ce fournisseur. Si les clients utilisent un navigateur web, vous pouvez avoir du Service d’applications diriger automatiquement tous les utilisateurs non authentifiés toohello point de terminaison se connecte aux utilisateurs. Sinon, vous devez toodirect vos clients trop`{your App Service base URL}/.auth/login/<provider>`, où `<provider>` est une des valeurs suivantes de hello : aad, facebook, google, microsoft ou twitter. Les scénarios portant sur les appareils mobiles et les API sont expliqués plus loin dans cet article.

Les utilisateurs qui interagissent avec votre application via un navigateur web se verront affecter un cookie, qui leur permettra de rester authentifiés tant qu’ils seront connectés à votre application. Pour d’autres types de client, telles que mobile, un jeton de web JSON (JWT), qui doit être présentée dans hello `X-ZUMO-AUTH` en-tête, sera émise toohello client. client des applications mobiles Hello kits de développement logiciel gère cela pour vous. Vous pouvez également un jeton d’identité Azure Active Directory ou d’un jeton d’accès peut être directement inclus dans hello `Authorization` en-tête comme un [jeton de support](https://tools.ietf.org/html/rfc6750).

Service d’application valide n’importe quel jeton que votre application émet tooauthenticate utilisateurs ou un cookie. toorestrict qui peut accéder à votre application, consultez hello [autorisation](#authorization) section plus loin dans cet article.

### <a name="mobile-authentication-with-a-provider-sdk"></a>Authentification d’appareils mobiles avec un Kit de développement logiciel (SDK) de fournisseur
Une fois que tout est configuré sur hello principal, vous pouvez modifier toosign de clients mobiles avec le Service d’applications. Il existe deux approches :

* Utiliser un kit de développement logiciel qu’un fournisseur d’identité donnée publie tooestablish identité et ensuite obtenir l’accès tooApp Service.
* Utiliser une seule ligne de code pour la connexion client Mobile Apps hello SDK dans les utilisateurs.

> [!TIP]
> La plupart des applications doivent utiliser un fournisseur SDK tooget une expérience plus cohérente lorsque les utilisateurs se connectent, toouse actualisation prise en charge et tooget spécifie de ce fournisseur hello autres avantages.
> 
> 

Lorsque vous utilisez un fournisseur de kit de développement logiciel, les utilisateurs peuvent se connecter expérience tooan qui intègre plus étroitement avec le système d’exploitation de hello cette application hello est en cours d’exécution. Cela vous donne également un jeton du fournisseur et des informations utilisateur sur le client hello, ce qui rend beaucoup plus facile graphique de tooconsume API et personnaliser l’expérience utilisateur hello. Occasionnellement sur les blogs et forums, vous verrez cette hello tooas référencé « flux client » ou « flux dirigée vers le client », car le code hello client se connecte à des utilisateurs et le code client hello a jeton d’accès tooa fournisseur.

Après obtention d’un jeton du fournisseur, il doit toobe envoyé tooApp Service pour la validation. Une fois que le Service d’application valide le jeton de hello, Service de l’application crée un nouveau jeton du Service d’applications qui est retourné toohello client. client des applications mobiles Hello SDK a toomanage des méthodes d’assistance cet échange et attachement automatique hello demandes de jeton tooall toohello application back-end. Les développeurs peuvent également conserver un jeton du fournisseur toohello référence s’ils le souhaitent.

### <a name="mobile-authentication-without-a-provider-sdk"></a>Authentification d’appareils mobiles sans Kit de développement logiciel (SDK) de fournisseur
Si vous ne souhaitez pas tooset un fournisseur de kit de développement logiciel, vous pouvez autoriser la fonctionnalité des applications mobiles hello de toosign du Service d’applications Azure dans pour vous. client des applications mobiles Hello SDK s’ouvrir un fournisseur de toohello d’affichage web de votre choix et connectez-vous à utilisateur de hello. Parfois sur des blogs et forums, vous obtiendrez cette tooas référencé hello « flux serveur » ou « flux dirigée vers le serveur », car le serveur de hello gère les processus de hello qui se connecte aux utilisateurs, et le client hello SDK ne reçoit jamais le jeton du fournisseur hello.

Le code toostart que ce flux est inclus dans le didacticiel d’authentification hello pour chaque plateforme. À fin hello du flux de hello, le client de hello SDK dispose d’un jeton du Service d’applications, et jeton de hello est automatiquement attaché tooall demandes toohello application back-end.

### <a name="service-to-service-authentication"></a>Authentification de service à service
Bien que vous pouvez donner aux utilisateurs accès tooyour application, vous pouvez également approuver une autre application toocall votre propre API. Par exemple, une application web pourrait appeler une API dans une autre application web. Dans ce scénario, vous utilisez les informations d’identification pour un compte de service au lieu de tooget des informations d’identification utilisateur un jeton. Un compte de service est également appelé *principal de service* dans Azure Active Directory. L’authentification pratiquée avec ce type de compte est également appelée « scénario de service à service ».

> [!IMPORTANT]
> Comme les applications mobiles s’exécutent sur des appareils clients, celles-ci ne sont *pas* considérées comme des applications approuvées et ne doivent pas utiliser un flux de principal de service. Au lieu de cela, elles doivent utiliser un flux utilisateur décrit précédemment.
> 
> 

Pour les scénarios de service à service, App Service peut protéger votre application à l’aide d’Azure Active Directory. application appelante Hello doit simplement tooprovide un jeton d’autorisation principale de service Azure Active Directory qui est obtenu en fournissant l’ID de client hello et secret d’Azure Active Directory du client. Un exemple de ce scénario qui utilise des API ASP.NET applications s’explique par le didacticiel de hello, [l’authentification principale du Service pour les applications API][apia-service].

Si vous souhaitez toouse toohandle de l’authentification du Service d’applications un scénario de service, vous pouvez utiliser des certificats de client ou de l’authentification de base. Pour plus d’informations sur les certificats de client dans Azure, consultez [comment tooConfigure l’authentification mutuelle de TLS pour les applications Web](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Pour plus d’informations sur l’authentification de base dans ASP.NET, consultez [Filtres d’authentification dans ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).

L’authentification du compte de service à partir d’une application de Service de l’application logique application tooan API est un cas spécial qui est détaillé dans [à l’aide de votre API personnalisée hébergé sur App Service avec les applications de la logique](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="authorization"></a>Fonctionnement de l’autorisation dans App Service
Vous avez un contrôle total sur les demandes hello pouvant accéder à votre application. Application Service authentification / autorisation peut être configurée avec les hello suit les comportements :

* Autoriser uniquement les demandes authentifiées tooreach votre application.
  
    Si un navigateur reçoit une demande anonyme, du Service d’applications effectue une redirection page tooa pour le fournisseur d’identité hello que vous choisissez afin que les utilisateurs peuvent se connecter. Si la demande de hello provient d’un appareil mobile, hello retourné une réponse est HTTP *401 non autorisé* réponse.
  
    Avec cette option, vous n’avez pas besoin toowrite n’importe quel code d’authentification du tout dans votre application. Si vous avez besoin d’autorisation plus précie, informations sur l’utilisateur de hello sont disponible tooyour code.
* Autoriser toutes les demandes tooreach votre application, mais valider les demandes authentifiées et transmettre les informations d’authentification dans les en-têtes HTTP de hello.
  
    Cette option diffère le code de l’application tooyour décisions d’autorisation. Elle offre plus de souplesse dans la gestion des demandes anonymes, mais vous avez toowrite code.
* Autoriser toutes les demandes tooreach votre application et effectuer aucune action sur les informations d’authentification dans les demandes de hello.
  
    Dans ce cas, hello d’authentification / autorisation fonctionnalité est désactivée. tâches Hello d’authentification et d’autorisation sont entièrement tooyour code de l’application.

les comportements précédente Hello sont contrôlées par hello **tootake Action lors de la demande n’est pas authentifiée** option Bonjour portail Azure. Si vous choisissez ** se connecter avec *nom du fournisseur* **, toutes les demandes ont toobe authentifié. **Autoriser les requêtes (aucune action)** diffère du code de tooyour décision hello d’autorisation, mais il fournit toujours des informations d’authentification. Si vous souhaitez toohave votre code gère tous les éléments, que vous pouvez désactiver l’authentification de hello / la fonctionnalité d’autorisation.

## <a name="working-with-user-identities-in-your-application"></a>Utilisation des identités des utilisateurs dans votre application
Service de l’application passe d’applications de tooyour informations utilisateur à l’aide des en-têtes spéciaux. Ces en-têtes ne sont pas autorisés dans les requêtes externes ; ils ne seront présents que si la fonctionnalité d’autorisation/d’authentification d’App Service les définit. Voici quelques exemples d’en-têtes :

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Le code qui est écrit dans n’importe quel langage ou le framework peut obtenir des informations de hello dont il a besoin à partir de ces en-têtes. Pour les applications ASP.NET 4.6, hello **ClaimsPrincipal** est défini automatiquement avec les valeurs appropriées hello.

Votre application peut également obtenir des informations utilisateur supplémentaires via HTTP GET sur hello `/.auth/me` point de terminaison de votre application. Un jeton valide n’est fourni avec la demande de hello sera retournent une charge JSON avec des détails sur le fournisseur de hello est utilisé, hello jeton du fournisseur sous-jacent et autres informations de l’utilisateur. serveur d’applications mobiles kits de développement logiciel Hello fournissent des méthodes d’assistance toowork avec ces données. Pour plus d’informations, consultez [comment toouse hello Azure Mobile Apps Node.js SDK](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), et [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info).

## <a name="documentation-and-additional-resources"></a>Documentation et ressources supplémentaires
### <a name="identity-providers"></a>Fournisseurs d’identité
Hello suivant didacticiels indiquent comment tooconfigure du Service d’applications toouse différents fournisseurs d’authentification :

* [Comment tooconfigure votre nom de connexion app toouse Azure Active Directory][AAD]
* [Comment tooconfigure votre connexion de Facebook toouse application][Facebook]
* [Comment tooconfigure votre connexion de Google toouse application][Google]
* [Comment tooconfigure votre connexion de Microsoft Account toouse application][MSA]
* [Comment tooconfigure votre connexion de Twitter toouse application][Twitter]

Si vous voulez toouse un système d’identité autre que ceux hello fournies ici, vous pouvez également utiliser hello [afficher un aperçu de la prise en charge de l’authentification personnalisée dans hello Mobile Apps .NET server SDK][custom-auth], qui peut être utilisé dans les applications web, les applications mobiles, ou les applications API.

### <a name="web-applications"></a>Applications web
Hello suivant didacticiels montrent comment tooadd authentification tooa application web :

* [Prise en main d’Azure App Service, 2e partie][web-getstarted]

### <a name="mobile-applications"></a>Applications mobiles
Hello suivant didacticiels montrent comment tooadd authentification tooyour des clients mobiles à l’aide de hello dirigée vers le serveur de flux :

* [Ajouter une application de l’authentification tooyour iOS][iOS]
* [Ajouter une application Android de l’authentification tooyour][Android]
* [Ajouter l’application Windows authentification tooyour][Windows]
* [Ajouter une application de l’authentification tooyour Xamarin.iOS][Xamarin.iOS]
* [Ajouter une application de l’authentification tooyour Xamarin.Android][ Xamarin.Android]
* [Ajouter une application de l’authentification tooyour Xamarin.Forms][Xamarin.Forms]
* [Ajouter l’application de l’authentification tooyour Cordova][Cordova]

Utilisez hello suivant des ressources que toouse hello dirigée vers le client de flux pour Azure Active Directory :

* [Utilisez hello bibliothèque d’authentification Active Directory pour iOS][ADAL-iOS]
* [Utiliser hello bibliothèque d’authentification Active Directory pour Android][ADAL-Android]
* [Utilisez hello Windows Active Directory Authentication Library pour et Xamarin][ADAL-dotnet]

Hello suivant des ressources que toouse hello dirigée vers le client de flux pour Facebook, utilisez :

* [Utilisez hello SDK Facebook pour iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#facebook-sdk)

Utilisez hello suivant des ressources si vous souhaitez toouse hello dirigée vers le client flux Twitter :

* [Twitter Fabric pour iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#twitter-fabric)

Utilisez hello suivant des ressources que toouse hello dirigée vers le client de flux pour Google :

* [Utilisez hello Google connectez-vous SDK pour iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#google-sdk)

### <a name="api-applications"></a>Applications API
Hello suivant didacticiels indiquent comment tooprotect vos applications API :

* [Authentification utilisateur pour API Apps dans Azure App Service][apia-user]
* [Authentification de principal du service pour API Apps dans Azure App Service][apia-service]

[apia-user]: ../app-service-api/app-service-api-dotnet-user-principal-auth.md
[apia-service]: ../app-service-api/app-service-api-dotnet-service-principal-auth.md

[web-getstarted]: ../app-service-web/app-service-web-get-started-2.md#authenticate-your-users

[iOS]: ../app-service-mobile/app-service-mobile-ios-get-started-users.md
[Android]: ../app-service-mobile/app-service-mobile-android-get-started-users.md
[Xamarin.iOS]: ../app-service-mobile/app-service-mobile-xamarin-ios-get-started-users.md
[ Xamarin.Android]: ../app-service-mobile/app-service-mobile-xamarin-android-get-started-users.md
[Xamarin.Forms]: ../app-service-mobile/app-service-mobile-xamarin-forms-get-started-users.md
[Windows]: ../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-users.md
[Cordova]: ../app-service-mobile/app-service-mobile-cordova-get-started-users.md

[AAD]: ../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook]: ../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md
[Google]: ../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md
[MSA]: ../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter]: ../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md

[custom-auth]: ../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth

[ADAL-Android]: ../app-service-mobile/app-service-mobile-android-how-to-use-client-library.md#adal
[ADAL-iOS]: ../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#adal
[ADAL-dotnet]: ../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md#adal
