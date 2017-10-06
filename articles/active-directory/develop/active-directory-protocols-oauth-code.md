---
title: "aaaUnderstand hello flux de code d’autorisation OAuth 2.0 dans Azure AD | Documents Microsoft"
description: "Cet article décrit comment accéder à toouse HTTP messages tooauthorize tooweb applications et API web dans votre client à l’aide d’Azure Active Directory et OAuth 2.0."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: de3412cb-5fde-4eca-903a-4e9c74db68f2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4a6fe67d786a5fcb87d1059c2e94ba0c88d26cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Autoriser les applications tooweb à l’aide d’OAuth 2.0 et Azure Active Directory
Azure Active Directory (Azure AD) utilise OAuth 2.0 tooenable vous tooauthorize, accéder aux applications tooweb et API web dans votre locataire Azure AD. Ce guide est indépendante du langage et décrit comment toosend et recevoir des messages HTTP sans utiliser l’un de nos bibliothèques open source.

Hello flux de code d’autorisation OAuth 2.0 est décrit dans [section 4.1 de spécification de hello OAuth 2.0](https://tools.ietf.org/html/rfc6749#section-4.1). Il est utilisé tooperform l’authentification et l’autorisation dans la plupart des types d’applications, y compris les applications web et applications ont été installées en mode natif.

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## Flux d’autorisation OAuth 2.0
À un niveau élevé, les flux d’autorisation entière hello pour une application ressemble un peu à ceci :

![Flux de code d’authentification OAuth](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## Demander un code d’autorisation
flux de code d’autorisation Hello commence par client hello dirigeant hello utilisateur toohello `/authorize` point de terminaison. Dans cette demande, client de hello indique les autorisations hello tooacquire à partir de l’utilisateur de hello. Vous pouvez obtenir des points de terminaison hello OAuth 2.0 à partir de la page de votre application dans le portail Azure Classic Bonjour **points de terminaison** bouton dans le tiroir inférieur de hello.

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https%3A%2F%2Fservice.contoso.com%2F
&state=12345
```

| Paramètre |  | Description |
| --- | --- | --- |
| locataire |required |Hello `{tenant}` valeur de chemin d’accès de hello de demande de hello peut être utilisé toocontrol qui peut se connecter à l’application hello.  Hello valeurs autorisées sont des identificateurs de client, par exemple, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` ou `common` pour les jetons d’indépendant du locataire |
| client_id |required |Hello Id d’Application attribué tooyour application lorsque vous avez l’inscrit auprès d’Azure AD. Vous pouvez le trouver dans hello portail Azure. Cliquez sur **Active Directory**, cliquez sur le répertoire hello, choisissez l’application hello et cliquez sur **configurer** |
| response_type |required |Doit inclure `code` pour les flux de code d’autorisation hello. |
| redirect_uri |recommandé |Bonjour redirect_uri de votre application, où les réponses d’authentification peuvent être envoyés et reçus par votre application.  Il doit correspondre exactement à celle de redirect_uris hello que vous inscrit dans le portail hello, à ceci près qu’il doit être codée url.  Pour les applications natives et mobiles, vous devez utiliser la valeur par défaut hello `urn:ietf:wg:oauth:2.0:oob`. |
| response_mode |recommandé |Spécifie la méthode hello qui doit être utilisés toosend hello résultant tooyour précédent jeton application.  Peut être `query` ou `form_post`. |
| state |recommandé |Une valeur incluse dans la demande de hello est également renvoyé dans la réponse du jeton hello. Une valeur unique générée de manière aléatoire est généralement utilisée pour [empêcher les falsifications de requête intersite](http://tools.ietf.org/html/rfc6749#section-10.12).  Hello état est également utilisé tooencode informations hello l’état utilisateur dans une application hello avant de la demande d’authentification hello s’est produite, page de hello ou un affichage qu’ils étaient sur. |
| resource |facultatif |Hello URI ID d’application de hello API web (ressource sécurisée). toofind hello URI ID d’application de hello API web, Bonjour portail Azure, cliquez sur **Active Directory**, cliquez sur le répertoire hello, cliquez sur l’application hello, puis sur **configurer**. |
| prompt |facultatif |Indiquer le type hello d’intervention de l’utilisateur qui est requise.<p> Les valeurs autorisées sont : <p> *connexion*: hello peut être invité à tooreauthenticate. <p> *consentement*: consentement de l’utilisateur a été accordé, mais doit toobe mis à jour. utilisateur de Hello doit être invité à tooconsent. <p> *admin_consent*: un administrateur doit être invité à tooconsent pour le compte de tous les utilisateurs dans leur organisation |
| login_hint |facultatif |Possible champ d’adresse utilisé toopre-remplissage hello nom d’utilisateur et de la messagerie de hello-page de connexion pour l’utilisateur de hello, si vous connaissez le nom d’utilisateur à l’avance.  Applications souvent utilisent ce paramètre lors de la réauthentification, ayant déjà extrait le nom d’utilisateur hello à partir d’une connexion précédente sign-in à l’aide de hello `preferred_username` de revendication. |
| domain_hint |facultatif |Fournit une indication sur le client de hello ou un domaine qui hello utilisateur doit utiliser toosign dans. valeur Hello hello domain_hint est un domaine enregistré pour le client de hello. Si les locataires hello est tooan fédérées des services locaux, AAD redirige serveur de fédération toohello client spécifié. |

> [!NOTE]
> Si l’utilisateur de hello fait partie d’une organisation, un administrateur de l’organisation de hello peut donner son consentement ou refuser au nom d’utilisateur hello ou autoriser hello utilisateur tooconsent. utilisateur de Hello bénéficie hello option tooconsent uniquement lorsque hello administrateur le permet.
>
>

À ce stade, hello utilisateur invité tooenter leurs informations d’identification et le consentement toohello autorisations indiquées dans hello `scope` paramètre de requête. Une fois que l’utilisateur de hello s’authentifie et donne son consentement, Azure AD envoie une application tooyour de réponse à hello `redirect_uri` adresse de votre requête.

### Réponse correcte
Une réponse réussie se présenterait ainsi :

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| Paramètre | Description |
| --- | --- |
| admin_consent |valeur de Hello a la valeur True si un administrateur consenti tooa de consentement de demande. |
| code |code d’autorisation Hello application hello demandée. application Hello peut utiliser toorequest de code d’autorisation hello un jeton d’accès pour la ressource cible de hello. |
| session_state |Une valeur unique qui identifie la session utilisateur en cours hello. Cette valeur est un GUID, mais doit être traitée comme une valeur opaque n’ayant fait l’objet d’aucune analyse. |
| state |Si un paramètre d’état est inclus dans la demande de hello, hello même valeur doit figurer dans la réponse de hello. Il est conseillé de tooverify d’application hello que les valeurs d’état hello dans hello demande et de réponse sont identiques avant à l’aide de la réponse de hello. Cela permet de toodetect [des attaques par falsification de demande d’intersites (CSRF)](https://tools.ietf.org/html/rfc6749#section-10.12) sur le client de hello. |

### Réponse d’erreur
Réponses d’erreur peuvent aussi être envoyés à toohello `redirect_uri` afin que l’application hello peut gérer de façon appropriée.

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Paramètre | Description |
| --- | --- |
| error |Une valeur de code d’erreur définie dans la Section 5.2 de hello [OAuth 2.0 Authorization Framework](http://tools.ietf.org/html/rfc6749). table de Hello suivant décrit les codes d’erreur de hello retournés par Azure AD. |
| error_description |Une description plus détaillée de l’erreur de hello. Ce message n’est pas destiné toobe nom convivial de l’utilisateur final. |
| state |valeur d’état Hello est une valeur non réutilisée générée de façon aléatoire qui est envoyée dans la demande hello et retournée dans les attaques de hello réponse tooprevent requête forgery (CSRF). |

#### Codes d’erreur pour les erreurs de point de terminaison d’autorisation
Hello tableau suivant décrit hello différents codes d’erreur qui peuvent être retournées dans hello `error` paramètre de réponse d’erreur hello.

| Code d'erreur | Description | Action du client |
| --- | --- | --- |
| invalid_request |Erreur de protocole, tel qu’un paramètre obligatoire manquant. |Corrigez et soumettez à nouveau la demande de hello. Il s’agit d’une erreur de développement généralement détectée lors des tests initiaux. |
| unauthorized_client |Hello application cliente n’est pas autorisé à toorequest un code d’autorisation. |Cela se produit généralement lorsque l’application cliente de hello n’est pas inscrit dans Azure AD ou locataire Azure AD de l’utilisateur toohello n’est pas ajoutée. application Hello peut inviter l’utilisateur hello avec des instructions pour installer l’application hello et en l’ajoutant tooAzure AD. |
| access_denied |Le propriétaire de la ressource n’a pas accordé son consentement. |application cliente de Hello peut avertir l’utilisateur de hello il ne peut pas continuer à moins que hello utilisateur y consent. |
| unsupported_response_type |serveur d’autorisation de Hello ne prend pas en charge le type de réponse hello dans la demande de hello. |Corrigez et soumettez à nouveau la demande de hello. Il s’agit d’une erreur de développement généralement détectée lors des tests initiaux. |
| server_error |serveur de Hello a rencontré une erreur inattendue. |Réessayez la demande de hello. Ces erreurs peuvent résulter de conditions temporaires. application cliente de Hello peut expliquer toohello utilisateur que sa réponse est retardée en raison de l’erreur temporaire de tooa. |
| temporarily_unavailable |serveur de Hello est temporairement trop occupé toohandle hello demande. |Réessayez la demande de hello. application cliente de Hello peut expliquer toohello utilisateur que sa réponse est retardée en raison de la condition temporaire de tooa. |
| invalid_resource |ressource de Hello cible n’est pas valide, car il n’existe pas, Azure AD ne peut pas trouver ou il n’est pas configuré correctement. |Cela indique la ressource de hello, s’il en existe n'a pas été configurée dans hello client. application Hello peut inviter l’utilisateur hello avec des instructions pour installer l’application hello et en l’ajoutant tooAzure AD. |

## Utilisez toorequest de code d’autorisation hello un jeton d’accès
Maintenant que vous avez acquis un code d’autorisation et l’autorisation avez été accordée par l’utilisateur de hello, vous pouvez utiliser le code hello pour une ressource de jeton toohello souhaité d’accès, en envoyant un toohello de la demande POST `/token` point de terminaison :

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code
&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA
&redirect_uri=https%3A%2F%2Flocalhost%2Fmyapp%2F
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=p@ssw0rd

//NOTE: client_secret only required for web apps
```

| Paramètre |  | Description |
| --- | --- | --- |
| locataire |required |Hello `{tenant}` valeur de chemin d’accès de hello de demande de hello peut être utilisé toocontrol qui peut se connecter à l’application hello.  Hello valeurs autorisées sont des identificateurs de client, par exemple, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` ou `common` pour les jetons d’indépendant du locataire |
| client_id |required |Hello Id d’Application attribué tooyour application lorsque vous avez l’inscrit auprès d’Azure AD. Vous pouvez le trouver dans hello portail classique Azure. Cliquez sur **Active Directory**, cliquez sur le répertoire hello, choisissez l’application hello et cliquez sur **configurer** |
| grant_type |required |Doit être `authorization_code` pour les flux de code d’autorisation hello. |
| code |required |Hello `authorization_code` que vous avez obtenue dans la section précédente de hello |
| redirect_uri |required |Hello même `redirect_uri` valeur qui a été utilisé tooacquire hello `authorization_code`. |
| client_secret |requis pour les applications Web |secret d’application Hello que vous avez créé dans le portail de l’enregistrement d’application hello pour votre application.  Il ne doit pas être utilisé dans une application native, car les clés secrètes client ne peuvent pas être stockées de manière sûre sur les appareils.  Il est requis pour les applications web et web API, qui ont hello de hello capacité toostore `client_secret` en toute sécurité sur le côté du serveur hello. |
| resource |requis s’il est spécifié dans la demande de code d’autorisation, facultatif dans le cas contraire |Hello URI ID d’application de hello API web (ressource sécurisée). |

toofind hello URI ID d’application Bonjour portail de gestion Azure, cliquez sur **Active Directory**, cliquez sur le répertoire hello, cliquez sur l’application hello, puis cliquez sur **configurer**.

### Réponse correcte
Azure AD renvoie un jeton d’accès dès réception d’une réponse correcte. toominimize des appels de réseau à partir de l’application cliente de hello et leur latence associé, application de client hello doit mettre en cache des jetons d’accès pour hello durée de vie qui est spécifiée dans hello réponse OAuth 2.0. durée de vie jeton toodetermine hello, utilisez soit hello `expires_in` ou `expires_on` les valeurs de paramètre.

Si une ressource de l’API web renvoie un `invalid_token` code d’erreur, cela peut indiquer que les ressources hello a déterminé que le jeton hello a expiré. Si le temps d’horloge hello client et les ressources sont différents (appelé un « décalage horaire »), les ressources hello envisagez toobe de jeton hello a expiré avant que le jeton de hello est effacé du cache du client de hello. Si cela se produit, désactivez le jeton hello à partir du cache hello, même si elle est toujours dans sa durée de vie calculée.

Une réponse réussie se présenterait ainsi :

```
{
  "access_token": " eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| Paramètre | Description |
| --- | --- |
| access_token |jeton d’accès demandé Hello. application Hello peut utiliser cette toohello tooauthenticate jeton ressource, telle qu’une API web sécurisée. |
| token_type |Indique la valeur de jeton de type hello. Hello tapez uniquement que prend en charge d’Azure AD est porteur. Pour plus d’informations sur les jetons du porteur, consultez le document [OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) |
| expires_in |La durée pendant laquelle le jeton d’accès hello est valide (en secondes). |
| expires_on |Hello date d’expiration jeton d’accès hello. date de Hello est représenté en tant que nombre hello de secondes entre 1970-01-01T0:0:0Z UTC jusqu'à ce que le délai d’expiration de hello. Cette valeur est la durée de vie utilisé toodetermine hello de jetons mis en cache. |
| resource |Hello URI ID d’application de hello API web (ressource sécurisée). |
| scope |Application cliente de toohello les autorisations de l’emprunt d’identité accordées. autorisation de Hello par défaut est `user_impersonation`. propriétaire de Hello Hello ressource sécurisée peut enregistrer des valeurs supplémentaires dans Azure AD. |
| refresh_token |Un jeton d’actualisation OAuth 2.0. application Hello peut utiliser ce jeton tooacquire des jetons d’accès supplémentaires après l’expiration du jeton d’accès actuel hello.  Actualiser les jetons sont de longue durées et peut être utilisé tooretain accès tooresources pendant de longues périodes de temps. |
| id_token |Un jeton Web JSON non signé (JWT). Hello application peut base64Url décoder segments hello de ces informations de jeton toorequest sur utilisateur hello connectés. application Hello peut mettre en cache les valeurs hello et les afficher, mais il ne doit pas dépendre les pour toute l’autorisation ou des limites de sécurité. |

### Demandes de jeton JWT
jeton Web JSON de Hello dans la valeur hello hello `id_token` paramètre peut être décodé en hello suivant revendications :

```
{
 "typ": "JWT",
 "alg": "none"
}.
{
 "aud": "2d4d11a2-f814-46a7-890a-274a72a7309e",
 "iss": "https://sts.windows.net/7fe81447-da57-4385-becb-6de57f21477e/",
 "iat": 1388440863,
 "nbf": 1388440863,
 "exp": 1388444763,
 "ver": "1.0",
 "tid": "7fe81447-da57-4385-becb-6de57f21477e",
 "oid": "68389ae2-62fa-4b18-91fe-53dd109d74f5",
 "upn": "frank@contoso.com",
 "unique_name": "frank@contoso.com",
 "sub": "JWvYdCWPhhlpS1Zsf7yYUxShUwtUm5yzPmw_-jX3fHY",
 "family_name": "Miller",
 "given_name": "Frank"
}.
```

Pour plus d’informations sur les jetons web JSON, consultez hello [spécification préliminaire JWT IETF](http://go.microsoft.com/fwlink/?LinkId=392344). Pour plus d’informations sur les types de jetons hello et revendications, consultez [pris en charge du jeton et Types de revendication](active-directory-token-and-claims.md)

Hello `id_token` paramètre inclut hello les types de revendications suivants :

| Type de revendication | Description |
| --- | --- |
| aud |Audience du jeton de hello. Lorsque le jeton de hello est émis application cliente de tooa, hello s’hello `client_id` du client de hello. |
| exp |Heure d’expiration. Hello expiration lorsque hello jeton. Pour toobe de la jeton de hello valide, hello date/heure actuelle doit être inférieur ou égal toohello `exp` valeur. temps de Hello est représenté en hello secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu'à ce que le jeton de hello hello temps a été émis. |
| family_name |Le nom de famille de l’utilisateur. application Hello peut afficher cette valeur. |
| given_name |Le prénom de l’utilisateur. application Hello peut afficher cette valeur. |
| iat |Heure d’émission. heure de Hello lorsque hello JWT a été émis. temps de Hello est représenté en hello secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu'à ce que le jeton de hello hello temps a été émis. |
| iss |Identifie l’émetteur de jeton hello |
| nbf |Pas avant l’heure. heure de Hello lorsque le jeton de hello devient effective. Pour toobe de la jeton de hello valide, hello date/heure actuelle doit être supérieure ou égale toohello Nbf valeur. temps de Hello est représenté en hello secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu'à ce que le jeton de hello hello temps a été émis. |
| oid |Identificateur d’objet (ID) de l’objet d’utilisateur hello dans Azure AD. |
| sub |Identificateur du sujet du jeton. Il s’agit d’un identificateur persistant et immuable pour l’utilisateur de hello hello jeton décrit. Utilisez cette valeur dans la logique de mise en cache. |
| tid |Identificateur (ID) de client hello Azure AD qui a émis le jeton de hello du client. |
| unique_name |Un identificateur unique pour qui peut être affichée toohello utilisateur. Il s’agit généralement d’un nom d’utilisateur principal (UPN, user principal name). |
| upn |Nom d’utilisateur principal de l’utilisateur de hello. |
| ver |Version. version de Hello du jeton Web JSON de hello, généralement 1.0. |

### Réponse d’erreur
erreurs de point de terminaison d’émission de jeton de Hello sont des codes d’erreur HTTP, car les appels du client hello hello le point de terminaison d’émission de jeton directement. En outre code d’état HTTP de toohello, point de terminaison d’émission de jeton de Azure AD hello retourne également un document JSON avec des objets qui décrivent l’erreur de hello.

Une réponse d’erreur se présenterait ainsi :

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: hello provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
}
```
| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être utilisés tooclassify des types d’erreurs qui se produisent et peut être utilisé tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |
| error_codes |Liste des codes d’erreur STS spécifiques pouvant être utiles dans les tests de diagnostic. |
| timestamp |heure de Hello hello erronée. |
| trace_id |Identificateur unique pour la demande hello qui peut aider dans les diagnostics. |
| correlation_id |Identificateur unique pour la demande hello qui peut vous aider à diagnostics entre les composants. |

#### Codes d’état HTTP
Hello tableau suivant répertorie les codes d’état HTTP de hello hello retourne de point de terminaison d’émission de jeton. Dans certains cas, code d’erreur hello est la réponse de hello toodescribe suffisante, mais s’il existe des erreurs, vous devez hello tooparse accompagnant JSON de document et examiner son code d’erreur.

| Code HTTP | Description |
| --- | --- |
| 400 |Code HTTP par défaut. Utilisé dans la plupart des cas et est généralement dû tooa de demande incorrect. Corrigez et soumettez à nouveau la demande de hello. |
| 401 |Échec d’authentification. Par exemple, demande de hello hello client_secret paramètre manquant. |
| 403 |Échec de l’autorisation. Par exemple, utilisateur de hello n’a pas de ressource d’autorisation tooaccess hello. |
| 500 |Une erreur interne s’est produite au niveau de service de hello. Réessayez la demande de hello. |

#### Codes d’erreur pour les erreurs de point de terminaison de jeton
| Code d'erreur | Description | Action du client |
| --- | --- | --- |
| invalid_request |Erreur de protocole, tel qu’un paramètre obligatoire manquant. |Corrigez et soumettez à nouveau la demande de hello |
| invalid_grant |code d’autorisation de Hello n’est pas valide ou a expiré. |Essayez une nouvelle toohello de demande `/authorize` point de terminaison |
| unauthorized_client |Hello client authentifié n’est pas autorisé toouse type d’accorder cette autorisation. |Cela se produit généralement lorsque l’application cliente de hello n’est pas inscrit dans Azure AD ou locataire Azure AD de l’utilisateur toohello n’est pas ajoutée. application Hello peut inviter l’utilisateur hello avec des instructions pour installer l’application hello et en l’ajoutant tooAzure AD. |
| invalid_client |Échec d’authentification du client. |informations d’identification du client Hello ne sont pas valides. toofix, administrateur de l’application hello met à jour les informations d’identification hello. |
| unsupported_grant_type |serveur d’autorisation de Hello ne prend pas en charge le type d’octroi d’autorisation hello. |Hello de modification accorder le type de demande de hello. Ce type d’erreur doit se produire uniquement lors du développement et doit être détecté lors du test initial. |
| invalid_resource |ressource de Hello cible n’est pas valide, car il n’existe pas, Azure AD ne peut pas trouver ou il n’est pas configuré correctement. |Cela indique la ressource de hello, s’il en existe n'a pas été configurée dans hello client. application Hello peut inviter l’utilisateur hello avec des instructions pour installer l’application hello et en l’ajoutant tooAzure AD. |
| interaction_required |demande de Hello nécessite une interaction utilisateur. Par exemple, une étape d’authentification supplémentaire est nécessaire. | Au lieu d’une demande non interactif, réessayez avec une demande d’autorisation interactive pour hello même ressource. |
| temporarily_unavailable |serveur de Hello est temporairement trop occupé toohandle hello demande. |Réessayez la demande de hello. application cliente de Hello peut expliquer toohello utilisateur que sa réponse est retardée en raison de la condition temporaire de tooa. |

## Utilisez hello accès tooaccess jeton hello ressource
Maintenant que vous avez acquis avec succès une `access_token`, vous pouvez utiliser le jeton de hello dans les demandes tooWeb API, en l’incluant dans hello `Authorization` en-tête. Hello [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt) spécification explique comment les ressources protégées dans les jetons de support toouse dans tooaccess des demandes HTTP.

### Exemple de requête
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### Réponse d’erreur
Les ressources sécurisées qui implémentent la spécification RFC 6750 émettent des codes d’état HTTP. Si la demande de hello n’inclut pas les informations d’identification d’authentification ou manque de réponse du jeton, hello de hello inclut un `WWW-Authenticate` en-tête. En cas d’échec d’une demande, serveur de ressources hello répond avec le code d’état HTTP hello et un code d’erreur.

Hello Voici un exemple d’une réponse d’échec lors de la demande du client hello n’inclut pas de jeton de support hello :

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="hello access token is missing.",
```

#### Paramètres d’erreur
| Paramètre | Description |
| --- | --- |
| authorization_uri |Hello URI (point de terminaison physique) du serveur d’autorisation de hello. Cette valeur est également utilisée comme une recherche de clé tooget plus d’informations sur le serveur hello à partir d’un point de terminaison de découverte. <p><p> client de Hello doit valider ce hello serveur d’autorisation est approuvé. Lorsque les ressources hello sont protégé par Azure AD, il est suffisant tooverify hello URL commence par https://login.microsoftonline.com ou un autre nom d’hôte qui prend en charge par Azure AD. Une ressource spécifique au client doit toujours retourner un URI d’autorisation spécifique au client. |
| error |Une valeur de code d’erreur définie dans la Section 5.2 de hello [OAuth 2.0 Authorization Framework](http://tools.ietf.org/html/rfc6749). |
| error_description |Une description plus détaillée de l’erreur de hello. Ce message n’est pas destiné toobe nom convivial de l’utilisateur final. |
| resource_id |Retourne hello identificateur unique de la ressource de hello. application cliente de Hello peut utiliser cet identificateur en tant que valeur hello Hello `resource` paramètre lorsqu’il demande un jeton pour la ressource de hello. <p><p> Il est important pour hello client application tooverify cette valeur, sinon un service malveillant peut être en mesure de tooinduce un **une élévation de privilèges** attaque <p><p> Hello stratégie recommandée pour empêcher une attaque est tooverify hello `resource_id` correspondances hello base du site web hello URL d’API qui en cours d’accès. Par exemple, si https://service.contoso.com/data est accessible, hello `resource_id` peut être htttps://service.contoso.com/. application cliente de Hello doit rejeter une `resource_id` qui ne commence pas par URL de base hello sauf s’il existe un id de hello tooverify autre façon fiable. |

#### Codes d’erreur du schéma de porteur
Hello spécification RFC 6750 définit hello pour les ressources qui utilisent les en-tête WWW-Authenticate de hello et schéma de support dans la réponse de hello, les erreurs suivantes.

| Code d’état HTTP | Code d'erreur | Description | Action du client |
| --- | --- | --- | --- |
| 400 |invalid_request |demande de Hello n’est pas correctement formée. Par exemple, il manque peut-être un paramètre ou à l’aide de hello même paramètre de deux fois. |Corrigez l’erreur de hello et nouvelle tentative de demande de hello. Ce type d’erreur doit se produire uniquement lors du développement et doit être détecté lors du test initial. |
| 401 |invalid_token |jeton d’accès Hello est manquant, incorrect ou est révoqué. valeur Hello du paramètre d’error_description hello fournit des détails supplémentaires. |Demander un nouveau jeton hello serveur d’autorisation. Si le jeton hello échoue, une erreur inattendue s’est produite. Envoyer à un utilisateur de toohello message erreur et recommencez après un délai aléatoire. |
| 403 |insufficient_scope |jeton d’accès Hello ne contient pas de hello d’emprunt d’identité autorisations requis tooaccess hello ressource. |Envoyer un nouveau point de terminaison d’autorisation d’autorisation demande toohello. Si la réponse de hello contient un paramètre d’étendue hello, utilisez la valeur de portée de hello dans la ressource de toohello demande hello. |
| 403 |insufficient_access |objet Hello du jeton de hello n’a pas d’autorisations de hello des ressources hello tooaccess requis. |Hello invite utilisateur toouse un autre compte ou toorequest autorisations toohello la ressource spécifiée. |

## L’actualisation des jetons d’accès hello
Les jetons d’accès sont de courte durées et doivent être actualisés après l’expiration des toocontinue l’accès aux ressources. Vous pouvez actualiser hello `access_token` en envoyant un autre `POST` demande toohello `/token` point de terminaison, mais cette fois en fournissant hello `refresh_token` au lieu de hello `code`.

Les jetons d’actualisation n’ont pas de durée de vie spécifiée. En règle générale, les durées de vie hello des jetons d’actualisation sont relativement longues. Toutefois, dans certains cas, des jetons d’actualisation expirent, sont considérés comme révoqués ou ne disposent pas de privilèges suffisants pour l’action de hello souhaité. Votre application doit tooexpect et gérer les erreurs retournées par point de terminaison d’émission de jeton hello correctement.

Lorsque vous recevez une réponse avec une erreur de jeton d’actualisation, ignorez hello actuel jeton d’actualisation et demandez un nouveau code d’autorisation ou jeton d’accès. En particulier, lorsque à l’aide d’une actualisation de jeton Bonjour flux d’octroi de Code d’autorisation, si vous recevez une réponse avec hello `interaction_required` ou `invalid_grant` codes d’erreur, ignorer le jeton d’actualisation hello et demandez un nouveau code d’autorisation.

Un toohello de demande d’exemple **spécifiques du client** point de terminaison (vous pouvez également utiliser hello **commune** point de terminaison) tooget un nouveau jeton d’accès à l’aide d’un jeton d’actualisation ressemble à ceci :

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

### Réponse correcte
Une réponse de jeton réussie se présente ainsi :

```
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1460404526",
  "resource": "https://service.contoso.com/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "refresh_token": "AwABAAAAv YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl PM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfmVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA"
}
```
| Paramètre | Description |
| --- | --- |
| token_type |type de jeton Hello. la valeur Hello uniquement pris en charge est **support**. |
| expires_in |Hello restant de durée de vie du jeton de hello en secondes. 3600 (une heure) est une valeur courante. |
| expires_on |date de Hello et l’heure à laquelle le jeton de hello expire. date de Hello est représenté en tant que nombre hello de secondes entre 1970-01-01T0:0:0Z UTC jusqu'à ce que le délai d’expiration de hello. |
| resource |Identifie hello ressource sécurisée ce jeton d’accès hello peut être utilisé tooaccess. |
| scope |Application cliente native de toohello les autorisations de l’emprunt d’identité accordées. autorisation de Hello par défaut est **user_impersonation**. propriétaire de Hello de ressource de hello cible peut enregistrer des valeurs alternatives dans Azure AD. |
| access_token |Hello nouveau jeton d’accès qui a été demandée. |
| refresh_token |Un nouveau refresh_token OAuth 2.0 qui peuvent être utilisés toorequest nouveaux jetons d’accès quand un hello dans cette réponse expire. |

### Réponse d’erreur
Une réponse d’erreur se présenterait ainsi :

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: hello application named https://foo.microsoft.com/mail.read was not found in hello tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.  You might have sent your authentication request toohello wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
}
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être utilisés tooclassify des types d’erreurs qui se produisent et peut être utilisé tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |
| error_codes |Liste des codes d’erreur STS spécifiques pouvant être utiles dans les tests de diagnostic. |
| timestamp |heure de Hello hello erronée. |
| trace_id |Identificateur unique pour la demande hello qui peut aider dans les diagnostics. |
| correlation_id |Identificateur unique pour la demande hello qui peut vous aider à diagnostics entre les composants. |

Pour obtenir une description des codes d’erreur hello et hello client action recommandée, consultez [codes d’erreur pour les erreurs de point de terminaison de jeton](#error-codes-for-token-endpoint-errors).
