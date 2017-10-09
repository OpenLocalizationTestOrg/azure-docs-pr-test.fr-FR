---
title: "aaaUse tooaccess d’authentification Azure AD API Azure Media Services avec REST | Documents Microsoft"
description: "Découvrez comment tooaccess API Azure Media Services avec l’authentification Azure Active Directory à l’aide de REST."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 114f7bdde3a8f5fe6189d712e05b6afdc8a8787a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-hello-azure-media-services-api-with-rest"></a>Utilisez Azure AD authentication tooaccess hello API Azure Media Services avec REST

équipe de Azure Media Services Hello a publié la prise en charge de l’authentification Azure Active Directory (Azure AD) pour accéder à Azure Media Services. Il a également annoncé plans toodeprecate Azure Access Control service l’authentification pour l’accès aux Services de support. Étant donné que chaque abonnement Azure et chaque compte Media Services, sont jointe tooan Azure AD client, prise en charge de l’authentification Azure AD apporte de nombreux avantages de sécurité. Pour plus d’informations sur cette modification et de la migration (si vous utilisez hello Media Services .NET SDK pour votre application), voir hello billets de blog et les articles :

- [Azure Media Services announces support for Azure AD and deprecation of Access Control authentication](https://azure.microsoft.com/blog/azure%20media%20service%20aad%20auth%20and%20acs%20deprecation) (Azure Media Services annonce la prise en charge d’Azure AD et déconseille l’authentification Access Control)
- [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md)
- [Utiliser Azure AD authentication tooaccess API Azure Media Services à l’aide de Microsoft .NET](media-services-dotnet-get-started-with-aad.md)
- [Mise en route avec l’authentification Azure AD à l’aide de hello portail Azure](media-services-portal-get-started-with-aad.md)

Certains clients doivent toodevelop leurs solutions de Media Services sous hello suivant contraintes :

*   Ils utilisent un langage de programmation qui n’est pas Microsoft .NET ou c#, ou l’environnement d’exécution hello n’est pas Windows.
*   Les bibliothèques Azure AD telles que des bibliothèques d’authentification Active Directory ne sont pas disponibles pour le langage de programmation de hello ou ne peut pas être utilisés pour leur environnement d’exécution.

Certains clients ont développé des applications à l’aide de l’API REST pour l’authentification Access Control et l’accès à Azure Media Services. Pour ces clients, vous devez un hello uniquement de façon toouse API REST pour l’authentification Azure AD et accéder à Azure Media Services suivantes. Vous devez toonot s’appuient sur une des bibliothèques de hello Azure AD ou sur hello Media Services .NET SDK. Dans cet article, nous décrivons une solution et fournissons des exemples de code pour ce scénario. Code de hello étant tous les appels d’API REST, sans dépendance sur n’importe quel Azure AD ou de la bibliothèque Azure Media Services, hello code peut facilement être traduite tooany autre langage de programmation.

> [!IMPORTANT]
> Actuellement, Media Services prend en charge le modèle d’authentification hello Azure Access Control services. Toutefois, l’authentification Access Control sera déconseillée à compter du 1er juin 2018. Nous vous recommandons de migrer modèle d’authentification Azure AD de toohello dès que possible.


## <a name="design"></a>Conception

Dans cet article, nous utilisons hello après l’authentification et d’autorisation :

*  Protocole d’autorisation : OAuth 2.0. OAuth 2.0 est une norme de sécurité web qui couvre l’authentification et l’autorisation. Elle est prise en charge par Google, Microsoft, Facebook et PayPal. Elle a été ratifiée en octobre 2012. Microsoft prend bien en charge OAuth 2.0 et OpenID Connect. Ces deux normes sont prises en charge dans plusieurs services et bibliothèques clientes, notamment Azure Active Directory, Open Web Interface for .NET (OWIN) Katana, et les bibliothèques Azure AD.
*  Type d’octroi : type d’octroi des informations d’identification du client. Informations d’identification du client est un des types d’allocation quatre hello dans OAuth 2.0. Ce type d’octroi est souvent utilisé pour l’accès à l’API Azure AD Microsoft Graph.
*  Mode d’authentification : principal de service. Hello autre mode d’authentification est utilisateur ou l’authentification interactive.

Un total de quatre applications ou services sont impliqués dans le flux de l’authentification et l’autorisation hello Azure AD pour l’utilisation de Media Services. Hello applications et services et les flux hello, sont décrites dans hello tableau suivant :

|Type d’application |Application |Flux|
|---|---|---|
|Client | Application ou solution cliente | Cette application (en fait, son proxy) est enregistrée dans le locataire Azure AD de hello quels Bonjour Azure media d’abonnement et hello réside le compte de service. Hello principal du service de l’application hello inscrit reçoit ensuite avec un rôle propriétaire ou contributeur Bonjour contrôle d’accès (IAM) du compte de service de support hello. principal du service Hello est représenté par hello client ID client et le secret d’application. |
|Fournisseur d’identité (IDP) | Azure AD en tant que fournisseur d’identité | principal du service application enregistrée Hello (ID client et question secrète du client) est authentifié par Azure AD en tant que hello IDP. Cette authentification est effectuée en interne et de manière implicite. Comme dans les flux d’informations d’identification de client, le client de hello est authentifié au lieu de l’utilisateur de hello. |
|Secure Token Service (STS)/serveur OAuth | Azure AD en tant que STS | Après une authentification par hello IDP (ou serveur OAuth en termes de OAuth 2.0), un jeton d’accès ou un jeton de Web JSON (JWT) émis par Azure AD en tant que serveur STS/OAuth pour la ressource de niveau intermédiaire accès toohello : dans le cas présent, hello le point de terminaison API REST Media Services. |
|Ressource | API REST Media Services | Chaque appel d’API REST Media Services est autorisé par un jeton d’accès qui est émis par Azure AD en tant que serveur STS ou hello OAuth. |

Si vous exécutez l’exemple de code hello et capturez un jeton Web JSON ou un jeton d’accès, hello JWT a hello suivant d’attributs :

    aud: "https://rest.media.azure.net",

    iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    iat: 1497146280,

    nbf: 1497146280,
    exp: 1497150180,

    aio: "Y2ZgYDjuy7SptPzO/muf+uRu1B+ZDQA=",

    appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6",

    appidacr: "1",

    idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    oid: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    sub: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    tid: "72f988bf-86f1-41af-91ab-2d7cd011db47",

Voici les mappages hello entre attributs hello dans hello JSON et hello quatre applications ou services dans le tableau précédent de hello :

|Type d’application |Application |Attribut JWT |
|---|---|---|
|Client |Application ou solution cliente |appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6". ID de client Hello d’une application, vous inscrirez tooAzure AD dans la section suivante de hello. |
|Fournisseur d’identité (IDP) | Azure AD en tant que fournisseur d’identité |idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/".  Hello GUID est un client d’ID de Microsoft hello (microsoft.onmicrosoft.com). Chaque locataire a son propre ID unique. |
|Secure Token Service (STS)/serveur OAuth |Azure AD en tant que STS | iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/". Hello GUID est un client d’ID de Microsoft hello (microsoft.onmicrosoft.com). |
|Ressource | API REST Media Services |aud: "https://rest.media.azure.net". destinataire de Hello ou audience du jeton d’accès hello. |

## <a name="steps-for-setup"></a>Étapes de configuration

tooregister et configurer une application Azure AD pour l’authentification Azure AD et tooobtain un jeton d’accès pour appeler le point de terminaison sur l’API REST de Azure Media Services des hello, hello complète comme suit :

1.  Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), inscrire un client de toohello Azure AD de l’application (par exemple, wzmediaservice) Azure AD (par exemple, microsoft.onmicrosoft.com). Peu importe si l’inscription est faite en tant qu’application web ou application native. En outre, vous pouvez choisir n’importe quelle URL de connexion et URL de réponse (par exemple, http://wzmediaservice.com pour les deux).
2. Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), accédez toohello **configurer** onglet de votre application. Hello de note **ID client**. Ensuite, sous **Clés**, générez une **clé client** (clé secrète client). 

    > [!NOTE] 
    > Prenez note de la clé secrète du client hello. Elle ne s’affichera plus.
    
