---
title: "aaaAzure Active Directory v2.0 étendues, les autorisations et consentement | Documents Microsoft"
description: "Description de l’autorisation dans le point de terminaison hello Azure AD v2.0, y compris les étendues, les autorisations et consentement."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 5721d368c435868bfb4ae91cff7fbb9bc4a79b66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scopes-permissions-and-consent-in-hello-azure-active-directory-v20-endpoint"></a>Consentement dans le point de terminaison v2.0 hello Azure Active Directory, les autorisations et les étendues
Les applications intégrées à Azure Active Directory (Azure AD) suivent un modèle d’autorisation, qui permet aux utilisateurs de contrôler le mode d’accès d’une application à leurs données. implémentation de v2.0 Hello du modèle d’autorisation de hello a été mis à jour, et il modifie la façon dont une application doit interagir avec Azure AD. Cet article traite des concepts de base hello de ce modèle d’autorisation, y compris les étendues, les autorisations et consentement.

> [!NOTE]
> point de terminaison Hello v2.0 ne prend pas en charge toutes les fonctionnalités et scénarios d’Azure Active Directory. toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
>
>

## <a name="scopes-and-permissions"></a>Étendues et autorisations
Azure AD implémente hello [OAuth 2.0](active-directory-v2-protocols.md) protocole d’autorisation. OAuth 2.0 est une méthode par le biais de laquelle une application tierce peut accéder aux ressources hébergées sur le web au nom d’un utilisateur. Les ressources hébergées sur le web qui s’intègrent à Azure AD présentent un identificateur de ressource, également appelé *URI d’ID d’application*. Voici, par exemple, quelques-unes des ressources hébergées sur le Web de Microsoft :

* Hello API de messagerie unifiée d’Office 365 :`https://outlook.office.com`
* Hello API Azure AD Graph :`https://graph.windows.net`
* Microsoft Graph : `https://graph.microsoft.com`

Hello qu'est de même pour toutes les ressources de tiers intégrés à Azure AD. Ces ressources peuvent également définir un jeu d’autorisations qui peuvent être des fonctionnalités de hello toodivide utilisé d’une ressource en plus petits. Par exemple, [Microsoft Graph](https://graph.microsoft.io) a défini hello de toodo autorisations suivant de tâches, entre autres :

* Lire le calendrier d’un utilisateur
* Calendrier de l’utilisateur écriture tooa
* Envoi de messages en tant qu’utilisateur

En définissant ces types d’autorisations, les ressources hello possède un contrôle affiné sur ses données et la façon dont les données de salutation sont exposées. Une application tierce peut demander ces autorisations à un utilisateur d’application. utilisateur d’application Hello doit approuver les autorisations hello avant de l’application hello peut agir au nom d’utilisateur hello. Par les fonctionnalités de la ressource hello dans les jeux d’autorisations plus petits de segmentation, les applications tierces peuvent être toorequest intégrée uniquement hello des autorisations spécifiques dont ils ont besoin tooperform leur fonction. Utilisateurs de l’application peuvent savoir exactement comment une application utilise leurs données, et ils peuvent être plus sûr pour que cette application hello ne semble pas fonctionne dans un but malveillant.

Dans Azure AD et OAuth, ces types d’autorisation sont appelés des *étendues*. Ils sont parfois également désignée tooas *oAuth2Permissions*. Une étendue est représentée dans Azure AD en tant que valeur de chaîne. Valeur de la portée hello pour chaque autorisation de poursuivre avec l’exemple de Microsoft Graph hello, est :

* Lire le calendrier d’un utilisateur en utilisant `Calendar.Read`
* Écrire le calendrier de l’utilisateur tooa à l’aide de`Mail.ReadWrite`
* Envoi de messages en tant qu’utilisateur en utilisant `Mail.Send`

Une application peut demander ces autorisations en spécifiant des étendues de hello dans le point de terminaison de demandes toohello v2.0.

## <a name="openid-connect-scopes"></a>Étendues OpenId Connect
implémentation de v2.0 Hello de OpenID Connect a quelques étendues bien définis qui ne s’appliquent pas les ressources spécifiques tooa : `openid`, `email`, `profile`, et `offline_access`.

