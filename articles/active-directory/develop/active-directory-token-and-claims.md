---
title: aaaLearn sur hello autre jeton et types pris en charge par Azure AD de revendication | Documents Microsoft
description: "Guide de présentation et évaluation des revendications hello dans hello SAML 2.0 et les jetons les jetons Web JSON (JWT) émis par Azure Active Directory (AAD)"
documentationcenter: na
author: dstrockis
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 166aa18e-1746-4c5e-b382-68338af921e2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: c512894476613e94d86a994c32a8459d6cf00fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-token-reference"></a>Référence de jeton Azure AD
Azure Active Directory (Azure AD) émet plusieurs types de jetons de sécurité dans le traitement de chaque flux d’authentification hello. Ce document décrit hello caractéristiques de sécurité et du contenu de chaque type de jeton.

## <a name="types-of-tokens"></a>Types de jetons
Azure AD prend en charge hello [protocole d’autorisation OAuth 2.0](active-directory-protocols-oauth-code.md), qui utilise à la fois access_tokens et refresh_tokens.  Il prend également en charge l’authentification et l’authentification à l’aide de [OpenID Connect](active-directory-protocols-openid-connect-code.md), ce qui introduit un troisième type de jeton, hello id_token.  Chacun de ces jetons est représenté en tant que « jeton porteur ».

Un jeton de support est un jeton de sécurité léger qu’accorde hello tooa d’accès « support » une ressource protégée. Dans ce sens, hello « support » est une partie capable de présenter le jeton de hello. Bien que l’authentification auprès d’Azure AD est nécessaire dans commande tooreceive un jeton de porteur, étapes doivent être effectuées à l’interception tooprevent jeton, toosecure hello par une partie indésirable. Étant donné que les jetons de support ne sont pas un tiers tooprevent non autorisé de mécanisme intégré à partir de leur utilisation, ils doivent être transportés dans un canal sécurisé, telles que la sécurité de couche de transport (HTTPS). Si un jeton de support est transmis en clair de hello, une attaque hello man-in peut être utilisé tooacquire hello jeton et obtenir des ressources de tooa protégée contre tout accès. Bonjour les mêmes principes de sécurité s’appliquent lors du stockage ou la mise en cache des jetons de support pour une utilisation ultérieure. Veillez systématiquement à ce que votre application transmette et stocke les jetons porteurs de manière sécurisée. Pour en savoir plus sur les aspects de sécurité des jetons porteurs, consultez [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750).

