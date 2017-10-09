---
title: "Azure Active Directory B2C : informations de référence sur les jetons | Microsoft Docs"
description: "types Hello des jetons émis dans Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/17/2017
ms.author: dastrock
ms.openlocfilehash: 776bc88cc0308875ac6e576f19ac9edf50319d08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-token-reference"></a>Azure AD B2C: références sur les jetons
Azure Active Directory B2C (Azure AD B2C) émet plusieurs types de jetons de sécurité lors du traitement de chaque [flux d’authentification](active-directory-b2c-apps.md). Ce document décrit hello caractéristiques de sécurité et du contenu de chaque type de jeton.

## <a name="types-of-tokens"></a>Types de jetons
Prend en charge de Azure AD B2C hello [protocole d’autorisation OAuth 2.0](active-directory-b2c-reference-protocols.md), qui utilise les deux jetons d’accès et les jetons d’actualisation. Il prend également en charge l’authentification et l’authentification à l’aide de [OpenID Connect](active-directory-b2c-reference-protocols.md), ce qui introduit un troisième type de jeton : le jeton d’ID hello. Chacun de ces jetons est représenté en tant que jeton du porteur.

Un jeton de support est un jeton de sécurité léger qu’accorde hello tooa d’accès « support » une ressource protégée. support de Hello est n’importe quelle partie peut présenter le jeton de hello. Une partie doit d’abord s’authentifier auprès d’Azure AD pour recevoir un jeton du porteur, Mais si hello nécessaire étapes ne sont pas prises jeton de hello toosecure de transmission et de stockage, il peut être intercepté et utilisé par une partie indésirable. Bien que certains jetons de sécurité intègrent un mécanisme de protection contre l’utilisation par des parties non autorisées, les jetons du porteur n’en sont pas dotés et doivent donc être acheminés sur un canal sécurisé, par exemple à l’aide du protocole TLS (HTTPS).

Si un jeton de support est transmis à l’extérieur d’un canal sécurisé, une personne malveillante peut utiliser un jeton de hello tooacquire attaque de man-in-the-middle et utiliser la ressource de tooa protégé accès toogain non autorisé. Bonjour les mêmes principes de sécurité s’appliquent lorsque des jetons de support sont stockés ou mis en cache pour une utilisation ultérieure. Veillez systématiquement à ce que votre application transmette et stocke les jetons porteurs de manière sécurisée.

Pour en savoir plus sur les aspects de sécurité des jetons du porteur, consultez [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750).

