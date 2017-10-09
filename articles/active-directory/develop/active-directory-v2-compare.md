---
title: "aaaWhat est différent dans le point de terminaison v2.0 hello Azure AD ? | Microsoft Docs"
description: "Une comparaison entre hello d’origine Azure AD et les points de terminaison hello v2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5060da46-b091-4e25-9fa8-af4ae4359b6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: e7ed196f9053fc21db799cd6bc513ba5c2b92885
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="whats-different-about-hello-v20-endpoint"></a>Quelle est la différence sur le point de terminaison hello v2.0 ?
Si vous êtes familiarisé avec Azure Active Directory ou avez intégré des applications avec Azure AD dans hello passée, il est peut-être des différences dans le point de terminaison hello v2.0 que vous attendez pas.  Pour votre bonne compréhension, ce document énumère ces différences.

> [!NOTE]
> Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.  toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
>

## <a name="microsoft-accounts-and-azure-ad-accounts"></a>Comptes Microsoft et comptes Azure AD
point de terminaison Hello v2.0 permettent aux développeurs toowrite les applications qui acceptent l’authentification à l’aide de comptes Microsoft Accounts et Azure AD, à l’aide d’un point de terminaison d’authentification unique.  Cette offre vous hello toowrite de capacité de votre application complètement indépendant du compte ; Il peut être de type hello de compte d’utilisateur s’inscrit à l’aide de hello ignorant la.  Bien entendu, vous *pouvez* rendez votre application prenant en charge de type hello du compte utilisé dans une session particulière, mais vous n’êtes pas obligé.