### <a name="openid"></a>openid
Si une application qui effectue la connexion à l’aide de [OpenID Connect](active-directory-v2-protocols.md), elle doit demander l’autorisation hello `openid` étendue. Hello `openid` montre étendue sur le compte de travail hello page de consentement hello « Connexion vous » l’autorisation et sur le compte Microsoft personnel de hello donner son accord page comme hello l’autorisation « Afficher votre profil et se connecter tooapps et services à l’aide de votre compte Microsoft ». Avec cette autorisation, une application peut recevoir un identificateur unique pour l’utilisateur de hello sous forme de hello Hello `sub` de revendication. Elle donne également le point de terminaison hello application accès toohello UserInfo. Hello `openid` étendue peut être utilisée à hello v2.0 point de terminaison token tooacquire ID jetons, qui peuvent être utilisé toosecure HTTP des appels entre les différents composants d’une application.

### <a name="email"></a>email
Hello `email` étendue peut être utilisée avec hello `openid` étendue et autres. Il donne l’adresse de messagerie principale de l’utilisateur toohello hello application accès sous forme de hello Hello `email` de revendication. Hello `email` revendication est incluse dans un jeton uniquement si une adresse de messagerie est associée au compte d’utilisateur hello, qui n’est pas toujours le cas de hello. Si elle utilise hello `email` étendue, votre application doit être préparée toohandle un cas dans le hello `email` revendication n’existe pas dans le jeton de hello.

### <a name="profile"></a>Profil
Hello `profile` étendue peut être utilisée avec hello `openid` étendue et autres. Elle donne hello application accès tooa beaucoup d’informations sur l’utilisateur de hello. Il peut accéder à des informations Hello inclut, mais ne sont pas limitées pour hello du nom de l’utilisateur, nom de famille, nom d’utilisateur par défaut et l’ID d’objet Pour obtenir une liste complète des revendications de profil hello disponibles dans le paramètre d’id_tokens hello pour un utilisateur spécifique, consultez hello [v2.0 jetons référence](active-directory-v2-tokens.md).

### <a name="offlineaccess"></a>offline_access
Hello [ `offline_access` étendue](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) donne votre tooresources de l’accès d’application pour le compte d’utilisateur de hello pendant une durée prolongée. Sur la page de consentement hello travail compte, cette étendue s’affiche comme hello « Accéder à vos données à tout moment » l’autorisation. Sur hello personnel consentement page de compte Microsoft, il apparaît comme hello « Accéder à vos informations à tout moment » l’autorisation. Quand un utilisateur approuve hello `offline_access` étendue, votre application peut recevoir des jetons d’actualisation à partir du point de terminaison token hello v2.0. Les jetons d’actualisation sont de longue durée. Votre application peut obtenir de nouveaux jetons d’accès lorsque les plus anciens arrivent à expiration.

Si votre application ne demande pas hello `offline_access` étendue, il ne sera pas recevoir des jetons d’actualisation. Cela signifie que lorsque vous utilisez un code d’autorisation Bonjour [flux de code d’autorisation OAuth 2.0](active-directory-v2-protocols.md), vous recevrez un jeton d’accès de hello `/token` point de terminaison. jeton d’accès Hello est valide pendant une courte période. jeton d’accès Hello expire généralement en une heure. À ce stade, votre application doit tooredirect hello utilisateur précédent toohello `/authorize` tooget de point de terminaison un nouveau code d’autorisation. Au cours de cette redirection, en fonction de type hello d’application, utilisateur de hello tooenter leurs informations d’identification de nouveau besoin ou donner son consentement à nouveau toopermissions.

Pour plus d’informations sur la façon dont tooget et utilisez jetons d’actualisation, consultez hello [référence au protocole v2.0](active-directory-v2-protocols.md).

## <a name="requesting-individual-user-consent"></a>Demande de consentement d’utilisateur individuel
Dans un [OpenID Connect ou OAuth 2.0](active-directory-v2-protocols.md) demande d’autorisation, une application peut demander des autorisations de hello dont il a besoin à l’aide de hello `scope` paramètre de requête. Par exemple, lorsqu’un utilisateur se connecte dans l’application de tooan, application hello envoie une requête comme hello exemple suivant (avec les sauts de ligne ajoutés pour une meilleure lisibilité) :

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

Hello `scope` paramètre est une liste séparée par des espaces d’étendues que hello application demande. Chaque étendue est indiqué par l’ajout de l’identificateur de la ressource toohello hello étendue valeur (hello URI ID d’Application). Dans l’exemple de demande hello, hello application besoins autorisation tooread hello calendrier de l’utilisateur et envoyer du courrier en tant qu’utilisateur de hello.