Nombre de jetons hello qui émet d’Azure AD B2C sont implémentées comme des jetons web JSON (Jwt). Un jeton JWT constitue un moyen compact et sécurisé pour les URL de transférer des informations entre deux parties. Les jetons JWT contiennent des informations appelées revendications. Il s’agit des assertions d’informations sur le support de hello et l’objet de hello de jeton de hello. revendications Hello dans les jetons Web JSON sont des objets JSON qui sont codés et sérialisées pour la transmission. Étant donné que hello jetons Web JSON émis par Azure AD B2C sont signés mais pas chiffré, vous pouvez facilement inspecter contenu hello d’un toodebug JWT il. Pour ce faire, plusieurs outils sont à votre disposition, y compris [calebb.net](http://calebb.net). Pour plus d’informations sur les jetons Web JSON, consultez trop[les spécifications de JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Jetons d’ID
Un jeton d’ID est une forme de jeton de sécurité que votre application reçoit hello Azure AD B2C `authorize` et `token` points de terminaison. Jetons d’ID sont représentés en tant que [jetons Web JSON](#types-of-tokens), et ils contiennent des revendications que vous pouvez utiliser tooidentify utilisateurs dans votre application. Lorsque les jetons d’ID sont acquis à partir de hello `authorize` point de terminaison, il s’agit souvent de toosign utilisé dans les applications tooweb les utilisateurs. Lorsque les jetons d’ID sont acquis à partir de hello `token` point de terminaison, elles peuvent être envoyées dans les demandes HTTP pendant la communication entre deux composants de hello même application ou un service. Vous pouvez utiliser les revendications hello dans un jeton d’ID comme vous le souhaitez. Ils sont couramment utilisés toodisplay compte informations ou toomake restrictions d’accès dans une application.  

Les jetons d’ID sont signés, mais ils ne sont actuellement pas chiffrés. Lorsque votre application ou les API reçoit un jeton d’ID, il doit [valider la signature de hello](#token-validation) tooprove hello jeton est authentique. Votre application ou l’API doit également valider des revendications quelques dans tooprove de jeton hello qu’il est valide. Selon les spécifications de scénario hello, revendications hello validées par une application peuvent varier, mais votre application doit effectuer certaines [les validations de revendication courantes](#token-validation) dans chaque scénario.

#### <a name="sample-id-token"></a>Exemple de jeton d’ID
```
// Line breaks for display purposes only

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IklkVG9rZW5TaWduaW5nS2V5Q29udGFpbmVyIn0.
eyJleHAiOjE0NDIzNjAwMzQsIm5iZiI6MTQ0MjM1NjQzNCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9s
b2dpbi5taWNyb3NvZnRvbmxpbmUuY29tLzc3NTUyN2ZmLTlhMzctNDMwNy04YjNkLWNjMzExZjU4ZDkyNS92
Mi4wLyIsImFjciI6ImIyY18xX3NpZ25faW5fc3RvY2siLCJzdWIiOiJOb3Qgc3VwcG9ydGVkIGN1cnJlbnRs
eS4gVXNlIG9pZCBjbGFpbS4iLCJhdWQiOiI5MGMwZmU2My1iY2YyLTQ0ZDUtOGZiNy1iOGJiYzBiMjlkYzYi
LCJpYXQiOjE0NDIzNTY0MzQsImF1dGhfdGltZSI6MTQ0MjM1NjQzNCwiaWRwIjoiZmFjZWJvb2suY29tIn0.
h-uiKcrT882pSKUtWCpj-_3b3vPs3bOWsESAhPMrL-iIIacKc6_uZrWxaWvIYkLra5czBcGKWrYwrAC8ZvQe
DJWZ50WXQrZYODEW1OUwzaD_I1f1HE0c2uvaWdGXBpDEVdsD3ExKaFlKGjFR2V7F-fPThkVDdKmkUDQX3bVc
yyj2V2nlCQ9jd7aGnokTPfLfpOjuIrTsAdPcGpe5hfSEuwYDmqOJjGs9Jp1f-eSNEiCDQOaTBSvr479L5ptP
XWeQZyX2SypN05Rjr05bjZh3j70ZUimiocfJzjibeoDCaQTz907yAg91WYuFOrQxb-5BaUoR7K-O7vxr2M-_
CQhoFA

```

### <a name="access-tokens"></a>Jetons d’accès
Un jeton d’accès est également une forme de jeton de sécurité que votre application reçoit hello Azure AD B2C `authorize` et `token` points de terminaison. Les jetons d’accès sont également représentés en tant que [jetons Web JSON](#types-of-tokens), et ils contiennent des revendications que vous pouvez utiliser hello tooidentify accordé les autorisations tooyour API. Les jetons d’accès sont signés, mais ils ne sont actuellement pas chiffrés. Les jetons d’accès doivent être utilisé tooprovide accéder aux serveurs tooAPIs et de ressources. En savoir plus sur la façon trop[utiliser des jetons d’accès](active-directory-b2c-access-tokens.md). 

Lorsque votre API reçoit un jeton d’accès, il doit [valider la signature de hello](#token-validation) tooprove hello jeton est authentique. Votre API doit également valider certaines revendications dans tooprove de jeton hello qu’il est valide. Selon les spécifications de scénario hello, revendications hello validées par une application peuvent varier, mais votre application doit effectuer certaines [les validations de revendication courantes](#token-validation) dans chaque scénario.

### <a name="claims-in-id-and-access-tokens"></a>Revendications dans les jetons d’ID et d’accès
Lorsque vous utilisez Azure AD B2C, vous avez un contrôle affiné sur le contenu de vos jetons hello. Vous pouvez configurer [stratégies](active-directory-b2c-reference-policies.md) toosend certain des jeux de données utilisateur dans les revendications dont votre application a besoin pour ses opérations. Ces revendications peuvent inclure des propriétés standard tels que l’utilisateur hello `displayName` et `emailAddress`. Elles peuvent également inclure des [attributs d’utilisateur personnalisés](active-directory-b2c-reference-custom-attr.md) que vous pouvez définir dans votre répertoire B2C. Chaque jeton d’ID et d’accès que vous recevez contient un certain ensemble de revendications relatives à la sécurité. Les applications peuvent utiliser ces revendications toosecurely authentifier les utilisateurs et les demandes.

Notez que les revendications de hello dans les jetons d’ID ne sont pas retournées dans un ordre particulier. En outre, de nouvelles revendications peuvent être introduites dans les jetons d’ID à tout moment. Votre application ne doit pas s’arrêter lors de l’ajout de nouvelles revendications. Voici hello revendications que vous prévoyez que les tooexist ID et l’accès des jetons émis par Azure AD B2C. Les éventuelles revendications supplémentaires sont déterminées par des stratégies. Pratique, essayez en inspectant hello les revendications dans le jeton d’ID exemple hello en le collant dans [calebb.net](http://calebb.net). Vous trouverez plus de détails dans hello [OpenID Connect de spécification](http://openid.net/specs/openid-connect-core-1_0.html).

| Nom | Revendication | Exemple de valeur | Description |
| --- | --- | --- | --- |
| Public ciblé |`aud` |`90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6` |Une revendication d’audience identifie le destinataire prévu de hello du jeton de hello. Pour Azure AD B2C, hello s’ID d’application de votre application, en tant qu’application tooyour attribué dans le portail de l’enregistrement d’application hello. Votre application doit valider cette valeur et rejeter le jeton de hello s’il ne correspond pas. |
| Émetteur |`iss` |`https://login.microsoftonline.com/775527ff-9a37-4307-8b3d-cc311f58d925/v2.0/` |Cette revendication identifie hello service jeton de sécurité (STS) qui crée et retourne le jeton de hello. Il identifie également hello Windows Azure AD dans le hello utilisateur a été authentifié. Votre application doit valider la revendication d’émetteur hello tooensure hello jeton provenant de point de terminaison v2.0 hello Azure Active Directory. |
| Émis à |`iat` |`1438535543` |Cette revendication est heure hello à quels hello jeton a été émis, représentée en heure de l’époque. |
| Heure d’expiration |`exp` |`1438539443` |Bonjour revendication d’heure d’expiration est heure hello à quels hello jeton devient non valide, représenté dans le temps de l’époque. Votre application doit utiliser la revendication tooverify hello validité de cette durée de vie de jeton hello. |
| Pas avant |`nbf` |`1438535543` |Cette revendication est heure hello à quels hello jeton devient valide, représenté dans le temps de l’époque. Cela est généralement hello même comme hello temps hello jeton a été émis. Votre application doit utiliser la revendication tooverify hello validité de cette durée de vie de jeton hello. |
| Version |`ver` |`1.0` |Il s’agit de version de hello du jeton d’ID hello, tel que défini par Azure AD. |
| Hachage de code |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Un hachage du code est inclus dans un jeton d’ID uniquement lorsque le jeton de hello est émis avec un code d’autorisation OAuth 2.0. Un hachage du code peut être l’authenticité de hello toovalidate utilisé d’un code d’autorisation. Pour plus d’informations sur la façon de tooperform cette validation, consultez hello [OpenID Connect de spécification](http://openid.net/specs/openid-connect-core-1_0.html).  |
| Hachage de jeton d’accès |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Un hachage de jeton d’accès est inclus dans un jeton d’ID uniquement lorsque le jeton de hello est émis avec un jeton d’accès OAuth 2.0. Un hachage de jeton d’accès peut être l’authenticité de hello toovalidate utilisé d’un jeton d’accès. Pour plus d’informations sur la façon de tooperform cette validation, consultez hello [OpenID Connect de spécification](http://openid.net/specs/openid-connect-core-1_0.html)  |
| Valeur à usage unique |`nonce` |`12345` |Une valeur à usage unique est qu'une stratégie utilisée toomitigate les attaques de relecture de jetons. Votre application peut spécifier une valeur à usage unique dans une demande d’autorisation à l’aide de hello `nonce` paramètre de requête. valeur de Hello que vous fournissez dans la demande hello sera émis tels quels dans hello `nonce` d’un jeton d’ID de revendication. Ainsi, la valeur de hello tooverify application par rapport à la valeur hello qu'il spécifié dans la demande de hello, qui associe la session de l’application hello avec un jeton d’ID donné. Votre application doit effectuer cette validation pendant le processus de validation du jeton d’ID hello. |
| Objet |`sub` |`884408e1-2918-4cz0-b12d-3aa027d7563b` |Il s’agit de principal de hello sur quel hello jeton déclare les informations, telles qu’utilisateur hello d’une application. Cette valeur est immuable et ne peut pas être réattribuée ou réutilisée. Il peut être utilisé tooperform des contrôles d’autorisation en toute sécurité, par exemple lorsque le jeton de hello est tooaccess utilisé une ressource. Par défaut, hello sujet revendication est remplie avec l’ID d’objet hello d’utilisateur hello dans le répertoire de hello. toolearn, voir [Azure Active Directory B2C : configuration de l’authentification unique, de session et de jeton](active-directory-b2c-token-session-sso.md). |
| Référence de classe du contexte d’authentification |`acr` |Non applicable |Ne pas utilisé actuellement, sauf dans les cas de hello des stratégies plus anciennes. toolearn, voir [Azure Active Directory B2C : configuration de l’authentification unique, de session et de jeton](active-directory-b2c-token-session-sso.md). |
| Stratégie d’infrastructure de confiance |`tfp` |`b2c_1_sign_in` |Il s’agit de nom hello de stratégie hello qui a été tooacquire utilisé le jeton d’ID hello. |
| Moment de l’authentification |`auth_time` |`1438535543` |Cette revendication est heure hello auquel une dernière entrée informations d’identification utilisateur, représentée en heure de l’époque. |

### <a name="refresh-tokens"></a>Jetons d’actualisation
Actualiser les jetons sont des jetons de sécurité de votre application peut utiliser les nouveaux jetons d’ID tooacquire et accès dans un flux OAuth 2.0. Ils fournissent votre application avec tooresources d’accès à long terme pour le compte des utilisateurs sans nécessiter une interaction avec les utilisateurs.

tooreceive un jeton d’actualisation dans une réponse de jeton, votre application doit demander l’autorisation hello `offline_acesss` étendue. toolearn plus en détail hello `offline_access` étendue, consultez le toohello [référence de protocole d’Azure AD B2C](active-directory-b2c-reference-protocols.md).

Jetons d’actualisation sont et sera toujours, application de tooyour complètement opaque. Ils sont émis par Azure AD et ne peuvent être inspectés et interprétés que par Azure AD. Ils sont de longue durées, mais votre application ne doit pas être écrit avec attente hello qui dure un jeton d’actualisation pour une période spécifique. Les jetons d’actualisation peuvent être rendus non valides à tout moment, et ce pour diverses raisons. Hello la seule façon pour votre tooknow application si un jeton d’actualisation est valide est tooattempt tooredeem il en effectuant une demande de jeton de tooAzure AD.

Lorsque vous utilisez un jeton d’actualisation pour un nouveau jeton (et si votre application a été accordée hello `offline_access` étendue), vous recevez un nouveau jeton d’actualisation dans la réponse du jeton hello. Vous devez enregistrer le jeton d’actualisation hello qui vient d’être émis. Il doit remplacer le jeton d’actualisation hello que vous avez utilisé précédemment dans la demande hello. Vous avez ainsi la garantie que vos jetons d’actualisation resteront valides le plus longtemps possible.

## <a name="token-validation"></a>Validation du jeton
toovalidate un jeton, votre application doit vérifier la signature de hello et revendications de jeton de hello.

Il existe de nombreuses bibliothèques open source pour valider les jetons JWT en fonction de votre langage préféré. Nous vous recommandons d’explorer ces options plutôt que d’implémenter votre propre logique de validation. informations de Hello dans ce guide peuvent vous aider à apprendre tooproperly utiliser ces bibliothèques.

### <a name="validate-hello-signature"></a>Valider la signature de hello
Un jeton Web JSON inclut trois segments, séparés par hello `.` caractère. Hello premier segment est hello *en-tête*, hello est ensuite hello *corps*, et hello le troisième hello *signature*. segment de signature Hello peut être l’authenticité de hello toovalidate utilisés du jeton de hello afin qu’elle peut être approuvée par votre application.

Les jetons Azure AD B2C sont signés à l’aide d’algorithmes de chiffrement asymétrique standard, tels que RSA 256. en-tête Hello du jeton de hello contient des informations sur la clé de hello et méthode de chiffrement utilisé le jeton de hello toosign :

```
{
        "typ": "JWT",
        "alg": "RS256",
        "kid": "GvnPApfWMdLRi8PDmisFn7bprKg"
}
```

Hello `alg` revendication indique l’algorithme hello qui était le jeton de hello toosign utilisé. Hello `kid` revendication indique hello clé publique qui a été de jeton de hello toosign utilisé.

À tout moment, Azure AD peut signer un jeton à l’aide de l’un des ensembles de paires de clés publique-privée. Azure AD fait pivoter ensemble possible de hello de clés périodiquement, votre application doit être écrite toohandle ces clé change automatiquement. Un toocheck fréquence raisonnable pour les clés publiques de mises à jour toohello utilisé par Azure AD est de 24 heures.

Azure AD B2C a un point de terminaison des métadonnées OpenID Connect. Cela permet aux applications toofetch d’informations sur Azure AD B2C lors de l’exécution. Ces informations incluent les points de terminaison, le contenu des jetons et les clés de signature de jetons. Votre répertoire B2C contient un document de métadonnées JSON pour chaque stratégie. Par exemple, les documents de métadonnées hello pour hello `b2c_1_sign_in` stratégie dans `fabrikamb2c.onmicrosoft.com` se trouve dans :

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in
```

`fabrikamb2c.onmicrosoft.com`est le répertoire de hello B2C utilisé tooauthenticate utilisateur de hello, et `b2c_1_sign_in` est stratégie de hello utilisé le jeton de hello tooacquire. toodetermine stratégie qui a été toosign utilisé un jeton (et où toogo toofetch hello métadonnées), vous avez deux options. Tout d’abord, le nom de la stratégie hello est inclus dans hello `acr` de revendication dans le jeton de hello. Vous pouvez analyser les revendications hors corps hello Hello JSON par le corps de hello décodage à base 64 et la désérialisation hello qui résulte de chaîne JSON. Hello `acr` revendication sera hello de stratégie hello qui était le jeton de hello tooissue utilisé.  L’autre option consiste à stratégie de hello tooencode valeur hello Hello `state` paramètre lorsque vous émettez la demande de hello et décoder toodetermine stratégie qui a été utilisée. Les 2 méthodes sont valides.

document de métadonnées Hello est un objet JSON qui contient plusieurs informations utiles. Ceux-ci incluent l’emplacement de hello de tooperform requis de points de terminaison hello OpenID Connect de l’authentification. Ils comprennent également `jwks_uri`, ce qui donne l’emplacement hello du jeu hello des clés publiques qui sont des jetons de toosign utilisé. Cet emplacement est fourni ici, mais il est meilleur emplacement de hello toofetch dynamiquement à l’aide de document de métadonnées hello et analyse de `jwks_uri`:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in
```

document JSON Hello situé à cette URL contient toutes les informations clés publiques hello en cours d’utilisation à un moment donné. Votre application peut utiliser hello `kid` de revendication dans hello JWT en-tête tooselect hello la clé publique dans le document JSON hello toosign utilisé un jeton donné. Il peut ensuite effectuer une validation de signature à l’aide d’une clé publique correcte hello et l’algorithme indiqué de hello.

Description de la validation des signatures tooperform est étendue de hello en dehors de ce document. De nombreuses bibliothèques open source sont disponible toohelp vous avec cette option si vous en avez besoin.

### <a name="validate-hello-claims"></a>Valider les réclamations de hello
Lorsque votre application ou les API reçoit un jeton d’ID, il doit également effectuer plusieurs vérifications par rapport aux revendications de hello dans le jeton d’ID hello. Ces vérifications portent notamment sur les revendications suivantes :

* Hello **public** de revendications : cette opération vérifie que le jeton d’ID hello a été prévue toobe donné tooyour application.
* Hello **pas avant** et **délai d’expiration** revendications : ces vérifier que le jeton d’ID hello n’a pas expiré.
* Hello **émetteur** de revendications : cette opération vérifie ce jeton hello a été émis tooyour application par Azure AD.
* Hello **nonce**: il s’agit d’une stratégie de prévention des attaques de relecture de jetons.

Pour obtenir une liste complète des contrôles de votre application doit effectuer, consultez toohello [OpenID Connect de spécification](https://openid.net). Détails des valeurs attendues de hello pour ces revendications sont inclus dans hello précédent [jeton section](#types-of-tokens).  

## <a name="token-lifetimes"></a>Durées de vie des jetons
Hello suivant des durées de vie de jeton est fournies toofurther votre base de connaissances. Elles peuvent vous être utiles lorsque vous développez et déboguez des applications. Notez que vos applications ne doivent pas être écrites tooexpect une de ces constantes tooremain de durées de vie. car celles-ci sont amenées à changer à un moment donné. En savoir plus sur hello [personnalisation des durées de vie de jeton](active-directory-b2c-token-session-sso.md) dans Azure AD B2C.

| Jeton | Durée de vie | Description |
| --- | --- | --- |
| Jetons d’ID |1 heure |Les jetons d’ID sont généralement valides 1 heure. Votre application web peut utiliser cette durée de vie toomaintain ses propres sessions avec des utilisateurs (recommandés). Vous pouvez également choisir une durée de vie de session différente. Si votre application a besoin d’un nouveau jeton d’ID de tooget, elle doit simplement toomake un nouveau tooAzure de demande de connexion AD. Si un utilisateur dispose d’une session de navigateur valide auprès d’Azure AD, cet utilisateur peut-être pas les informations d’identification de tooenter requises à nouveau. |
| Jetons d’actualisation |Jours d’activité too14 |Un jeton d’actualisation est valide pendant 14 jours au maximum. Cependant, un jeton d’actualisation peut devenir non valide à tout moment pour différentes raisons. Votre application doit continuer tootry toouse un jeton d’actualisation jusqu'à ce que la demande de hello échoue, ou jusqu'à ce que votre application remplace le jeton d’actualisation hello avec un autre. Un jeton d’actualisation peut également devenir non valide si 90 jours se sont écoulées depuis de l’utilisateur de hello entré en dernier des informations d’identification. |
| Codes d’autorisation |5 minutes |La durée de vie des codes d’autorisation est intentionnellement limitée. Ils doivent être utilisés immédiatement après réception pour les jetons d’accès, les jetons d’ID ou les jetons d’actualisation. |