Par exemple, si votre application appelle hello [Microsoft Graph](https://graph.microsoft.io), certaines des fonctionnalités supplémentaires et les données seront disponibles tooenterprise utilisateurs, tels que leurs sites SharePoint ou les données d’annuaire.  Mais pour de nombreuses actions, telles que [courrier d’un utilisateur lors de la lecture](https://graph.microsoft.io/docs/api-reference/v1.0/resources/message), code de hello peut être écrits exactement même hello pour les comptes Microsoft Accounts et Azure AD.  

L’intégration de votre application aux comptes Microsoft et Azure AD est désormais un simple processus.  Vous pouvez utiliser un seul jeu de points de terminaison, une bibliothèque unique et une seule application d’enregistrement toogain accès tooboth hello consommateur et entreprise mondes.  toolearn savoir plus sur hello v2.0 le point de terminaison, l’extraction [hello vue d’ensemble](active-directory-appmodel-v2-overview.md).

## <a name="new-app-registration-portal"></a>Nouveau portail d’inscription des applications
tooregister une application qui fonctionne avec le point de terminaison hello v2.0, vous devez utiliser un nouveau portail de l’inscription d’application : [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Il s’agit portail hello où vous pouvez obtenir un ID d’application, personnaliser l’apparence de hello de page de connexion de votre application et bien plus encore.  Il vous suffit de portail de hello tooaccess est un compte Microsoft sous tension - compte personnel ou de travail/school.

## <a name="one-app-id-for-all-platforms"></a>Un ID d’application pour toutes les plateformes
Si vous avez utilisé Azure Active Directory, vous avez probablement inscrit plusieurs applications différentes pour un seul et même projet.  Par exemple, si vous avez créé un site Web et une application iOS, vous aviez tooregister les séparément, à l’aide de deux ID d’Application différent. portail de l’enregistrement d’application Hello Azure AD forcé vous toomake cette distinction lors de l’inscription :

![Ancienne interface utilisateur de l’inscription des applications](../../media/active-directory-v2-flows/old_app_registration.PNG)

De même, si vous aviez un site web et une API web principale, vous avez pu les inscrire chacun en tant qu’application distincte dans Azure AD.  Si vous aviez une application iOS et une application Android, vous pouvez également avoir inscrit deux applications différentes.  L’inscription de chaque composant d’application conduit toosome des comportements inattendus pour les développeurs et leurs clients :

* Chaque composant a été trouvé en tant qu’une application distincte dans le locataire d’Azure Active Directory hello de chaque client.
* Lorsqu’un administrateur client a tenté de stratégie tooapply pour gérer l’accès à ou supprimer une application, ils auraient pas toodo c’est le cas pour chaque composant de l’application hello.
* Lorsque les clients consentement tooan application, chaque composant apparaît dans l’écran de consentement hello comme une application distincte.

Avec le point de terminaison hello v2.0, vous pouvez maintenant inscrire tous les composants de votre projet en tant qu’une inscription d’une application unique et utiliser un Id unique de l’Application pour l’ensemble du projet.  Vous pouvez ajouter plusieurs « plateformes » tooa chaque projet et fournissent les données appropriées hello pour chaque plateforme que vous ajoutez.  Bien entendu, vous pouvez créer autant d’applications que vous souhaitez selon vos besoins, mais pour la majorité de hello de cas qu’un seul Id de l’Application doit être nécessaire.

Notre objectif est que va entraîner la gestion des applications tooa plus simplifié et l’expérience de développement et une vue consolidée de plus d’un projet unique que vous travaillez peut-être sur.

## <a name="scopes-not-resources"></a>Des étendues, pas des ressources
Dans Azure Active Directory, une application peut se comporter comme une **ressource**, ou un destinataire de jetons.  Une ressource peut définir un nombre de **étendues** ou **oAuth2Permissions** comprenant, autorisant les applications clientes ressource de toothat de jetons toorequest pour un ensemble d’étendues.  Tenez compte des API d’Azure AD Graph hello comme exemple d’une ressource :

* Identificateur de ressource, ou `AppID URI` : `https://graph.windows.net/`
* Étendues, ou `OAuth2Permissions` : `Directory.Read`, `Directory.Write`, etc.  

Tout ceci est vrai pour point de terminaison hello hello v2.0.  Une application peut toujours se comporter comme une ressource, définir des étendues et être identifiée par un URI.  Les applications clientes peuvent toujours demander des étendues toothose d’accès.  Toutefois, hello dans laquelle un client demande des autorisations a été modifiée.  Bonjour passé, une OAuth 2.0 autorisent tooAzure demande QU'AD ont présentait :

```
GET https://login.microsoftonline.com/common/oauth2/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&resource=https%3A%2F%2Fgraph.windows.net%2F
...
```

où hello **ressource** paramètre indiqué ressource hello client application demande l’autorisation pour.  Azure AD calculée autorisations hello requises par l’application hello basé sur la configuration statique Bonjour Azure Portal et jetons émis en conséquence.  Maintenant, hello même OAuth 2.0 autorisent demande ressemble :

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

où hello **étendue** paramètre indique quelle application hello ressource et les autorisations demande d’autorisation pour. Hello souhaité de ressource est toujours très présente dans la demande de hello - il est simplement incluse dans chacune des valeurs de paramètre d’étendue hello d’hello.  À l’aide du paramètre d’étendue hello de cette manière permet toobe de point de terminaison v2.0 hello plus conforme à la spécification de hello OAuth 2.0 et est mieux adaptée aux pratiques du secteur commun.  Il permet également d’applications tooperform [consentement incrémentielle](#incremental-and-dynamic-consent), qui est décrite dans la section suivante de hello.

## <a name="incremental-and-dynamic-consent"></a>Consentement incrémentiel et dynamique
Applications inscrit dans Azure AD précédemment nécessaire toospecify leurs autorisations OAuth 2.0 requises Bonjour portail Azure, au moment de la création d’application :

![Interface utilisateur de l’inscription des autorisations](../../media/active-directory-v2-flows/app_reg_permissions.PNG)

autorisations Hello une application requis ont été configurés **statiquement**.  Alors que cela autorisé de configuration de hello application tooexist Bonjour portail Azure tout en conservant les code hello agréable et simple, il présente quelques problèmes pour les développeurs :

* Une application a tooknow toutes les autorisations hello il faudrait jamais au moment de la création d’application.  L’ajout d’autorisations au fil du temps était un processus difficile.
* Une application a tooknow toutes les ressources hello il serait jamais accéder avance.  Il était difficile toocreate applications auxquels ont accès à un nombre arbitraire de ressources.
* Une application devait toorequest toutes les autorisations hello qu'il faudrait jamais lors de l’utilisateur hello première connexion.  Dans certains cas, cela conduit tooa très longue liste d’autorisations, ce qui est déconseillé aux utilisateurs finaux à partir de l’approbation des accès de l’application hello lors de l’authentification initiale.

Avec le point de terminaison hello v2.0, vous pouvez spécifier des autorisations de hello les besoins de votre application **dynamiquement**, lors de l’exécution, au cours d’utilisation de votre application.  toodo, vous pouvez spécifier hello étendues de vos besoins de l’application à un moment donné dans le temps en les incluant dans hello `scope` paramètre d’une demande d’autorisation :

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

Hello ci-dessus demande l’autorisation pour hello application tooread d’un utilisateur Azure AD données d’annuaire, ainsi qu’écriture données tootheir à l’annuaire.  Si l’utilisateur de hello a consenti autorisations toothose Bonjour passées pour cette application, ils seront simplement entrent leurs informations d’identification et être connectés à l’application hello.  Si l’utilisateur de hello a consenti pas tooany de ces autorisations, point de terminaison hello v2.0 demande hello utilisateur pour les autorisations de toothose de consentement.  toolearn plus, vous pouvez lire sur [autorisations consentement et étendues](active-directory-v2-scopes.md).

Autorisations toorequest dynamiquement via hello permettant d’une application `scope` paramètre vous donne un contrôle total sur l’expérience utilisateur.  Si vous le souhaitez, vous pouvez choisir toofrontload votre consentement expérience et demandez pour toutes les autorisations dans une demande d’autorisation initiale.  Ou, si votre application nécessite un grand nombre d’autorisations, vous pouvez choisir toogather ces autorisations à partir de l’utilisateur de hello incrémentielle, alors qu’ils tentent toouse certaines fonctionnalités de votre application au fil du temps.

## <a name="well-known-scopes"></a>Étendues connues
#### <a name="offline-access"></a>Accès hors connexion
Applications à l’aide du point de terminaison hello v2.0 peuvent nécessiter hello utilisation d’une nouvelle autorisation bien connue pour les applications - hello `offline_access` étendue.  Toutes les applications devez toorequest cette autorisation si elles ont besoin de tooaccess ressources procuration hello d’un utilisateur pour une période prolongée, même quand l’utilisateur de hello utilise ne peut-être pas activement application hello.  Hello `offline_access` étendue apparaîtra utilisateur toohello un consentement boîtes de dialogue en tant que « Accéder à vos données en mode hors connexion », les utilisateurs qui hello doivent accepter.  Demande hello `offline_access` autorisation activera votre tooreceive d’application web refresh_tokens OAuth 2.0 à partir du point de terminaison hello v2.0.  Les jetons d’actualisation sont de longue durée, et peuvent être échangés contre les nouveaux jetons d’accès OAuth 2.0 pour des périodes d’accès prolongées.  

Si votre application ne demande pas hello `offline_access` étendue, elle ne recevra pas refresh_tokens.  Cela signifie que lorsque vous utilisez un authorization_code dans le flux de code d’autorisation hello OAuth 2.0, vous ne recevrez que dans un access_token de hello `/token` point de terminaison.  Ce jeton d’accès demeure valide pendant une courte période (généralement une heure), avant d’arriver à expiration.  À ce moment précis, votre application devez tooredirect hello utilisateur précédent toohello `/authorize` tooretrieve de point de terminaison un nouveau authorization_code.  Au cours de cette redirection, utilisateur de hello parfois pas tooenter leurs informations d’identification de nouveau besoin ou nouveau consentement toopermissions, selon le type de hello hello d’application.

toolearn plus d’informations sur OAuth 2.0, refresh_tokens et access_tokens, extraction hello [référence au protocole v2.0](active-directory-v2-protocols.md).

#### <a name="openid-profile-and-email"></a>OpenID, profile et email
Historiquement, hello plus basique OpenID Connect flux de connexion avec Azure Active Directory fournit une mine d’informations sur l’utilisateur hello dans id_token résultant de hello.  revendications Hello dans un id_token peuvent inclure l’utilisateur hello nom, nom d’utilisateur par défaut, adresse de messagerie, ID d’objet et bien plus encore.

Nous sommes maintenant limitant les informations hello que hello `openid` étendue permet à votre application l’accès.  Hello 'openid' étendue sera uniquement autoriser votre application toosign hello utilisateur et recevoir un identificateur spécifique à l’application pour l’utilisateur de hello.  Si vous souhaitez tooobtain informations d’identification personnelle (PII) sur l’utilisateur de hello dans votre application, toorequest des autorisations supplémentaires à partir de l’utilisateur de hello est nécessaire à votre application.  Nous vous présentons deux étendues : hello `email` et `profile` étendues – qui vous toodo donc.

Hello `email` étendue est très simple : il permet d’adresse de messagerie principale de votre application l’accès toohello l’utilisateur via hello `email` hello id_token de revendication.  Hello `profile` étendue permet à votre tooall d’accès application autres informations de base utilisateur hello-le nom, le nom d’utilisateur par défaut, ID d’objet et ainsi de suite.

Cela vous permet de toocode votre application de façon minimale divulgation – vous pouvez demander seulement utilisateur de hello pour hello information que votre application requiert toodo son travail.  Pour plus d’informations sur ces étendues, consultez trop[hello référence d’étendue v2.0](active-directory-v2-scopes.md).

## <a name="token-claims"></a>Demandes de jetons
revendications de Hello dans les jetons émis par le point de terminaison hello v2.0 ne sera pas tootokens identiques émis par les points de terminaison hello généralement disponible Azure AD - toohello nouveau service de migration des applications ne doivent pas supposer qu'une revendication spécifique existe dans id_tokens ou access_tokens. toolearn sur les revendications spécifiques hello émis dans les jetons v2.0, consultez hello [référence de jeton v2.0](active-directory-v2-tokens.md).

## <a name="limitations"></a>Limites
Il existe quelques restrictions toobe connaître lors de l’utilisation du point de v2.0 hello.  Reportez-vous toohello [doc de limitations v2.0](active-directory-v2-limitations.md) toosee si ces restrictions s’appliquent tooyour scénario en particulier.
