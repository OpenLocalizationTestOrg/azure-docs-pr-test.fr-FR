---
title: aaaAzure Active Directory v2.0 point de terminaison limitations et restrictions | Documents Microsoft
description: Une liste des limitations et restrictions pour le point de terminaison v2.0 hello Azure AD.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a99289c0-e6ce-410c-94f6-c279387b4f66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: bcbb7239f1d117002d16ac23dca8f1feb13a9161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-use-hello-v20-endpoint"></a>Point de terminaison hello v2.0 dois-je utiliser ?
Lorsque vous générez des applications qui s’intègrent à Azure Active Directory, vous devez toodecide si les protocoles d’authentification et le point de terminaison v2.0 hello répondent à vos besoins. Le point de terminaison d’origine d’Azure Active Directory est toujours intégralement pris en charge. À certains égards, il est plus riche en fonctionnalités que le point de terminaison v2.0. Toutefois, hello v2.0 le point de terminaison [présente des avantages significatifs](active-directory-v2-compare.md) pour les développeurs.

Voici notre recommandation simplifiée pour les développeurs à ce stade :

* Si vous devez prendre en charge les comptes Microsoft personnels dans votre application, utilisez le point de terminaison hello v2.0. Mais avant de procéder, assurez-vous que vous comprenez les limitations hello que nous avons abordées dans cet article.
* Si votre application doit uniquement toosupport travail de Microsoft et comptes d’établissement scolaire, n’utilisez pas de point de terminaison hello v2.0. Au lieu de cela, consultez tooour [guide du développeur Azure AD](active-directory-developers-guide.md).

Au fil du temps, point de terminaison hello v2.0 augmente les restrictions de hello tooeliminate répertoriées ici, afin que vous devez toujours point de terminaison toouse hello v2.0. Bonjour attendant, cet article est prévue toohelp vous déterminez si le point de terminaison de hello v2.0 vous convient. Nous continuerons à tooupdate cet état article tooreflect hello actuel du point de terminaison hello v2.0. Vérifiez à nouveau un tooreevaluate vos besoins par rapport aux fonctionnalités de la version 2.0.

Si vous avez une application Azure AD existante qui n’utilise pas de point de terminaison hello v2.0, il n’existe aucun toostart besoin à partir de zéro. Bonjour future, nous proposons un moyen vous toouse vos applications Azure AD existantes avec un point de terminaison hello v2.0.

## <a name="restrictions-on-app-types"></a>Restrictions concernant les types d’applications
Actuellement, hello types d’applications suivants ne sont pas pris en charge par le point de terminaison hello v2.0. Pour obtenir une description des types d’application pris en charge, consultez [types d’application pour le point de terminaison v2.0 hello Azure Active Directory](active-directory-v2-flows.md).