Nombre de jetons hello émis par Azure AD sont implémentés en tant que jetons Web JSON, ou des jetons Web JSON.  Un jeton JWT constitue un moyen compact et sécurisé pour les URL de transférer des informations entre deux parties.  les informations de Hello contenues dans les jetons Web JSON sont appelés « revendications », ou assertions d’informations sur le support de hello et l’objet de jeton de hello.  revendications Hello dans les jetons Web JSON sont les objets JSON encodée et sérialisées pour la transmission.  Étant donné que les jetons Web JSON hello émis par Azure AD est signés, mais pas chiffré, vous pouvez facilement inspecter le contenu hello d’un jeton JWT à des fins de débogage.  Il existe plusieurs outils disponibles pour y parvenir, tels que [jwt.calebb.net](http://jwt.calebb.net). Pour plus d’informations sur les jetons Web JSON, vous pouvez vous reporter toohello [spécification JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

## <a name="idtokens"></a>Jetons id_token
Les jetons id_token constituent une forme de jeton de sécurité de connexion. Votre application les reçoit quand elle procède à l’authentification à l’aide [d’OpenID Connect](active-directory-protocols-openid-connect-code.md).  Ils sont représentés en tant que [jetons Web JSON](#types-of-tokens)et contiennent des revendications que vous pouvez utiliser pour la signature d’utilisateur de hello dans votre application.  Vous pouvez utiliser les revendications hello dans un id_token en tant que vous le souhaitez - ils sont utilisés pour afficher les informations de compte ou de prendre des décisions de contrôle d’accès dans une application.

Les jetons id_token sont signés, mais ils ne sont pas chiffrés pour l’instant.  Lorsque votre application reçoit un id_token, il doit [valider la signature de hello](#validating-tokens) tooprove hello les authenticité du jeton et valider des réclamations quelques dans tooprove de jeton hello sa validité.  Hello revendications validées par une application varient selon les spécifications de scénario, mais il existe quelques [les validations de revendication courantes](#validating-tokens) que votre application doit effectuer dans chaque scénario.

Consultez hello section suivante pour plus d’informations sur les revendications id_tokens, ainsi que d’un id_token exemple.  Notez que les revendications de hello dans id_tokens ne sont pas retournées dans un ordre particulier.  Par ailleurs, de nouvelles revendications peuvent être introduites dans des jetons id_token à n’importe quel moment. L’introduction de nouvelles déclarations ne doit pas altérer votre application.  Hello liste suivante inclut les revendications hello que votre application peut interpréter de façon fiable au moment de hello de rédaction de cet article.  Si nécessaire, encore plus de détails se trouve dans hello [OpenID Connect de spécification](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-idtoken"></a>Exemple de jeton id_token
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ.
```

> [!TIP]
> Pratique, essayez en inspectant les revendications hello dans id_token d’exemple hello en le collant dans [calebb.net](http://jwt.calebb.net).
> 
> 

#### <a name="claims-in-idtokens"></a>Revendications dans les jetons id_token
> [!div class="mx-codeBreakAll"]
| Revendication JWT | Name | Description |
| --- | --- | --- |
| `appid` |ID de l'application |Identifie l’application hello qui utilise tooaccess de jeton hello une ressource. application Hello peut agir en tant que telle ou pour le compte d’un utilisateur. ID de l’application Hello représente généralement un objet d’application, mais il peut également représenter un objet principal de service dans Azure AD. <br><br> **Exemple de valeur JWT** : <br> `"appid":"15CB020F-3984-482A-864D-1D92265E8268"` |
| `aud` |Public ciblé |Hello destiné destinataire du jeton de hello. application Hello qui reçoit le jeton de hello doit vérifier que la valeur de l’audience hello est correcte et rejeter les jetons destinés à une autre audience. <br><br> **Exemple de valeur SAML** : <br> `<AudienceRestriction>`<br>`<Audience>`<br>`https://contoso.com`<br>`</Audience>`<br>`</AudienceRestriction>` <br><br> **Exemple de valeur JWT** : <br> `"aud":"https://contoso.com"` |
| `appidacr` |Référence de classe du contexte d’authentification de l’application |Indique comment les clients hello a été authentifié. Pour un client public, la valeur de hello est 0. Si l’ID client et question secrète du client sont utilisés, la valeur de hello est 1. <br><br> **Exemple de valeur JWT** : <br> `"appidacr": "0"` |
| `acr` |Référence de classe du contexte d'authentification |Indique comment les objet hello a été authentifié en tant que client toohello exécutée dans une revendication d’Application Authentication Context Class Reference hello. Une valeur « 0 » indique que l’authentification de l’utilisateur final hello ne répondait pas aux exigences de hello de norme ISO/CEI 29115. <br><br> **Exemple de valeur JWT** : <br> `"acr": "0"` |
| Moment d’authentification |Enregistrements hello date et heure de l’authentification. <br><br> **Exemple de valeur SAML** : <br> `<AuthnStatement AuthnInstant="2011-12-29T05:35:22.000Z">` | |
| `amr` |Méthode d'authentification |Identifie comment le sujet hello du jeton de hello a été authentifié. <br><br> **Exemple de valeur SAML** : <br> `<AuthnContextClassRef>`<br>`http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod/password`<br>`</AuthnContextClassRef>` <br><br> **Exemple de valeur JWT** : `“amr”: ["pwd"]` |
| `given_name` |Prénom |Fournit des hello tout d’abord, ou « donné « nom d’utilisateur de hello, tel que défini dans l’objet utilisateur de hello Azure AD. <br><br> **Exemple de valeur SAML** : <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname”>`<br>`<AttributeValue>Frank<AttributeValue>` <br><br> **Exemple de valeur JWT** : <br> `"given_name": "Frank"` |
| `groups` |Groupes |Fournit l’ID d’objet qui représentent les appartenances aux groupes du sujet hello. Ces valeurs sont unique (voir ID d’objet) et peuvent être utilisées en toute sécurité pour gérer l’accès, par exemple l’application d’autorisation tooaccess une ressource. groupes de Hello inclus dans la revendication de groupes hello sont configurés sur une base par application, via la propriété « groupMembershipClaims » de hello hello du manifeste d’application. Une valeur Null exclut tous les groupes, une valeur « SecurityGroup » inclut uniquement les appartenances aux groupes de sécurité Active Directory et une valeur « All » inclut les groupes de sécurité et les listes de Distribution Office 365. <br><br> **Exemple de valeur SAML** : <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">`<br>`<AttributeValue>07dd8a60-bf6d-4e17-8844-230b77145381</AttributeValue>` <br><br> **Exemple de valeur JWT** : <br> `“groups”: ["0e129f5b-6b0a-4944-982d-f776045632af", … ]` |
| `idp` |Fournisseur d’identité |Enregistrements hello fournisseur d’identité qui a authentifié le sujet hello du jeton de hello. Cette valeur est identique toohello Hello émetteur de revendication, sauf si le compte d’utilisateur hello est dans un autre client que celui de l’émetteur de hello. <br><br> **Exemple de valeur SAML** : <br> `<Attribute Name=” http://schemas.microsoft.com/identity/claims/identityprovider”>`<br>`<AttributeValue>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/<AttributeValue>` <br><br> **Exemple de valeur JWT** : <br> `"idp":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `iat` |IssuedAt |Stocke l’heure hello à quels hello jeton a été émis. Il est souvent utilisé toomeasure actualisation du jeton. <br><br> **Exemple de valeur SAML** : <br> `<Assertion ID="_d5ec7a9b-8d8f-4b44-8c94-9812612142be" IssueInstant="2014-01-06T20:20:23.085Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">` <br><br> **Exemple de valeur JWT** : <br> `"iat": 1390234181` |
| `iss` |Émetteur |Identifie hello service jeton de sécurité (STS) qui crée et retourne le jeton de hello. Dans les jetons hello retournés par Azure AD, l’émetteur de hello est sts.windows.net. Hello GUID dans la valeur de la revendication émetteur hello est hello des ID de client de Windows Azure AD hello. ID de client Hello est un identificateur immuable et fiable du répertoire de hello. <br><br> **Exemple de valeur SAML** : <br> `<Issuer>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/</Issuer>` <br><br> **Exemple de valeur JWT** : <br>  `"iss":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `family_name` |Nom |Fournit le nom hello, Patronyme ou nom de famille de l’utilisateur de hello tel que défini dans l’objet utilisateur de hello Azure AD. <br><br> **Exemple de valeur SAML** : <br> `<Attribute Name=” http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname”>`<br>`<AttributeValue>Miller<AttributeValue>` <br><br> **Exemple de valeur JWT** : <br> `"family_name": "Miller"` |
| `unique_name` |Nom |Fournit une valeur contrôlable de visu qui identifie le sujet hello du jeton de hello. Cette valeur n’est pas garantie toobe unique au sein d’un client et est conçue toobe utilisé uniquement à des fins d’affichage. <br><br> **Exemple de valeur SAML** : <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name”>`<br>`<AttributeValue>frankm@contoso.com<AttributeValue>` <br><br> **Exemple de valeur JWT** : <br> `"unique_name": "frankm@contoso.com"` |
| `oid` |ID objet |Contient un identificateur unique d’un objet dans Azure AD. Cette valeur est immuable et ne peut pas être réattribuée ou réutilisée. Utilisez hello objet ID tooidentify un objet dans les requêtes tooAzure AD. <br><br> **Exemple de valeur SAML** : <br> `<Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">`<br>`<AttributeValue>528b2ac2-aa9c-45e1-88d4-959b53bc7dd0<AttributeValue>` <br><br> **Exemple de valeur JWT** : <br> `"oid":"528b2ac2-aa9c-45e1-88d4-959b53bc7dd0"` |
| `roles` |contrôleur |Contrôle d’accès représente tous les rôles d’application hello soumises a été accordé à la fois directement et indirectement via l’appartenance au groupe et peut être utilisé tooenforce en fonction du rôle. Les rôles d’application sont définis sur une base par application, via hello `appRoles` propriété hello du manifeste d’application. Hello `value` propriété de chaque rôle d’application est la valeur hello qui apparaît dans la revendication de rôle hello. <br><br> **Exemple de valeur SAML** : <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">`<br>`<AttributeValue>Admin</AttributeValue>` <br><br> **Exemple de valeur JWT** : <br> `“roles”: ["Admin", … ]` |
| `scp` |Scope |Indique hello d’emprunt d’identité des autorisations accordées toohello client application. autorisation de Hello par défaut est `user_impersonation`. propriétaire de Hello Hello ressource sécurisée peut enregistrer des valeurs supplémentaires dans Azure AD. <br><br> **Exemple de valeur JWT** : <br> `"scp": "user_impersonation"` |
| `sub` |Objet |Identifie le principal de hello sur quel hello jeton déclare les informations, telles qu’utilisateur hello d’une application. Cette valeur est immuable et ne peut pas être réassignée ou réutilisée, par conséquent, il peut être utilisé tooperform des contrôles d’autorisation en toute sécurité. Étant donné que l’objet de hello est toujours présent dans hello jetons émis par Azure AD hello, nous vous recommandons d’utiliser cette valeur dans un système d’autorisation d’usage général. <br> `SubjectConfirmation` n’est pas une revendication. Elle décrit comment le sujet hello du jeton de hello est vérifié. `Bearer`Indique que l’objet hello est confirmée par leur possession du jeton de hello. <br><br> **Exemple de valeur SAML** : <br> `<Subject>`<br>`<NameID>S40rgb3XjhFTv6EQTETkEzcgVmToHKRkZUIsJlmLdVc</NameID>`<br>`<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />`<br>`</Subject>` <br><br> **Exemple de valeur JWT** : <br> `"sub":"92d0312b-26b9-4887-a338-7b00fb3c5eab"` |
| `tid` |ID client |Un identificateur immuable et non réutilisable qui identifie le locataire d’annuaire hello qui a émis le jeton de hello. Vous pouvez utiliser des ressources spécifiques du client Active cette tooaccess dans une application mutualisée. Par exemple, vous pouvez utiliser ce client de hello tooidentify valeur dans un toohello d’appel de l’API Graph. <br><br> **Exemple de valeur SAML** : <br> `<Attribute Name=”http://schemas.microsoft.com/identity/claims/tenantid”>`<br>`<AttributeValue>cbb1a5ac-f33b-45fa-9bf5-f37db0fed422<AttributeValue>` <br><br> **Exemple de valeur JWT** : <br> `"tid":"cbb1a5ac-f33b-45fa-9bf5-f37db0fed422"` |
| `nbf`, `exp` |Durée de vie du jeton |Définit l’intervalle de temps hello dans lequel un jeton est valide. service Hello qui valide le jeton de hello doit vérifier que hello date actuelle est dans hello jeton durée de vie, sinon qu'il doit rejeter le jeton de hello. Hello service peut autoriser pour les minutes toofive au-delà de tooaccount de plage de durée de vie de jeton hello les différences d’horloge (« décalage horaire ») entre Azure AD et le service de hello. <br><br> **Exemple de valeur SAML** : <br> `<Conditions`<br>`NotBefore="2013-03-18T21:32:51.261Z"`<br>`NotOnOrAfter="2013-03-18T22:32:51.261Z"`<br>`>` <br><br> **Exemple de valeur JWT** : <br> `"nbf":1363289634, "exp":1363293234` |
| `upn` |Nom d’utilisateur principal |Magasins hello nom d’utilisateur hello principal.<br><br> **Exemple de valeur JWT** : <br> `"upn": frankm@contoso.com` |
| `ver` |Version |Stocke le numéro de version de hello du jeton de hello. <br><br> **Exemple de valeur JWT** : <br> `"ver": "1.0"` |

## <a name="access-tokens"></a>Jetons d’accès
Après une authentification réussie, Azure AD renvoie un jeton d’accès, qui peut être utilisé tooaccess protégé ressources. jeton d’accès Hello est une base 64 encodé JSON Web Token (JWT) et son contenu peut être inspecté en l’exécutant via un décodeur.

Si votre application uniquement *utilise* tooget accès tooAPIs jetons d’accès, vous pouvez (et doivent) traitent les jetons d’accès complètement opaque ; ils sont simplement des chaînes, votre application peut passer tooresources dans les demandes HTTP.

Lorsque vous demandez un jeton d’accès, Azure AD renvoie également des métadonnées sur le jeton d’accès hello pour la consommation de votre application.  Ces informations comprennent le délai d’expiration hello du jeton d’accès hello et étendues hello pour lequel il est valide.  Ainsi, votre tooperform application intelligent mise en cache des jetons d’accès sans avoir à tooparse d’ouvrir le jeton d’accès hello lui-même.

Si votre application est une API protégée par Azure AD, qui attend des jetons d’accès dans les demandes HTTP, vous devez effectuer la validation et l’inspection des jetons hello que vous recevez. Votre application doit effectuer la validation du jeton d’accès hello avant de l’utiliser tooaccess ressources. Pour plus d’informations sur la validation, consultez [Validation des jetons](#validating-tokens).  
Pour plus d’informations sur comment toodo avec .NET, consultez [protéger une API Web à l’aide de jetons de support auprès d’Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

## <a name="refresh-tokens"></a>Jetons d’actualisation

Actualiser les jetons sont des jetons de sécurité, votre application peut utiliser tooacquire nouveau accès dans un flux OAuth 2.0.  Il permet à votre tooresources de l’accès à long terme application tooachieve part d’un utilisateur sans nécessiter une interaction par l’utilisateur de hello.

Les jetons d’actualisation prennent en charge plusieurs ressources.  Qui est toosay un jeton d’actualisation reçu au cours d’une demande de jeton pour une ressource peut être échangée pour les jetons d’accès tooa complètement autre ressource. toodo, hello ensemble `resource` paramètre hello demande toohello ciblé de ressources.

Jetons d’actualisation sont complètement opaques tooyour application. Ils sont de longue durées, mais votre application ne doit pas être écrit tooexpect dure un jeton d’actualisation pour une période donnée.  Les jetons d’actualisation peuvent être rendus non valides à tout moment, et ce pour diverses raisons.  Hello la seule façon pour votre tooknow application si un jeton d’actualisation est valide est tooattempt tooredeem il en effectuant un point de terminaison demande de jeton tooAzure AD jeton.

Lorsque vous utilisez un jeton d’actualisation pour un nouveau jeton d’accès, vous recevez un nouveau jeton d’actualisation dans la réponse du jeton hello.  Vous devez enregistrer jeton d’actualisation hello qui vient d’être émis, en remplaçant hello une que demande de hello.  Vous avez ainsi la garantie que vos jetons d’actualisation resteront valides le plus longtemps possible.

## <a name="validating-tokens"></a>Validation des jetons

Dans l’ordre toovalidate un id_token ou un access_token, votre application doit valider les revendications hello et de signature du jeton de deux hello. Dans les jetons d’accès ordre toovalidate, votre application doit également valider l’émetteur de hello, audience de hello et hello de signature de jetons. Ceux-ci doivent toobe validée par rapport aux valeurs hello dans le document de découverte hello OpenID. Par exemple, la version indépendante de hello client d’un document de hello est située [https://login.microsoftonline.com/common/.well-known/openid-configuration](https://login.microsoftonline.com/common/.well-known/openid-configuration). Intergiciel (middleware) de Azure AD offre des fonctionnalités intégrées pour valider les jetons d’accès, et vous pouvez parcourir notre [exemples](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-code-samples) toofind une en langage hello de votre choix. Pour plus d’informations sur la façon dont tooexplicitly valider un jeton Web JSON, consultez hello [manuelle de l’échantillon validation JWT](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation).  

Nous fournissons des bibliothèques et des exemples de code qui montrent comment tooeasily gèrent la validation des jetons - hello sous informations est fournie simplement pour ceux qui souhaitent hello toounderstand sous-jacent du processus.  Il existe également de nombreuses bibliothèques open source tierces qui permettent de valider les jetons JWT. Quels que soient la plateforme et le langage que vous utilisez, vous avez la quasi-certitude de trouver au moins une option. Pour plus d’informations sur les exemples de code et les bibliothèques d’authentification Azure AD, reportez-vous à la section [Bibliothèques d’authentification Azure AD](active-directory-authentication-libraries.md).

#### <a name="validating-hello-signature"></a>Validation de signature de hello

Un jeton Web JSON contient trois segments, qui sont séparés par hello `.` caractère.  premier segment de Hello est appelé hello **en-tête**, hello seconde sous la forme hello **corps**et hello troisième comme hello **signature**.  segment de signature Hello peut être l’authenticité de hello toovalidate utilisés du jeton de hello afin qu’elle peut être approuvée par votre application.

Les jetons émis par Azure AD sont signés à l’aide d’algorithmes de chiffrement asymétrique standard, tels que RSA 256. en-tête Hello Hello JWT contient des informations sur la clé de hello et méthode de chiffrement utilisé le jeton de hello toosign :

```
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "kriMPdmBvx68skT8-mPAB3BseeA"
}
```

Hello `alg` revendication indique l’algorithme hello qui était le jeton utilisé toosign hello, hello `x5t` revendication indique hello clé publique qui a été de jeton de hello toosign utilisé.

À tout moment, Azure AD peut signer un jeton id_token à l'aide de l'un des ensembles de paires de clés publique-privée. Azure AD fait pivoter l’ensemble possible hello de clés sur une base périodique, votre application doit être écrite toohandle ces clé change automatiquement.  Un toocheck fréquence raisonnable pour les clés publiques de mises à jour toohello utilisé par Azure AD est de 24 heures.

Vous pouvez acquérir hello signature de données de clé nécessaire toovalidate hello de signature à l’aide du document de métadonnées OpenID Connect hello situé à :

```
https://login.microsoftonline.com/common/.well-known/openid-configuration
```

> [!TIP]
> Testez cette URL dans un navigateur !
> 
> 

Ce document de métadonnées est un objet JSON qui contient plusieurs éléments utiles d’information, tels qu’emplacement hello Hello différents points de terminaison requis pour l’authentification du OpenID Connect.  

Il inclut également un `jwks_uri`, ce qui donne l’emplacement de hello de hello du jeu de clés publiques utilisées toosign jetons.  document JSON Hello situé hello `jwks_uri` contient toutes les informations de clé publique hello en cours d’utilisation à ce moment spécifique dans le temps.  Votre application peut utiliser hello `kid` de revendication dans tooselect d’en-tête JWT hello quelle clé publique dans ce document a été toosign utilisé un jeton donné.  Il peut ensuite effectuer la validation de la signature à l’aide d’une clé publique correcte hello et l’algorithme indiqué de hello.

Exécution de la validation de signature est étendue de hello en dehors de ce document : il existe de nombreuses bibliothèques open source disponibles pour vous aider à le faire si nécessaire.

#### <a name="validating-hello-claims"></a>Validation des revendications de hello

Lorsque votre application reçoit un jeton (un id_token lors de l’authentification de l’utilisateur, ou un jeton d’accès en tant que jeton de support dans la demande hello HTTP), il doit également effectuer quelques vérifications par rapport aux revendications de hello dans le jeton de hello.  Ces vérifications portent notamment sur les revendications suivantes :

* Hello **public** revendication - tooverify hello jeton a été prévu toobe donné tooyour application.
* Hello **pas avant** et **délai d’Expiration** de revendications - tooverify hello jeton n’a pas expiré.
* Hello **émetteur** revendication - tooverify hello jeton a été émis en effet tooyour application par Azure AD.
* Hello **Nonce** -toomitigate une attaque par relecture de jetons.
* et bien plus...

Pour obtenir une liste complète des validations de revendication votre application doit effectuer pour les ID de jetons, consultez toohello [OpenID Connect de spécification](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). Détails des valeurs attendues de hello pour ces revendications sont inclus dans hello précédent [id_token section](#id-tokens) section.

## <a name="sample-tokens"></a>Exemples de jeton

Cette section affiche des exemples de jetons SAML et JWT retournés par Azure AD. Ces exemples vous permettent de voir les revendications hello en contexte.

### <a name="saml-token"></a>Jeton SAML

Il s'agit d'un exemple de jeton SAML classique.

    <?xml version="1.0" encoding="UTF-8"?>
    <t:RequestSecurityTokenResponse xmlns:t="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <t:Lifetime>
        <wsu:Created xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T05:15:47.060Z</wsu:Created>
        <wsu:Expires xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T06:15:47.060Z</wsu:Expires>
      </t:Lifetime>
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
          <Address>https://contoso.onmicrosoft.com/MyWebApp</Address>
        </EndpointReference>
      </wsp:AppliesTo>
      <t:RequestedSecurityToken>
        <Assertion xmlns="urn:oasis:names:tc:SAML:2.0:assertion" ID="_3ef08993-846b-41de-99df-b7f3ff77671b" IssueInstant="2014-12-24T05:20:47.060Z" Version="2.0">
          <Issuer>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</Issuer>
          <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
              <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
              <ds:Reference URI="#_3ef08993-846b-41de-99df-b7f3ff77671b">
                <ds:Transforms>
                  <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
                <ds:DigestValue>cV1J580U1pD24hEyGuAxrbtgROVyghCqI32UkER/nDY=</ds:DigestValue>
              </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>j+zPf6mti8Rq4Kyw2NU2nnu0pbJU1z5bR/zDaKaO7FCTdmjUzAvIVfF8pspVR6CbzcYM3HOAmLhuWmBkAAk6qQUBmKsw+XlmF/pB/ivJFdgZSLrtlBs1P/WBV3t04x6fRW4FcIDzh8KhctzJZfS5wGCfYw95er7WJxJi0nU41d7j5HRDidBoXgP755jQu2ZER7wOYZr6ff+ha+/Aj3UMw+8ZtC+WCJC3yyENHDAnp2RfgdElJal68enn668fk8pBDjKDGzbNBO6qBgFPaBT65YvE/tkEmrUxdWkmUKv3y7JWzUYNMD9oUlut93UTyTAIGOs5fvP9ZfK2vNeMVJW7Xg==</ds:SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <X509Data>
                <X509Certificate>MIIDPjCCAabcAwIBAgIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTQwMTAxMDcwMDAwWhcNMTYwMTAxMDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSCWg6q9iYxvJE2NIhSyOiKvqoWCO2GFipgH0sTSAs5FalHQosk9ZNTztX0ywS/AHsBeQPqYygfYVJL6/EgzVuwRk5txr9e3n1uml94fLyq/AXbwo9yAduf4dCHTP8CWR1dnDR+Qnz/4PYlWVEuuHHONOw/blbfdMjhY+C/BYM2E3pRxbohBb3x//CfueV7ddz2LYiH3wjz0QS/7kjPiNCsXcNyKQEOTkbHFi3mu0u13SQwNddhcynd/GTgWN8A+6SN1r4hzpjFKFLbZnBt77ACSiYx+IHK4Mp+NaVEi5wQtSsjQtI++XsokxRDqYLwus1I1SihgbV/STTg5enufuwIDAQABo2IwYDBeBgNVHQEEVzBVgBDLebM6bK3BjWGqIBrBNFeNoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAA4IBAQCJ4JApryF77EKC4zF5bUaBLQHQ1PNtA1uMDbdNVGKCmSp8M65b8h0NwlIjGGGy/unK8P6jWFdm5IlZ0YPTOgzcRZguXDPj7ajyvlVEQ2K2ICvTYiRQqrOhEhZMSSZsTKXFVwNfW6ADDkN3bvVOVbtpty+nBY5UqnI7xbcoHLZ4wYD251uj5+lo13YLnsVrmQ16NCBYq2nQFNPuNJw6t3XUbwBHXpF46aLT1/eGf/7Xx6iy8yPJX4DyrpFTutDz882RWofGEO5t4Cw+zZg70dJ/hH/ODYRMorfXEW+8uKmXMKmX2wyxMKvfiPbTy5LmAU8Jvjs2tLg4rOBcXWLAIarZ</X509Certificate>
              </X509Data>
            </KeyInfo>
          </ds:Signature>
          <Subject>
            <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">m_H3naDei2LNxUmEcWd0BZlNi_jVET1pMLR6iQSuYmo</NameID>
            <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
          </Subject>
          <Conditions NotBefore="2014-12-24T05:15:47.060Z" NotOnOrAfter="2014-12-24T06:15:47.060Z">
            <AudienceRestriction>
              <Audience>https://contoso.onmicrosoft.com/MyWebApp</Audience>
            </AudienceRestriction>
          </Conditions>
          <AttributeStatement>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
              <AttributeValue>a1addde8-e4f9-4571-ad93-3059e3750d23</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/tenantid">
              <AttributeValue>b9411234-09af-49c2-b0c3-653adc1f376e</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
              <AttributeValue>sample.admin@contoso.onmicrosoft.com</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname">
              <AttributeValue>Admin</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname">
              <AttributeValue>Sample</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">
              <AttributeValue>5581e43f-6096-41d4-8ffa-04e560bab39d</AttributeValue>
              <AttributeValue>07dd8a89-bf6d-4e81-8844-230b77145381</AttributeValue>
              <AttributeValue>0e129f4g-6b0a-4944-982d-f776000632af</AttributeValue>
              <AttributeValue>3ee07328-52ef-4739-a89b-109708c22fb5</AttributeValue>
              <AttributeValue>329k14b3-1851-4b94-947f-9a4dacb595f4</AttributeValue>
              <AttributeValue>6e32c650-9b0a-4491-b429-6c60d2ca9a42</AttributeValue>
              <AttributeValue>f3a169a7-9a58-4e8f-9d47-b70029v07424</AttributeValue>
              <AttributeValue>8e2c86b2-b1ad-476d-9574-544d155aa6ff</AttributeValue>
              <AttributeValue>1bf80264-ff24-4866-b22c-6212e5b9a847</AttributeValue>
              <AttributeValue>4075f9c3-072d-4c32-b542-03e6bc678f3e</AttributeValue>
              <AttributeValue>76f80527-f2cd-46f4-8c52-8jvd8bc749b1</AttributeValue>
              <AttributeValue>0ba31460-44d0-42b5-b90c-47b3fcc48e35</AttributeValue>
              <AttributeValue>edd41703-8652-4948-94a7-2d917bba7667</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/identityprovider">
              <AttributeValue>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</AttributeValue>
            </Attribute>
          </AttributeStatement>
          <AuthnStatement AuthnInstant="2014-12-23T18:51:11.000Z">
            <AuthnContext>
              <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
            </AuthnContext>
          </AuthnStatement>
        </Assertion>
      </t:RequestedSecurityToken>
      <t:RequestedAttachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedAttachedReference>
      <t:RequestedUnattachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedUnattachedReference>
      <t:TokenType>http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0</t:TokenType>
      <t:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</t:RequestType>
      <t:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</t:KeyType>
    </t:RequestSecurityTokenResponse>

### <a name="jwt-token---user-impersonation"></a>Jeton JWT - emprunt d'identité de l'utilisateur
Il s’agit d’un exemple de jeton web JSON (JWT) classique utilisé dans un flux d’octroi d’un code d’autorisation.
Dans Ajout tooclaims, jeton de hello inclut un numéro de version dans **ver** et **appidacr**, hello authentification classe référence de contexte, ce qui indique comment les clients hello a été authentifié. Pour un client public, la valeur de hello est 0. Si un ID de client ou de la clé secrète du client a été utilisé, la valeur de hello est 1.

    {
     typ: "JWT",
     alg: "RS256",
     x5t: "kriMPdmBvx68skT8-mPAB3BseeA"
    }.
    {
     aud: "https://contoso.onmicrosoft.com/scratchservice",
     iss: "https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/",
     iat: 1416968588,
     nbf: 1416968588,
     exp: 1416972488,
     ver: "1.0",
     tid: "b9411234-09af-49c2-b0c3-653adc1f376e",
     amr: [
      "pwd"
     ],
     roles: [
      "Admin"
     ],
     oid: "6526e123-0ff9-4fec-ae64-a8d5a77cf287",
     upn: "sample.user@contoso.onmicrosoft.com",
     unique_name: "sample.user@contoso.onmicrosoft.com",
     sub: "yf8C5e_VRkR1egGxJSDt5_olDFay6L5ilBA81hZhQEI",
     family_name: "User",
     given_name: "Sample",
     groups: [
      "0e129f6b-6b0a-4944-982d-f776000632af",
      "323b13b3-1851-4b94-947f-9a4dacb595f4",
      "6e32c250-9b0a-4491-b429-6c60d2ca9a42",
      "f3a161a7-9a58-4e8f-9d47-b70022a07424",
      "8d4c81b2-b1ad-476d-9574-544d155aa6ff",
      "1bf80164-ff24-4866-b19c-6212e5b9a847",
      "76f80127-f2cd-46f4-8c52-8edd8bc749b1",
      "0ba27160-44d0-42b5-b90c-47b3fcc48e35"
     ],
     appid: "b075ddef-0efa-123b-997b-de1337c29185",
     appidacr: "1",
     scp: "user_impersonation",
     acr: "1"
    }.

## <a name="related-content"></a>Contenu connexe
* Consultez hello Azure AD Graph [opérations de stratégie](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) et hello [entité stratégie](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity), toolearn plus d’informations sur la gestion de la stratégie de durée de vie de jeton via hello API Azure AD Graph.
* Pour plus d’informations et des exemples sur la gestion des stratégies par le biais des applets de commande PowerShell, consultez [Durées de vie de jeton configurables dans Azure AD](../active-directory-configurable-token-lifetimes.md) (en anglais). 
