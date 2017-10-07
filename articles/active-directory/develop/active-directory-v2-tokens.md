---
title: "référence des jetons aaaAzure Active Directory v2.0 | Documents Microsoft"
description: "types Hello de jetons et de revendications émises par le point de terminaison v2.0 hello Azure AD"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: dc58c282-9684-4b38-b151-f3e079f034fd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 29eb5c3402aeae302ee7c6234488520495f85904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-tokens-reference"></a>Informations de référence sur les jetons Azure Active Directory v2.0
point de terminaison Azure Active Directory (Azure AD) v2.0 Hello émet plusieurs types de jetons de sécurité dans chaque [flux d’authentification](active-directory-v2-flows.md). Cette référence décrit hello caractéristiques de sécurité et du contenu de chaque type de jeton.

> [!NOTE]
> point de terminaison Hello v2.0 ne prend pas en charge toutes les fonctionnalités et scénarios d’Azure Active Directory. toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
>
>

## <a name="types-of-tokens"></a>Types de jetons
Hello v2.0 le point de terminaison prend en charge hello [protocole d’autorisation OAuth 2.0](active-directory-v2-protocols.md), qui utilise des jetons d’accès et les jetons d’actualisation. point de terminaison Hello v2.0 prend également en charge l’authentification et l’authentification à l’aide de [OpenID Connect](active-directory-v2-protocols.md). OpenID Connect introduit un troisième type de jeton d’ID de jeton, hello. Chacun de ces jetons est représenté en tant que jeton du *porteur*.

Un jeton de support est un jeton de sécurité léger qu’accorde hello PORTEUR accès tooa une ressource protégée. support de Hello est n’importe quelle partie peut présenter le jeton de hello. Bien qu’un tiers doivent s’authentifier avec un jeton de support tooreceive hello Azure AD, si étapes ne sont pas prises jeton de hello toosecure durant la transmission et de stockage, il peut être interceptée et utilisée par une partie indésirable. Certains jetons de sécurité un mécanisme intégré tooprevent non autorisé tiers disposent de l’utilisation, mais effectuez des jetons de porteur ne pas. doivent donc être acheminés sur un canal sécurisé, par exemple à l’aide du protocole TLS (HTTPS). Si un jeton de support est transmis sans ce type de sécurité, une personne malveillante pourrait utiliser un jeton de hello tooacquire « attaque de man-in-the-middle » et l’utiliser pour la ressource de tooa protégée contre tout accès. Bonjour les mêmes principes de sécurité s’appliquent lors du stockage ou la mise en cache des jetons de support pour une utilisation ultérieure. Veillez systématiquement à ce que votre application transmette et stocke les jetons du porteur. Pour en savoir plus sur les aspects de sécurité des jetons du porteur, consultez [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750).