### <a name="standalone-web-apis"></a>API Web autonome
Vous pouvez utiliser le point de terminaison de hello v2.0 trop[générer une API Web sécurisé avec OAuth 2.0](active-directory-v2-flows.md#web-apis). Toutefois, cette API Web peut recevoir des jetons uniquement à partir d’une application qui a hello même ID d’Application. Vous ne pouvez pas accéder à une API web à partir d’un client qui a un ID d’application différent. client de Hello ne seront pas être en mesure de toorequest ou obtenir des autorisations tooyour API Web.

toosee toobuild une API Web qui accepte les jetons à partir d’un client qui a hello même ID d’Application, voir hello exemples d’API Web de point de terminaison v2.0 dans notre [mise en route](active-directory-appmodel-v2-overview.md#getting-started) section.

## <a name="restrictions-on-app-registrations"></a>Restrictions sur les inscriptions d’application
Actuellement, pour chaque application que vous souhaitez toointegrate avec point de terminaison hello v2.0, vous devez créer un enregistrement d’application Bonjour [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList). AD Azure existant ou applications de compte Microsoft ne sont pas compatibles avec le point de terminaison hello v2.0. Les applications qui sont inscrits dans n’importe quel portail autre que hello portail de l’enregistrement d’Application ne sont pas compatibles avec le point de terminaison hello v2.0. Bonjour future, nous prévoyons de tooprovide un toouse de façon une application existante comme une application de la version 2.0. Actuellement, cependant, il n’est aucun chemin de migration pour un toowork d’application existant avec un point de terminaison hello v2.0.

En outre, les inscriptions d’application que vous créez dans hello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ont hello suivant mises en garde :

* Seuls deux secrets d’application sont autorisés par ID d’application.
* Une application inscrite par un utilisateur dans un compte Microsoft personnel ne peut être affichée et gérée que par un compte de développeur. Elle ne peut pas être partagée entre plusieurs développeurs.  Si vous souhaitez que tooshare votre inscription d’une application dans la liste de plusieurs développeurs, vous pouvez créer l’application hello en vous connectant au portail d’inscription hello avec un compte Azure AD.
* Il existe plusieurs restrictions sur le format de hello de redirection de hello URI qui est autorisé. Pour plus d’informations sur l’URI de redirection, consultez la section suivante de hello.

## <a name="restrictions-on-redirect-uris"></a>Restrictions concernant les URI de redirection
Actuellement, les applications qui sont inscrits dans hello portail de l’enregistrement d’Application sont ensemble restreint tooa limité de valeurs d’URI de redirection. Hello redirection URI pour les services et applications web doit commencer par le schéma de hello `https`, et toutes les valeurs d’URI de redirection doivent partager un seul domaine DNS. Par exemple, vous ne pouvez pas inscrire une application web contenant l’un de ces URI de redirection :

`https://login-east.contoso.com`  
`https://login-west.contoso.com`

système d’enregistrement de Hello compare hello ensemble nom DNS de hello redirection URI toohello DNS nom existant de l’URI que vous ajoutez de la redirection hello. le nom DNS hello Hello demande tooadd échoue si une de hello conditions suivantes est vraie :  

* Hello ensemble nom DNS de l’URI de redirection de nouveau hello ne correspond pas nom DNS de hello de l’URI de redirection hello existant.
* Hello ensemble nom DNS de l’URI de redirection de nouveau hello n’est pas un sous-domaine de l’URI de redirection hello existant.

Par exemple, si l’application hello a cet URI de redirection :

`https://login.contoso.com`

Vous pouvez ajouter tooit, comme suit :

`https://login.contoso.com/new`

Dans ce cas, le nom DNS de hello correspond exactement. Vous pouvez aussi définir l’URI suivant :

`https://new.login.contoso.com`

Dans ce cas, vous faites référence sous-domaine DNS de tooa de login.contoso.com. Si vous souhaitez toohave une application ayant east.contoso.com de connexion et de connexion-west.contoso.com comme URI de redirection, vous devez ajouter que les URI de redirection dans cet ordre :

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

Vous pouvez ajouter hello dernier deux car elles sont des sous-domaines de hello tout d’abord URI de redirection, contoso.com. Cette limitation sera supprimée dans une version ultérieure.

toolearn tooregister application Bonjour portail de l’enregistrement d’Application, voir [comment tooregister une application avec un point de terminaison hello v2.0](active-directory-v2-app-registration.md).

## <a name="restrictions-on-services-and-apis"></a>Restrictions concernant les services et API
Actuellement, point de terminaison hello v2.0 prend en charge la connexion pour n’importe quelle application qui est inscrite dans hello portail de l’enregistrement d’Application, et qui se trouve dans la liste des hello [prise en charge des flux d’authentification](active-directory-v2-flows.md). Toutefois, ces applications peuvent obtenir des jetons d’accès OAuth 2.0 pour un ensemble très limité de ressources. problèmes de point de terminaison Hello v2.0 accéder uniquement pour les jetons :

* application Hello qui a demandé le jeton de hello. Une application peut acquérir un jeton d’accès pour lui-même, si l’application logique hello est composée de plusieurs composants différents ou deux niveaux. toosee ce scénario en action, consultez notre [mise en route](active-directory-appmodel-v2-overview.md#getting-started) didacticiels.
* Hello Outlook courrier, calendrier et API REST de Contacts, qui se trouvent dans https://outlook.office.com. toolearn toowrite une application qui accède à ces API, voir hello [Office prise en main](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) didacticiels.
* Les API Microsoft Graph. Vous pouvez en savoir plus sur [Microsoft Graph](https://graph.microsoft.io) et données hello tooyou disponible.

Aucun autre service n’est actuellement pris en charge. Plusieurs services Microsoft Online Services sera ajoutées dans hello future, en outre toosupport pour votre propre les API Web et les services.

## <a name="restrictions-on-libraries-and-sdks"></a>Restrictions concernant les bibliothèques et les SDK
Actuellement, la prise en charge de la bibliothèque de point de terminaison hello v2.0 est limité. Si vous souhaitez toouse hello v2.0 point de terminaison dans une application de production, vous disposez des options suivantes :

* Si vous générez une application web, vous pouvez utiliser en toute sécurité Microsoft généralement disponible intergiciel (middleware) côté serveur tooperform connectez-vous et jeton de validation. Notamment intergiciel (middleware) OWIN Open ID connecter hello pour ASP.NET et hello Node.js Passport plug-in. Pour obtenir des exemples de code qui utilisent le middleware Microsoft, consultez la section [Prise en main](active-directory-appmodel-v2-overview.md#getting-started).
* Si vous créez une application de bureau ou mobile, vous pouvez utiliser l’une de nos bibliothèques d’authentification Microsoft (MSAL).  Ces bibliothèques sont dans une version préliminaire prise en charge de production, afin qu’il soit sécurisé toouse dans les applications de production. Vous pouvez lire plus d’informations sur les conditions de hello Hello afficher un aperçu et hello bibliothèques disponibles dans notre [référence des bibliothèques d’authentification](active-directory-v2-libraries.md).
* Pour les plateformes non couvertes par des bibliothèques de Microsoft, vous pouvez intégrer avec le point de terminaison hello v2.0 par envoi et la réception des messages de protocole dans votre code d’application directement. Hello les protocoles OpenID Connect et OAuth v2.0 [sont expliquées dans](active-directory-v2-protocols.md) toohelp effectuer une intégration de ce type.
* Enfin, vous pouvez utiliser open source ouvrir les ID de connexion et toointegrate de bibliothèques OAuth avec le point de terminaison hello v2.0. protocole de v2.0 Hello doit être compatible avec de nombreuses bibliothèques open source protocole sans modifications majeures. disponibilité Hello de ces types de bibliothèques varie selon le langage et la plateforme. Hello [connecter à Open ID](http://openid.net/connect/) et [OAuth 2.0](http://oauth.net/2/) sites Web maintenir une liste des implémentations courantes. Pour plus d’informations, consultez [bibliothèques v2.0 et l’authentification d’Azure Active Directory](active-directory-v2-libraries.md)et liste hello de bibliothèques open source client et des exemples qui ont été testés avec un point de terminaison hello v2.0.

## <a name="restrictions-on-protocols"></a>Restrictions sur les protocoles
point de terminaison Hello v2.0 ne prend pas en charge SAML ou WS-Federation ; Il prend uniquement en charge les connecter à Open ID et OAuth 2.0.  Pas toutes les fonctionnalités et capacités de protocoles d’OAuth ont été incorporées dans le point de terminaison hello v2.0. Ces fonctionnalités de protocole et les fonctionnalités sont actuellement *non disponible* dans le point de terminaison hello v2.0 :

* ID les jetons émis par le point de terminaison hello v2.0 ne contiennent pas une `email` de revendication pour l’utilisateur de hello, même si vous acquérez une autorisation à partir de hello utilisateur tooview leur courrier électronique.
* point de terminaison UserInfo de connexion OpenID Hello n’est pas implémentée sur le point de terminaison hello v2.0. Toutefois, toutes les données de profil utilisateur que si vous potentiellement à ce point de terminaison est disponible à partir de hello Microsoft Graph `/me` point de terminaison.
* point de terminaison Hello v2.0 ne prend pas en charge émettrices revendications de rôle ou un groupe dans les jetons de l’ID.
* Hello [OAuth 2.0 ressource propriétaire d’informations d’identification de mot de passe Grant](https://tools.ietf.org/html/rfc6749#section-4.3) n’est pas pris en charge par le point de terminaison hello v2.0.

En outre, point de terminaison hello v2.0 ne prend pas en charge toutes les formes de hello SAML ou les protocoles WS-Federation.

toobetter comprendre étendue hello de fonctionnalités d’un protocole pris en charge dans le point de terminaison hello v2.0, lisez notre [référence de protocole OpenID Connect et OAuth 2.0](active-directory-v2-protocols.md).

## <a name="restrictions-for-work-and-school-accounts"></a>Restrictions concernant les comptes professionnels et scolaires
Si vous avez utilisé la bibliothèque d’authentification Active Directory (ADAL) dans les applications Windows, vous pouvez avoir dirigé parti de l’authentification intégrée Windows, qui utilise l’octroi d’assertion hello Security Assertion Markup Language (SAML). Avec cet octroi, les utilisateurs de locataires Azure AD fédérés peuvent s’authentifier en mode silencieux auprès de leur instance d’Active Directory locale sans entrer leurs informations d’identification. Actuellement, hello SAML assertion grant n’est pas pris en charge sur le point de terminaison hello v2.0.