Une fois que l’utilisateur de la hello entre leurs informations d’identification, point de terminaison hello v2.0 vérifie un enregistrement correspondant de *consentement de l’utilisateur*. Si l’utilisateur de hello n’a pas accepté tooany Hello demandé Bonjour passé, les autorisations de point de terminaison hello v2.0 demande hello utilisateur toogrant hello les autorisations demandées.

![Consentement dans le compte professionnel](../../media/active-directory-v2-flows/work_account_consent.png)

Lorsque l’utilisateur de hello approuve l’autorisation de hello, consentement de hello est enregistré pour hello utilisateur ne dispose pas tooconsent à nouveau sur les connexions de compte suivantes.

## <a name="requesting-consent-for-an-entire-tenant"></a>Demande de consentement d’un client entier
Souvent, lorsqu’une organisation achète une licence ou un abonnement pour une application, organisation de hello souhaite que toofully disposition hello application pour ses employés. Dans le cadre de ce processus, un administrateur peut accorder son consentement à tooact d’application hello pour le compte de tous les employés. Si hello admin consentement pour le client entière de hello, hello ses employés ne voyez pas une page de consentement pour l’application hello.

consentement toorequest pour tous les utilisateurs dans un locataire, votre application peut utiliser consentement point de terminaison admin hello.

## <a name="admin-restricted-scopes"></a>Étendues limitées aux administrateurs
Certaines autorisations à privilèges élevés dans l’écosystème de Microsoft hello peuvent être définies trop*restreint aux administrateurs*. Exemples de ces types de portées hello les autorisations suivantes :

* Lire le répertoire d’une organisation à l’aide de `Directory.Read`
* Écrire des données tooan l’annuaire organisation à l’aide de`Directory.ReadWrite`
* Lire des groupes de sécurité dans le répertoire d’une organisation à l’aide de `Groups.Read.All`

Même si un utilisateur de consommateur peut être un toothis d’accès application type de données, les utilisateurs professionnels sont restreints l’octroi de toohello accès même jeu de données d’entreprise sensibles. Si votre application demande tooone d’accès de ces autorisations à partir d’un utilisateur d’organisation, utilisateur de hello reçoit un message d’erreur indiquant qu’ils ne sont pas des autorisations de l’application de tooyour tooconsent autorisés.

Si votre application nécessite un accès restreint tooadmin étendues pour les organisations, vous devez les demander également directement à partir d’un administrateur d’entreprise, à l’aide de hello admin consentement point de terminaison, décrite ci-après.

Lorsqu’un administrateur accorde que ces autorisations via hello admin consentement de point de terminaison, le consentement est accordé pour tous les utilisateurs dans le locataire de hello.

## <a name="using-hello-admin-consent-endpoint"></a>À l’aide du point de terminaison consentement hello admin
Si vous suivez ces étapes, votre application peut rassembler les autorisations pour tous les utilisateurs dans un client, notamment les étendues restreintes aux administrateurs. toosee un exemple de code qui implémente la procédure hello, consultez hello [exemple d’étendues de restreint aux administrateurs](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).