3.  Bonjour [portail Azure](http://ms.portal.azure.com), passez le compte de service de média toohello. Sélectionnez hello **le contrôle d’accès** volet de (IAM). Ajout d’un membre qui a hello propriétaire ou rôle de collaborateur hello. Pour le principal de hello, recherchez les nom de l’application hello que vous inscrit à l’étape 1 (dans cet exemple, wzmediaservice).

## <a name="info-toocollect"></a>Informations toocollect

tooprepare REST de codage, collecter hello suivant tooinclude de points de données dans le code hello :

*   Azure AD en tant que point de terminaison STS : https://login.microsoftonline.com/microsoft.onmicrosoft.com/oauth2/token. À partir de ce point de terminaison, un jeton d’accès JWT est demandé. En outre tooserving comme un IDP, Azure AD sert également un service STS. Azure AD émet un JWT pour l’accès aux ressources (jeton d’accès). Un jeton JWT a plusieurs revendications.
*   APIT REST Azure Media Services en tant que ressource ou audience : https://rest.media.azure.net.
*   ID client : consultez l’étape 2 dans [Étapes de configuration](#steps-for-setup).
*   Clé secrète client : consultez l’étape 2 dans [Étapes de configuration](#steps-for-setup).
*   Point de terminaison API REST Bonjour suivant le format de compte de vos Services de support :

    https://[media_service_account_name].restv2.[data_center].media.azure.net/API 

    Il s’agit de point de terminaison hello sur les API REST de tous les Media Services dans votre application sont appelées. Par exemple, https://willzhanmswjapan.restv2.japanwest.media.azure.net/API.

Vous pouvez ensuite placer ces cinq paramètres dans votre fichier web.config ou app.config, toouse dans votre code.

## <a name="sample-code"></a>Exemple de code

Vous trouverez un exemple de code hello dans [l’authentification Azure AD pour Azure Media Services Access : à la fois via une API REST](https://github.com/willzhan/WAMSRESTSoln).

exemple de code Hello comporte deux parties :

*   Un projet de bibliothèque DLL contenant tout le code hello API REST pour l’authentification Azure AD et l’autorisation. Il a également une méthode pour rendre les API REST appelle toohello API REST Media Services point de terminaison, avec le jeton d’accès hello.
*   Un client test de console, qui lance l’authentification Azure AD et appelle une autre API REST Media Services.

exemple de projet Hello a trois fonctionnalités :

*   Les authentifications AD Azure via les informations d’identification du client hello accorder à l’aide uniquement hello API REST.
*   Accès Azure Media Services à l’aide uniquement hello API REST.
*   Accès de stockage Azure à l’aide de hello uniquement les API REST (comme toocreate utilisé un compte Media Services, à l’aide des API REST).


## <a name="where-is-hello-refresh-token"></a>Où se trouve le jeton d’actualisation hello ?

Certains lecteurs peuvent demander : où est le jeton d’actualisation hello ? Pourquoi ne pas utiliser un jeton d’actualisation ici ?

objectif de Hello d’un jeton d’actualisation n’est pas toorefresh un jeton d’accès. Au lieu de cela, il est conçue toobypass intervention de l’utilisateur ou l’authentification par l’utilisateur et qu’un jeton d’accès valide au moment de l’expiration d’un jeton antérieur. Il serait peut-être plus clair de parler de « jeton de contournement de la reconnexion utilisateur ».

Si vous utilisez hello OAuth 2.0 (nom d’utilisateur et mot de passe, qui agit pour le compte d’utilisateur) de flux d’octroi de l’autorisation, un jeton d’actualisation vous permet d’obtenir un accès renouvelé jeton sans demander l’intervention de l’utilisateur. Toutefois, pour hello OAuth 2.0, informations d’identification client accorder flux que nous décrivons dans cet article, hello fait Office de pour son propre compte. Vous ne devez pas du tout l’intervention de l’utilisateur, et serveur d’autorisation de hello n’a pas besoin de trop (et ne sera pas) vous donne un jeton d’actualisation. Si vous déboguez hello **GetUrlEncodedJWT** (méthode), vous remarquerez que la réponse hello à partir du point de terminaison token hello a un jeton d’accès, mais aucun jeton d’actualisation.

## <a name="next-steps"></a>Étapes suivantes

Prise en main [téléchargement de fichiers tooyour compte](media-services-dotnet-upload-files.md).