Nombre de jetons hello émis par le point de terminaison hello v2.0 sont implémentées comme des jetons Web JSON (Jwt). Un jeton Web JSON est un moyen compact et sécurisés pour les URL des informations tootransfer entre deux parties. informations Hello dans un jeton Web JSON sont appelées un *revendication*. Il s’agit d’une assertion de plus d’informations sur le support de hello et l’objet de jeton de hello. revendications Hello dans un jeton Web JSON sont des objets JavaScript Objet Notation (JSON) qui sont codés et sérialisées pour la transmission. Étant donné que les jetons Web JSON hello émis par point de terminaison hello v2.0 sont signés mais pas chiffré, vous pouvez facilement inspecter contenu hello d’un jeton JWT à des fins de débogage. Pour plus d’informations sur les jetons Web JSON, consultez hello [spécification JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Jetons d’ID
Un jeton d’ID est une forme de jeton de sécurité de connexion que votre application reçoit quand elle procède à l’authentification à l’aide [d’OpenID Connect](active-directory-v2-protocols.md). Jetons d’ID sont représentés en tant que [jetons Web JSON](#types-of-tokens), et ils contiennent des revendications que vous pouvez utiliser l’utilisateur de hello toosign dans tooyour application. Vous pouvez utiliser les revendications hello dans un jeton d’ID de différentes manières. Généralement, administrateurs utilisent les informations de compte ID jetons toodisplay ou toomake décisions du contrôle d’accès dans une application. point de terminaison Hello v2.0 ne émet qu’un seul type de jeton d’ID, qui est un ensemble cohérent de revendications, quel que soit le type hello d’utilisateur qui est connecté. format de Hello et le contenu des jetons d’ID sont même hello pour les utilisateurs de compte Microsoft personnels et pour les comptes professionnels ou scolaires.

Pour le moment, les jetons d’ID sont signés, mais pas chiffrés. Lorsque votre application reçoit un jeton d’ID, il doit [valider la signature de hello](#validating-tokens) tooprove hello les authenticité du jeton et valider des réclamations quelques dans tooprove de jeton hello sa validité. Hello revendications validées par une application varient selon les spécifications de scénario, mais votre application doit effectuer certaines [les validations de revendication courantes](#validating-tokens) dans chaque scénario.

Nous vous offrons hello en savoir plus sur les revendications dans les jetons d’ID dans hello suivants sections, en outre le jeton d’ID tooa exemple. Les revendications contenues dans les jetons d’ID ne sont pas retournées dans un ordre spécifique. En outre, de nouvelles revendications peuvent être introduites dans les jetons d’ID à tout moment. Votre application ne doit pas s’arrêter lorsque de nouvelles revendications sont ajoutées. Hello suivant liste inclut les revendications hello que votre application peut interpréter actuellement fiable. Vous trouverez plus de détails dans hello [OpenID Connect de spécification](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-id-token"></a>Exemple de jeton d’ID
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiI2NzMxZGU3Ni0xNGE2LTQ5YWUtOTdiYy02ZWJhNjkxNDM5MWUiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vYjk0MTk4MTgtMDlhZi00OWMyLWIwYzMtNjUzYWRjMWYzNzZlL3YyLjAiLCJpYXQiOjE0NTIyODUzMzEsIm5iZiI6MTQ1MjI4NTMzMSwiZXhwIjoxNDUyMjg5MjMxLCJuYW1lIjoiQmFiZSBSdXRoIiwibm9uY2UiOiIxMjM0NSIsIm9pZCI6ImExZGJkZGU4LWU0ZjktNDU3MS1hZDkzLTMwNTllMzc1MGQyMyIsInByZWZlcnJlZF91c2VybmFtZSI6InRoZWdyZWF0YmFtYmlub0BueXkub25taWNyb3NvZnQuY29tIiwic3ViIjoiTUY0Zi1nZ1dNRWppMTJLeW5KVU5RWnBoYVVUdkxjUXVnNWpkRjJubDAxUSIsInRpZCI6ImI5NDE5ODE4LTA5YWYtNDljMi1iMGMzLTY1M2FkYzFmMzc2ZSIsInZlciI6IjIuMCJ9.p_rYdrtJ1oCmgDBggNHB9O38KTnLCMGbMDODdirdmZbmJcTHiZDdtTc-hguu3krhbtOsoYM2HJeZM3Wsbp_YcfSKDY--X_NobMNsxbT7bqZHxDnA2jTMyrmt5v2EKUnEeVtSiJXyO3JWUq9R0dO-m4o9_8jGP6zHtR62zLaotTBYHmgeKpZgTFB9WtUq8DVdyMn_HSvQEfz-LWqckbcTwM_9RNKoGRVk38KChVJo4z5LkksYRarDo8QgQ7xEKmYmPvRr_I7gvM2bmlZQds2OeqWLB1NSNbFZqyFOCgYn3bAQ-nEQSKwBaA36jYGPOVG2r2Qv1uKcpSOxzxaQybzYpQ
```

> [!TIP]
> Pour pratique, tooinspect hello revendications dans le jeton d’ID exemple hello, collez le jeton d’ID exemple hello dans [calebb.net](http://calebb.net/).
>
>

#### <a name="claims-in-id-tokens"></a>Revendications des jetons d’ID
| Nom | Revendication | Exemple de valeur | Description |
| --- | --- | --- | --- |
| audience |`aud` |`6731de76-14a6-49ae-97bc-6eba6914391e` |Identifie le destinataire prévu de hello du jeton de hello. Dans les jetons de ID, hello s’ID d’Application de votre application, attribué application tooyour Bonjour portail de l’enregistrement des applications Microsoft. Votre application doit valider cette valeur et rejeter le jeton de hello si hello valeur ne correspond pas. |
| émetteur |`iss` |`https://login.microsoftonline.com/b9419818-09af-49c2-b0c3-653adc1f376e/v2.0 ` |Identifie hello service jeton de sécurité (STS) qui crée et retourne le jeton de hello et client Azure AD de hello dans le hello utilisateur a été authentifié. Votre application doit valider la revendication d’émetteur hello tooensure hello jeton provenant de point de terminaison hello v2.0. Il doit également utiliser hello GUID de jeu de hello hello revendications toorestrict clients qui peuvent se connecter toohello application. GUID qui indique que l’utilisateur hello Hello est un utilisateur de consommateur à partir d’un compte Microsoft `9188040d-6c67-4c5b-b112-36a304b66dad`. |
| émis à |`iat` |`1452285331` |heure de Hello à quels hello jeton a été émis, représentée en heure de l’époque. |
| heure d’expiration |`exp` |`1452289231` |temps Hello à quels hello jeton devient non valide, représentée en heure de l’époque. Votre application doit utiliser la revendication tooverify hello validité de cette durée de vie de jeton hello. |
| pas avant |`nbf` |`1452285331` |temps Hello à quels hello jeton devient valide, représentée en heure de l’époque. Il s’agit généralement de même hello comme heure d’émission de hello. Votre application doit utiliser la revendication tooverify hello validité de cette durée de vie de jeton hello. |
| version |`ver` |`2.0` |version de Hello du jeton d’ID hello, tel que défini par Azure AD. Pour le point de terminaison hello v2.0, valeur de hello est `2.0`. |
| ID client |`tid` |`b9419818-09af-49c2-b0c3-653adc1f376e` |Un GUID qui représente le locataire Azure AD de hello hello utilisateur provient. Pour les comptes professionnels et scolaires, hello GUID est client non modifiable de hello ID d’organisation hello qui hello utilisateur appartient. Pour les comptes personnels, valeur de hello est `9188040d-6c67-4c5b-b112-36a304b66dad`. Hello `profile` étendue est requise dans commande tooreceive cette revendication. |
| hachage de code |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hachage de code Hello est incluse dans les jetons de code uniquement lorsque le jeton d’ID hello est émis avec un code d’autorisation OAuth 2.0. Il peut être l’authenticité de hello toovalidate utilisé d’un code d’autorisation. Pour plus d’informations sur l’exécution de cette validation, consultez hello [OpenID Connect de spécification](http://openid.net/specs/openid-connect-core-1_0.html). |
| hachage de jeton d’accès |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hachage de jeton accès Hello est incluse dans les jetons de code uniquement lorsque le jeton d’ID hello est émis avec un jeton d’accès OAuth 2.0. Il peut être l’authenticité de hello toovalidate utilisé d’un jeton d’accès. Pour plus d’informations sur l’exécution de cette validation, consultez hello [OpenID Connect de spécification](http://openid.net/specs/openid-connect-core-1_0.html). |
| nonce |`nonce` |`12345` |valeur à usage unique Hello est une stratégie pour atténuer les attaques par relecture de jetons. Votre application peut spécifier une valeur à usage unique dans une demande d’autorisation à l’aide de hello `nonce` paramètre de requête. valeur Hello vous fournissez dans la demande de hello est émis dans le jeton d’ID hello `nonce` revendication, non modifiée. Votre application peut vérifier la valeur hello par rapport à la valeur hello qu'il spécifié dans la demande de hello, qui associe la session de l’application hello avec un jeton d’ID spécifique. Votre application doit effectuer cette validation pendant le processus de validation du jeton d’ID hello. |
| name |`name` |`Babe Ruth` |revendication de nom Hello fournit une valeur contrôlable de visu qui identifie le sujet hello du jeton de hello. valeur de Hello n’est pas garantie toobe unique, il est mutable, et il est conçu toobe utilisé uniquement à des fins d’affichage. Hello `profile` étendue est requise dans commande tooreceive cette revendication. |
| email |`email` |`thegreatbambino@nyy.onmicrosoft.com` |adresse de messagerie principale Hello associé avec un compte d’utilisateur hello, s’il en existe. Sa valeur est mutable et peut changer au fil du temps. Hello `email` étendue est requise dans commande tooreceive cette revendication. |
| nom d’utilisateur par défaut |`preferred_username` |`thegreatbambino@nyy.onmicrosoft.com` |Bonjour nom d’utilisateur principal qui représente l’utilisateur hello dans le point de terminaison hello v2.0. Il peut s’agir d’une adresse e-mail, d’un numéro de téléphone ou d’un nom d’utilisateur générique sans format spécifié. Sa valeur est mutable et peut changer au fil du temps. Hello `profile` étendue est requise dans commande tooreceive cette revendication. |
| subject |`sub` |`MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q` | Hello principal sur lequel hello jeton déclare les informations, telles qu’utilisateur hello d’une application. Cette valeur est immuable et ne peut pas être réattribuée ou réutilisée. Il peut être utilisé tooperform des contrôles d’autorisation en toute sécurité, notamment lorsque le jeton de hello est tooaccess utilisé une ressource et peut être utilisé en tant que clé dans les tables de base de données. Étant donné que le sujet de hello est toujours présente dans les jetons hello qu’émis par Azure AD, nous vous recommandons d’utiliser cette valeur dans un système d’autorisation à usage général. objet de Hello est, toutefois, un identificateur par paire - il s’agit de l’ID unique tooa application particulière.  Par conséquent, si un seul utilisateur se connecte à deux applications différentes à l’aide de deux ID de client différents, ces applications reçoit deux valeurs différentes pour la revendication de sujet hello.  Ceci peut être souhaitable ou non en fonction de vos besoins d’architecture et de confidentialité. |
| ID d’objet |`oid` |`a1dbdde8-e4f9-4571-ad93-3059e3750d23` | Bonjour identificateur immuable pour un objet hello identité système Microsoft, dans ce cas, un compte d’utilisateur.  Il peut également être des contrôles d’autorisation tooperform utilisés en tant que clé dans les tables de base de données et en toute sécurité. Cet ID identifie l’utilisateur de hello entre les applications - deux applications différentes signature Bonjour même utilisateur recevra hello même valeur Bonjour `oid` de revendication.  Cela signifie qu’il peut être utilisé lors de l’établissement des requêtes tooMicrosoft des services en ligne, par exemple hello Microsoft Graph.  Hello Microsoft Graph retournera cet ID en tant que hello `id` propriété pour un compte d’utilisateur donné.  Étant donné que hello `oid` permet à plusieurs applications toocorrelate utilisateurs, hello `profile` étendue est requise dans commande tooreceive cette revendication. Notez que si un seul utilisateur existe dans plusieurs locataires, utilisateur de hello contient un ID différent dans chaque client, ils sont considérés comme des comptes différents, bien que hello utilisateur se connecte à chaque compte hello les mêmes informations d’identification. |

### <a name="access-tokens"></a>Jetons d’accès
Actuellement, les jetons d’accès émis par le point de terminaison hello v2.0 peuvent être utilisées uniquement par les Services Microsoft. Vos applications ne doivent pas devez tooperform toute validation ou l’inspection des jetons d’accès pour les scénarios de hello actuellement pris en charge. Vous pouvez traiter les jetons d’accès complètement opaques. Ils sont seulement les chaînes que votre application peut passer tooMicrosoft dans les demandes HTTP.

Bonjour future, hello v2.0 près de point de terminaison introduira capacité hello pour les jetons d’accès tooreceive votre application à partir d’autres clients. À ce stade, les informations hello dans cette rubrique de référence mettra à jour avec les informations de hello dont vous avez besoin pour votre validation de jeton d’accès tooperform application et d’autres tâches similaires.

Lorsque vous demandez un jeton d’accès à partir du point de terminaison hello v2.0, point de terminaison hello v2.0 retourne également des métadonnées sur le jeton d’accès hello toouse de votre application. Ces informations comprennent le délai d’expiration hello du jeton d’accès hello et étendues hello pour lequel il est valide. Votre application utilise cette métadonnées tooperform intelligent mise en cache des jetons d’accès sans avoir de jeton d’accès Ouvrir hello tooparse lui-même.

### <a name="refresh-tokens"></a>Jetons d’actualisation
Jetons d’actualisation sont des jetons de sécurité que votre application peut utiliser tooget nouvel accès dans un flux OAuth 2.0. Votre application peut utiliser l’actualisation des jetons tooachieve à long terme accès tooresources part d’un utilisateur sans nécessiter une interaction avec l’utilisateur de hello.

Les jetons d’actualisation prennent en charge plusieurs ressources. Un jeton d’actualisation reçu au cours d’une demande de jeton pour une ressource peut être échangé pour la ressource de l’accès jetons tooa complètement différents.

tooreceive une actualisation dans une réponse de jeton, votre application doit demander et de recevoir hello `offline_acesss` étendue. toolearn plus en détail hello `offline_access` étendue, consultez hello [étendues et consentement](active-directory-v2-scopes.md) l’article.

Jetons d’actualisation sont donc toujours sera, application de tooyour complètement opaque. Ils sont émis par le point de terminaison v2.0 hello Azure AD et peuvent uniquement être inspectés et interprétés par le point de terminaison hello v2.0. Ils sont de longue durées, mais votre application ne doit pas être écrit tooexpect dure un jeton d’actualisation pour une période donnée. Les jetons d’actualisation peuvent être rendus non valides à tout moment pour diverses raisons. Hello la seule façon pour votre tooknow application si un jeton d’actualisation est valide est tooattempt tooredeem il en effectuant un point de terminaison de demande de jeton toohello v2.0.

Lorsque vous utilisez un jeton d’actualisation pour un nouveau jeton d’accès (et si votre application a été accordée hello `offline_access` étendue), vous recevez un nouveau jeton d’actualisation dans la réponse du jeton hello. Enregistrez hello nouvellement émis actualisation jeton, tooreplace hello vous utilisé dans la demande hello. Vous avez ainsi la garantie que vos jetons d’actualisation resteront valides le plus longtemps possible.

## <a name="validating-tokens"></a>Validation des jetons
Actuellement, hello uniquement validation du jeton vos applications devez tooperform valide les jetons de code. toovalidate un jeton d’ID, votre application doit valider signature et hello revendications présentes des deux hello le jeton d’ID dans le jeton d’ID hello.

<!-- TODO: Link -->
Microsoft fournit des bibliothèques et des exemples de code qui vous montrent comment tooeasily gérer la validation du jeton. Dans les sections suivantes hello, nous décrivons hello sous-jacent du processus. Plusieurs bibliothèques open source tierces sont également disponibles pour la validation de jetons JWT. Il existe au moins une bibliothèque pour la plupart des plateformes et langues.

### <a name="validate-hello-signature"></a>Valider la signature de hello
Un jeton Web JSON contient trois segments, qui sont séparés par hello `.` caractère. premier segment de Hello est appelé hello *en-tête*, deuxième segment de hello est hello *corps*, et le troisième segment de hello est hello *signature*. segment de signature Hello peut être l’authenticité de hello toovalidate utilisés de jeton d’ID hello afin qu’elle peut être approuvée par votre application.

Les jetons d’ID sont signés à l’aide d’algorithmes de chiffrement asymétrique standard, tels que RSA 256. en-tête de jeton d’ID hello Hello contient plus d’informations sur la clé de hello et méthode de chiffrement utilisé le jeton de hello toosign. Par exemple :

```
{
  "typ": "JWT",
  "alg": "RS256",
  "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Hello `alg` revendication indique l’algorithme hello qui était le jeton de hello toosign utilisé. Hello `kid` revendication indique la clé publique hello qui était le jeton de hello toosign utilisé.

À tout moment, point de terminaison hello v2.0 peut se connecter à un jeton d’ID à l’aide de l’un d’un ensemble spécifique de paires de clés publique-privée. point de terminaison Hello v2.0 régulièrement fait pivoter le jeu possible de hello de clés, votre application doit être écrite toohandle ces clé change automatiquement. Un toocheck fréquence raisonnable pour les clés publiques de mises à jour toohello utilisé par le point de terminaison hello v2.0 est de 24 heures.

Vous pouvez acquérir hello signature des données clés que vous avez besoin d’une signature de hello toovalidate à l’aide du document de métadonnées OpenID Connect hello situé à :

```
https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration
```

> [!TIP]
> Essayez d’URL hello dans un navigateur !
>
>

Ce document de métadonnées est un objet JSON qui a plusieurs informations, utiles comme emplacement de hello de hello différents points de terminaison requis pour l’authentification de OpenID Connect.  Hello comprend également un *jwks_uri*, ce qui donne l’emplacement de hello de hello du jeu de clés publiques utilisées toosign jetons. document JSON Hello situé hello jwks_uri a toutes les hello informations de clé publique qui est actuellement en cours d’utilisation. Votre application peut utiliser hello `kid` de revendication dans tooselect d’en-tête JWT hello quelle clé publique dans ce document a été toosign utilisé un jeton. Il effectue ensuite la validation des signatures à l’aide d’une clé publique correcte hello et l’algorithme indiqué de hello.

Exécution de la validation de signature est étendue de hello en dehors de ce document. De nombreuses bibliothèques open source sont disponible toohelp vous avec ce.

### <a name="validate-hello-claims"></a>Valider les réclamations de hello
Lorsque votre application reçoit un jeton d’ID lors de l’authentification de l’utilisateur, il doit également effectuer quelques vérifications par rapport aux revendications de hello dans le jeton d’ID hello. Ces vérifications portent notamment sur les revendications suivantes :

* **audience** tooverify qui hello le jeton d’ID a été prévue toobe donné tooyour application de la revendication
* **pas avant** et **délai d’expiration** des revendications, tooverify que le jeton d’ID de hello n’a pas expiré.
* **émetteur** tooverify hello jeton a été émis tooyour application par point de terminaison hello v2.0 de la revendication
* **valeur à usage unique** : il s’agit d’atténuer les attaques par relecture de jetons.

Pour obtenir une liste complète des validations de revendication que votre application doit effectuer, consultez hello [OpenID Connect de spécification](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).

Détails des valeurs attendues de hello pour ces revendications sont inclus dans hello [les jetons ID](# ID tokens) section.

## <a name="token-lifetimes"></a>Durées de vie des jetons
Nous fournissons hello suivant des durées de vie jeton pour votre information uniquement. Hello informations peuvent vous aider à développer et déboguer des applications. Vos applications ne doivent pas être écrites tooexpect une de ces constantes tooremain de durées de vie. car les durées de vie des jetons peuvent changer à tout moment.

| par jeton | Durée de vie | Description |
| --- | --- | --- |
| Jetons d’ID (comptes professionnels ou scolaires) |1 heure |Les jetons d’ID sont généralement valides pendant 1 heure. Votre application web peut utiliser cette même toomaintain de durée de vie sa propre session utilisateur hello (recommandé), ou vous pouvez choisir une durée de vie de session complètement différents. Si votre application a besoin d’un nouveau jeton d’ID de tooget, il doit demande toomake une nouvelle connexion de point de terminaison authorize de toohello v2.0. Si l’utilisateur de hello a une session de navigateur valide avec le point de terminaison hello v2.0, utilisateur de hello ne peut pas tooenter requis leurs informations d’identification de nouveau être. |
| Jetons d’ID (comptes personnels) |24 heures |Les jetons d’ID pour les comptes personnels sont généralement valides 24 heures. Votre application web peut utiliser cette même toomaintain de durée de vie sa propre session utilisateur hello (recommandé), ou vous pouvez choisir une durée de vie de session complètement différents. Si votre application a besoin d’un nouveau jeton d’ID de tooget, il doit demande toomake une nouvelle connexion de point de terminaison authorize de toohello v2.0. Si l’utilisateur de hello a une session de navigateur valide avec le point de terminaison hello v2.0, utilisateur de hello ne peut pas tooenter requis leurs informations d’identification de nouveau être. |
| Jetons d’accès (comptes professionnels ou scolaires) |1 heure |Indiqués dans les réponses de jeton dans le cadre des métadonnées de jeton hello. |
| Jetons d’accès (comptes personnels) |1 heure |Indiqués dans les réponses de jeton dans le cadre des métadonnées de jeton hello. Les jetons d’accès émis au nom de comptes personnels peuvent être configurés pour une durée de vie différente, mais ils sont généralement valides pendant une heure. |
| Jetons d’actualisation (comptes professionnels ou scolaires) |Jours d’activité too14 |Un jeton d’actualisation est valide pendant 14 jours au maximum. Toutefois, un jeton d’actualisation hello peut devenir non valide à tout moment pour diverses raisons, afin que votre application doit continuer tootry toouse un jeton d’actualisation jusqu'à ce qu’il ne parvient pas, ou jusqu'à ce que votre application remplace par un nouveau jeton d’actualisation. En outre, un jeton d’actualisation devient non valide si elle a été 90 jours, car les utilisateurs hello a entré leurs informations d’identification. |
| Jetons d’actualisation (comptes personnels) |Too1 année |Un jeton d’actualisation est valide pendant 1 an au maximum. Toutefois, jeton d’actualisation hello peut-être devenir non valide à tout moment pour diverses raisons, par conséquent, votre application doit continuer tootry toouse un jeton d’actualisation jusqu'à ce qu’il échoue. |
| Codes d’autorisation (comptes professionnels ou scolaires) |10 minutes |Codes d’autorisation sont volontairement de courte durées et doivent être échangés immédiatement pour les jetons d’accès et les jetons d’actualisation lors de la réception des jetons de hello. |
| Codes d’autorisation (comptes personnels) |5 minutes |Codes d’autorisation sont volontairement de courte durées et doivent être échangés immédiatement pour les jetons d’accès et les jetons d’actualisation lors de la réception des jetons de hello. Les codes d’autorisation émis au nom de comptes personnels sont à usage unique. |