### <a name="request-hello-permissions-in-hello-app-registration-portal"></a>Demander des autorisations dans le portail de l’enregistrement d’application hello hello
1. Accédez application tooyour Bonjour [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou [créer une application](active-directory-v2-app-registration.md) si vous n’avez pas déjà.
2. Recherchez hello **Microsoft Graph autorisations** section, puis ajoutez les autorisations de hello que votre application requiert.
3. Vérifiez que vous **enregistrer** hello d’inscription d’une application.

### <a name="recommended-sign-hello-user-in-tooyour-app"></a>Recommandé : Se connecter hello utilisateur dans l’application de tooyour
En règle générale, lorsque vous générez une application qui utilise le point de terminaison consentement hello admin, application hello a besoin d’une page ou un affichage dans le hello administrateur peut approuver les autorisations de l’application hello. Cette page peut faire partie du flux d’inscription de l’application hello, partie des paramètres de l’application hello, ou il peut être « se connecter » flux dédié. Dans de nombreux cas, il est logique pour hello application tooshow cela « se connecter » afficher uniquement une fois un utilisateur connecté avec un professionnel ou scolaire compte Microsoft.

Lorsque vous vous connectez utilisateur hello dans tooyour application, vous pouvez identifier les organisation hello toowhich hello admin appartient avant de demander les autorisations nécessaires de tooapprove hello. Même si cela n’est pas strictement nécessaire, cela peut vous aider à créer une expérience plus intuitive pour les utilisateurs de l’organisation. toosign hello utilisateur, suivez notre [didacticiels de protocole v2.0](active-directory-v2-protocols.md).

### <a name="request-hello-permissions-from-a-directory-admin"></a>Demander des autorisations hello à partir d’un administrateur d’annuaire
Lorsque vous êtes prêt toorequest les autorisations de l’administrateur de votre organisation, vous pouvez rediriger hello utilisateur toohello v2.0 *point de terminaison admin consentement*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Paramètre | Condition | Description |
| --- | --- | --- |
| locataire |Requis |locataire d’annuaire Hello toorequest autorisation souhaité. Peut être fourni au format GUID ou sous forme de nom convivial. |
| client_id |Requis |Hello Application ID que hello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) affecté tooyour application. |
| redirect_uri |Requis |Hello rediriger URI où vous souhaitez hello toobe de réponse envoyé pour toohandle de votre application. Il doit correspondre exactement à celle de la redirection de hello URI que vous avez enregistré dans le portail de l’enregistrement d’application hello. |
| state |Recommandé |Une valeur incluse dans la demande hello qui s’affichera dans la réponse du jeton hello. Il peut s’agir d’une chaîne du contenu de votre choix. Utilisez hello état tooencode d’informations sur l’état de l’utilisateur hello dans application hello avant de la demande d’authentification hello s’est produite, hello page ou un affichage qu’ils étaient sur. |

À ce stade, Azure AD nécessite une toosign d’administrateur client dans la demande toocomplete hello. administrateur de Hello est demandé tooapprove que tous hello les autorisations que vous avez demandé pour votre application dans le portail de l’enregistrement d’application hello.

#### <a name="successful-response"></a>Réponse correcte
Si hello administrateur approuve les autorisations hello pour votre application, la réponse correcte de hello ressemble à ceci :

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Paramètre | Description |
| --- | --- | --- |
| locataire |locataire d’annuaire Hello qui a accordé les autorisations de hello de votre application il a demandées, au format GUID. |
| state |Une valeur incluse dans la demande hello qui sera également renvoyé dans la réponse du jeton hello. Il peut s’agir d’une chaîne du contenu de votre choix. l’état Hello est tooencode utilisé plus d’informations sur l’état de l’utilisateur hello dans application hello avant de la demande d’authentification hello s’est produite, page de hello ou un affichage qu’ils étaient sur. |
| admin_consent |Est défini trop**true**. |

#### <a name="error-response"></a>Réponse d’erreur
Si l’administrateur de hello n’approuve pas les autorisations hello pour votre application, hello a échoué présente de réponse comme suit :

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Paramètre | Description |
| --- | --- | --- |
| error |Une chaîne de code d’erreur qui peut être utilisés tooclassify des types d’erreurs qui se produisent et peut être utilisé tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur. |

Une fois que vous avez reçu une réponse correcte à partir de la terminaison de consentement admin hello, votre application a obtenu les autorisations hello qu'il demandé. Ensuite, vous pouvez demander un jeton de ressource hello souhaitée.

## <a name="using-permissions"></a>Utilisation des autorisations
Une fois que l’utilisateur de hello donne son consentement toopermissions pour votre application, votre application peut acquérir des jetons d’accès qui représentent les tooaccess d’autorisation de votre application une ressource dans une capacité. Un jeton d’accès peut être utilisé uniquement pour une seule ressource, mais encodé dans le jeton d’accès hello est chaque autorisation que votre application a été accordée pour cette ressource. tooacquire un jeton d’accès, votre application peut effectuer une demande toohello v2.0 jeton point de terminaison, comme suit :

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

Vous pouvez utiliser le jeton d’accès obtenu hello dans la ressource de toohello de demandes HTTP. Il indique fiable ressource toohello que votre application rencontre hello autorisation appropriée tooperform une tâche spécifique.  

Pour plus d’informations sur hello OAuth 2.0, protocole et de jetons d’accès tooget, voir hello [référence de protocole de point de terminaison v2.0](active-directory-v2-protocols.md).
