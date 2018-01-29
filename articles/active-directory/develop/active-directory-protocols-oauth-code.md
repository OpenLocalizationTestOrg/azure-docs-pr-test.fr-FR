---
title: "Comprendre le flux du code d’autorisation OAuth 2.0 dans Azure AD"
description: "Cet article explique comment utiliser des messages HTTP pour autoriser l’accès aux applications web et API web dans votre client à l’aide d’Azure Active Directory et OAuth 2.0."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mtillman
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 77df32710f17f8c5b749c39af9f6c64f0cc0b376
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/09/2018
---
# <a name="authorize-access-to-web-applications-using-oauth-20-and-azure-active-directory"></a>Autoriser l’accès aux applications web à l’aide d’OAuth 2.0 et Azure Active Directory
Azure Active Directory (Azure AD) utilise OAuth 2.0 pour vous permettre d’autoriser l’accès aux applications web et aux API web dans votre client Azure AD. Ce guide est indépendant du langage. Il explique comment envoyer et recevoir des messages HTTP sans utiliser l’une de nos bibliothèques open source.

Le flux de code d’autorisation OAuth 2.0 est décrit dans la [section 4.1 des spécifications OAuth 2.0](https://tools.ietf.org/html/rfc6749#section-4.1). Il est utilisé pour exécuter des activités d’authentification et d’autorisation dans la majorité des types d’applications, notamment les applications web et les applications installées de façon native.

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## <a name="oauth-20-authorization-flow"></a>Flux d’autorisation OAuth 2.0
À un niveau élevé, le flux d’autorisation complet pour une application est semblable à l’illustration suivante :

![Flux de code d’authentification OAuth](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## <a name="request-an-authorization-code"></a>Demander un code d’autorisation
Le flux de code d'autorisation commence par le client dirigeant l'utilisateur vers le point de terminaison `/authorize` . Dans cette requête, le client indique les autorisations qu’il doit obtenir auprès de l’utilisateur : Vous pouvez obtenir le point de terminaison OAuth 2.0 pour votre client en sélectionnant **Inscriptions d’applications > Points de terminaison** dans le portail Azure.

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

| Paramètre |  | DESCRIPTION |
| --- | --- | --- |
| locataire |required |La valeur `{tenant}` dans le chemin d’accès de la requête peut être utilisée pour contrôler les utilisateurs qui peuvent se connecter à l’application.  Les valeurs autorisées sont les identificateurs du client, par exemple `8eaef023-2b34-4da1-9baa-8bc8c9d6a490`, `contoso.onmicrosoft.com` ou `common` pour les jetons indépendants du client |
| client_id |required |L’ID d’application attribué à votre application lorsque vous l’avez inscrite auprès d’Azure AD. Vous le trouverez sur le portail Azure. Cliquez sur **Active Directory**, sur le répertoire, sélectionnez l’application et cliquez sur **Configurer** |
| response_type |required |Doit inclure `code` pour le flux de code d’autorisation. |
| redirect_uri |recommandé |L’URI de redirection de votre application, vers lequel votre application peut envoyer et recevoir des réponses d’authentification.  Il doit correspondre exactement à l’un des URI de redirection enregistrés dans le portail, auquel s’ajoute le codage dans une URL.  Pour les applications natives et mobiles, vous devez utiliser la valeur par défaut `urn:ietf:wg:oauth:2.0:oob`. |
| response_mode |recommandé |Spécifie la méthode à utiliser pour envoyer le jeton résultant à votre application.  Peut être `query` ou `form_post`. |
| state |recommandé |Une valeur incluse dans la requête qui est également renvoyée dans la réponse de jeton. Une valeur unique générée de manière aléatoire est généralement utilisée pour [empêcher les falsifications de requête intersite](http://tools.ietf.org/html/rfc6749#section-10.12).  La valeur d’état est également utilisée pour coder les informations sur l’état de l’utilisateur dans l’application avant la requête d’authentification, comme la page ou l’écran sur lequel ou laquelle il était positionné. |
| resource |facultatif |URI ID d’application de l’API web (ressource sécurisée). Pour rechercher l’URI ID d’application de l’API web, dans le portail Azure, cliquez successivement sur **Active Directory**, le répertoire, l’application et sur **Configurer**. |
| prompt |facultatif |Indique le type d’interaction utilisateur requis.<p> Les valeurs autorisées sont : <p> *login*: l’utilisateur doit être invité à se réauthentifier. <p> *consent*: le consentement de l’utilisateur a été accordé, mais il doit être mis à jour. L’utilisateur doit être invité à donner son consentement. <p> *admin_consent* : un administrateur doit être invité à donner son consentement pour le compte de tous les utilisateurs de son organisation |
| login_hint |facultatif |Peut être utilisé pour remplir au préalable le champ réservé au nom d’utilisateur/à l’adresse électronique de la page de connexion de l’utilisateur si vous connaissez déjà son nom d’utilisateur.  Les applications utilisent souvent ce paramètre au cours de la réauthentification, après avoir extrait le nom d’utilisateur d’une connexion précédente à l’aide de la revendication `preferred_username`. |
| domain_hint |facultatif |Fournit une indication sur le client ou le domaine que l’utilisateur doit utiliser pour se connecter. La valeur du paramètre domain_hint est un domaine inscrit pour le client. Si le client est fédéré sur un répertoire local, AAD redirige vers le serveur de fédération du client spécifié. |

> [!NOTE]
> Si l’utilisateur fait partie d’une organisation, un administrateur de l’organisation peut donner son consentement ou refuser pour le compte de l’utilisateur, ou autoriser l’utilisateur à donner son consentement. L’utilisateur a la possibilité de donner son consentement uniquement lorsque l’administrateur le lui permet.
>
>

À ce stade, l’utilisateur est invité à entrer ses informations d’identification et à donner son consentement vis-à-vis des autorisations indiquées dans le paramètre de requête `scope`. Une fois que l’utilisateur s’authentifie et donne son consentement, Azure AD envoie une réponse à votre application à l’adresse `redirect_uri` dans votre demande.

### <a name="successful-response"></a>Réponse correcte
Une réponse réussie se présenterait ainsi :

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| Paramètre | DESCRIPTION |
| --- | --- |
| admin_consent |La valeur est True si un administrateur a donné son consentement lorsqu’il y a été invité. |
| code |Le code d’autorisation demandé par l’application. L’application peut utiliser ce code d’autorisation pour demander un jeton d’accès pour la ressource cible. |
| session_state |Une valeur unique identifiant la session utilisateur actuelle. Cette valeur est un GUID, mais doit être traitée comme une valeur opaque n’ayant fait l’objet d’aucune analyse. |
| state |Si un paramètre d’état est inclus dans la demande, la même valeur doit apparaître dans la réponse. Avant d’utiliser la réponse, il est recommandé que l’application vérifie que les valeurs d’état de la demande et de la réponse sont identiques. Cela permet de détecter les [attaques par falsification de requête intersites (CSRF, Cross Site Request Forgery)](https://tools.ietf.org/html/rfc6749#section-10.12) menaçant le client. |

### <a name="error-response"></a>Réponse d’erreur
Les réponses d’erreur peuvent également être envoyées à l’élément `redirect_uri` , de manière à ce que l’application puisse les traiter de manière appropriée.

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Paramètre | DESCRIPTION |
| --- | --- |
| error |Une valeur de code d’erreur définie dans la section 5.2 du document [OAuth 2.0 Authorization Framework](http://tools.ietf.org/html/rfc6749)(Infrastructure d’autorisation OAuth 2.0). Le tableau suivant décrit les codes d’erreur retournés par Azure AD. |
| error_description |Une description plus détaillée de l’erreur. Ce message n’est pas destiné à offrir une description claire à l’utilisateur final. |
| state |La valeur d’état est une valeur non réutilisée, générée de manière aléatoire, envoyée dans la demande et retournée dans la réponse pour empêcher les falsifications de requête intersites (CSRF, Cross Site Request Forgery). |

#### <a name="error-codes-for-authorization-endpoint-errors"></a>Codes d’erreur pour les erreurs de point de terminaison d’autorisation
Le tableau suivant décrit les différents codes d’erreur qui peuvent être retournés dans le paramètre `error` de la réponse d’erreur.

| Code d'erreur | DESCRIPTION | Action du client |
| --- | --- | --- |
| invalid_request |Erreur de protocole, tel qu’un paramètre obligatoire manquant. |Corrigez l’erreur, puis envoyez à nouveau la demande. Il s’agit d’une erreur de développement généralement détectée lors des tests initiaux. |
| unauthorized_client |L’application cliente n’est pas autorisée à demander un code d’autorisation. |Cela se produit généralement lorsque l’application cliente n’est pas inscrite dans Azure AD ou n’est pas ajoutée au client Azure AD de l’utilisateur. L’application peut proposer à l’utilisateur des instructions pour installer l’application et l’ajouter à Azure AD. |
| access_denied |Le propriétaire de la ressource n’a pas accordé son consentement. |L’application cliente peut avertir l’utilisateur qu’elle ne peut pas continuer sans son consentement. |
| unsupported_response_type |Le serveur d’autorisation ne prend pas en charge le type de réponse dans la demande. |Corrigez l’erreur, puis envoyez à nouveau la demande. Il s’agit d’une erreur de développement généralement détectée lors des tests initiaux. |
| server_error |Le serveur a rencontré une erreur inattendue. |relancez la requête. Ces erreurs peuvent résulter de conditions temporaires. L’application cliente peut expliquer à l’utilisateur que sa réponse est reportée en raison d’une erreur temporaire. |
| temporarily_unavailable |Le serveur est temporairement trop occupé pour traiter la demande. |relancez la requête. L’application cliente peut expliquer à l’utilisateur que sa réponse est reportée en raison d’une condition temporaire. |
| invalid_resource |La ressource cible n’est pas valide car elle n’existe pas, Azure AD ne la trouve pas ou elle n’est pas configurée correctement. |Cela indique que la ressource, si elle existe, n’a pas été configurée dans le client. L’application peut proposer à l’utilisateur des instructions pour installer l’application et l’ajouter à Azure AD. |

## <a name="use-the-authorization-code-to-request-an-access-token"></a>Utiliser le code d’autorisation pour demander un jeton d’accès
Maintenant que vous avez acquis un code d’autorisation et que l’utilisateur vous a octroyé une autorisation, vous pouvez échanger le code contre un jeton d’accès à la ressource souhaitée, en envoyant une demande POST au point de terminaison `/token` :

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

| Paramètre |  | DESCRIPTION |
| --- | --- | --- |
| locataire |required |La valeur `{tenant}` dans le chemin d’accès de la requête peut être utilisée pour contrôler les utilisateurs qui peuvent se connecter à l’application.  Les valeurs autorisées sont les identificateurs du client, par exemple `8eaef023-2b34-4da1-9baa-8bc8c9d6a490`, `contoso.onmicrosoft.com` ou `common` pour les jetons indépendants du client |
| client_id |required |L’ID d’application attribué à votre application lorsque vous l’avez inscrite auprès d’Azure AD. Vous le trouverez sur le portail Azure. L’ID d’application s’affiche dans les paramètres de l’inscription de l’application.  |
| grant_type |required |Doit être `authorization_code` pour le flux de code d'autorisation. |
| code |required |`authorization_code` que vous avez obtenu dans la section précédente. |
| redirect_uri |required |Valeur `redirect_uri` qui a été utilisée pour acquérir le `authorization_code`. |
| client_secret |requis pour les applications Web |Le secret d’application que vous avez créé dans le portail d’inscription des applications pour votre application.  Il ne doit pas être utilisé dans une application native, car les clés secrètes client ne peuvent pas être stockées de manière sûre sur les appareils.  Il est requis pour les applications web et les API web, qui peuvent stocker en toute sécurité le `client_secret` sur le côté serveur. |
| resource |requis s’il est spécifié dans la demande de code d’autorisation, facultatif dans le cas contraire |URI ID d’application de l’API web (ressource sécurisée). |

Pour rechercher l’URI ID d’application, dans le portail de gestion Azure, cliquez successivement sur **Active Directory**, le répertoire, l’application, puis sur **Configurer**.

### <a name="successful-response"></a>Réponse correcte
Azure AD renvoie un jeton d’accès dès réception d’une réponse correcte. Pour réduire le nombre d’appels réseau de l’application cliente et la latence associée, l’application cliente doit mettre en cache des jetons d’accès tout au long de la durée de vie des jetons, spécifiée dans la réponse OAuth 2.0. Pour déterminer la durée de vie des jetons, utilisez les valeurs de paramètre `expires_in` ou `expires_on`.

Si une ressource de l’API web renvoie un code d’erreur `invalid_token` , cela peut indiquer que la ressource a déterminé que le jeton est arrivé à expiration. Si les temps horloge du client et de la ressource sont différents (on parle alors de « différence de temps »), la ressource peut considérer que le jeton a expiré avant que celui-ci n’ait été effacé du cache du client. Si cela se produit, effacez le jeton du cache, même si sa durée de vie calculée n’a pas expiré.

Une réponse réussie se présenterait ainsi :

```
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| Paramètre | DESCRIPTION |
| --- | --- |
| access_token |Le jeton d’accès demandé sous forme de JSON Web Token (JWT) signé. L’application peut utiliser ce jeton pour procéder à l’authentification sur la ressource sécurisée, comme une API Web. |
| token_type |Indique la valeur du type de jeton. Le seul type de jeton pris en charge par Azure AD est le jeton porteur. Pour plus d’informations sur les jetons du porteur, consultez le document [OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) |
| expires_in |La durée de validité (en secondes) du jeton d’accès. |
| expires_on |L’heure d’expiration du jeton d’accès. La date est représentée en nombre de secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu’au moment de l’expiration. Cette valeur est utilisée pour déterminer la durée de vie des jetons en cache. |
| resource |URI ID d’application de l’API web (ressource sécurisée). |
| scope |Autorisations d’emprunt d’identité accordées à l’application cliente. L’autorisation par défaut est `user_impersonation`. Le propriétaire de la ressource sécurisée peut enregistrer des valeurs supplémentaires dans Azure AD. |
| refresh_token |Un jeton d’actualisation OAuth 2.0. L’application peut utiliser ce jeton pour acquérir des jetons d’accès supplémentaires après l’expiration du jeton d’accès actuel.  Les jetons d’actualisation sont durables, et peuvent être utilisés pour conserver l’accès aux ressources pendant des périodes prolongées. |
| id_token |Un jeton Web JSON non signé (JWT). L’application peut décoder les segments de ce jeton à l’aide d’un décodeur base64Url afin de demander des informations relatives à l’utilisateur qui s’est connecté. L’application peut mettre en cache les valeurs et les afficher, mais ne peut aucunement les utiliser pour les limites d’autorisation ou de sécurité. |

### <a name="jwt-token-claims"></a>Demandes de jeton JWT
Le jeton JWT dans la valeur du paramètre `id_token` peut être décodé dans les revendications suivantes :

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

Pour plus d’informations sur les jetons web JSON, consultez le [projet de spécification JWT de l’IETF](http://go.microsoft.com/fwlink/?LinkId=392344). Pour plus d’informations sur les types de jeton et les revendications, consultez la page [Types de jeton et de revendication pris en charge](active-directory-token-and-claims.md)

Le paramètre `id_token` inclut les types de revendication suivants :

| Type de revendication | DESCRIPTION |
| --- | --- |
| aud |Audience du jeton. Lorsque le jeton est émis pour une application cliente, l’audience est le `client_id` du client. |
| exp |Heure d’expiration. L’heure d’expiration du jeton. Pour que le jeton soit valide, la date et l’heure actuelles doivent être antérieures ou identiques à la valeur `exp` . L’heure est représentée en nombre de secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu’à l’expiration du jeton.|
| family_name |Le nom de famille de l’utilisateur. L’application peut afficher cette valeur. |
| given_name |Le prénom de l’utilisateur. L’application peut afficher cette valeur. |
| iat |Heure d’émission. L’heure d’émission du jeton JWT. L’heure est représentée en nombre de secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu’au moment de l’émission du jeton. |
| iss |Identifie l’émetteur du jeton. |
| nbf |Pas avant l’heure. Heure à laquelle le jeton entre en vigueur. Pour que le jeton soit valide, la date et l’heure actuelles doivent être postérieures ou identiques à la valeur Nbf. L’heure est représentée en nombre de secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu’au moment de l’émission du jeton. |
| oid |Identificateur (ID) de l’objet utilisateur dans Azure AD. |
| sub |Identificateur du sujet du jeton. Il s’agit d’un identificateur persistant et immuable de l’utilisateur décrit par le jeton. Utilisez cette valeur dans la logique de mise en cache. |
| tid |Identificateur (ID) du client Azure AD qui a émis le jeton. |
| unique_name |Identificateur unique pouvant être affiché pour l’utilisateur. Il s’agit généralement d’un nom d’utilisateur principal (UPN, user principal name). |
| upn |Nom d’utilisateur principal. |
| ver |Version. La version du jeton JWT, généralement 1.0. |

### <a name="error-response"></a>Réponse d’erreur
Les erreurs de point de terminaison d’émission de jeton sont des codes d’erreur HTTP, étant donné que le client appelle directement le point de terminaison d’émission de jeton. Outre le code d’état HTTP, le point de terminaison d’émission de jeton Azure AD retourne également un document JSON avec des objets qui décrivent l’erreur.

Une réponse d’erreur se présenterait ainsi :

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: The provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
}
```
| Paramètre | DESCRIPTION |
| --- | --- |
| error |Une chaîne de code d’erreur pouvant être utilisée pour classer les types d’erreur se produisant, et pouvant être utilisée pour intervenir face aux erreurs. |
| error_description |Un message d’erreur spécifique qui peut aider un développeur à identifier la cause principale d’une erreur d’authentification. |
| error_codes |Liste des codes d’erreur STS spécifiques pouvant être utiles dans les tests de diagnostic. |
| timestamp |Heure à laquelle l’erreur s’est produite. |
| trace_id |Identifiant unique de la demande pouvant être utile dans les tests de diagnostic. |
| correlation_id |Identifiant unique de la demande pouvant être utile dans les tests de diagnostic sur les divers composants. |

#### <a name="http-status-codes"></a>Codes d’état HTTP
Le tableau suivant répertorie les codes d’état HTTP retournés par le point de terminaison d’émission de jeton. Dans certains cas, le code d’erreur est suffisant pour décrire la réponse, mais en cas d’erreurs, vous devez analyser le document JSON joint et examiner son code d’erreur.

| Code HTTP | DESCRIPTION |
| --- | --- |
| 400 |Code HTTP par défaut. Il est utilisé dans la plupart des cas et est généralement dû à une demande incorrecte. Corrigez l’erreur, puis envoyez à nouveau la demande. |
| 401 |Échec d’authentification. Par exemple, la demande ne contient pas le paramètre client_secret. |
| 403 |Échec de l’autorisation. Par exemple, l’utilisateur n’est pas autorisé à accéder à la ressource. |
| 500 |Une erreur interne s’est produite au niveau du service. relancez la requête. |

#### <a name="error-codes-for-token-endpoint-errors"></a>Codes d’erreur pour les erreurs de point de terminaison de jeton
| Code d'erreur | DESCRIPTION | Action du client |
| --- | --- | --- |
| invalid_request |Erreur de protocole, tel qu’un paramètre obligatoire manquant. |Corrigez l’erreur, puis envoyez à nouveau la demande. |
| invalid_grant |Le code d’autorisation n’est pas valide ou a expiré. |Essayez une nouvelle demande sur le point de terminaison `/authorize` |
| unauthorized_client |Le client authentifié n’est pas autorisé à utiliser ce type d’octroi d’autorisation. |Cela se produit généralement lorsque l’application cliente n’est pas inscrite dans Azure AD ou n’est pas ajoutée au client Azure AD de l’utilisateur. L’application peut proposer à l’utilisateur des instructions pour installer l’application et l’ajouter à Azure AD. |
| invalid_client |Échec d’authentification du client. |Les informations d’identification du client ne sont pas valides. Pour résoudre le problème, l’administrateur de l’application met à jour les informations d’identification. |
| unsupported_grant_type |Le serveur d’autorisation ne prend pas en charge le type d’octroi d’autorisation. |Modifiez le type d’octroi dans la demande. Ce type d’erreur doit se produire uniquement lors du développement et doit être détecté lors du test initial. |
| invalid_resource |La ressource cible n’est pas valide car elle n’existe pas, Azure AD ne la trouve pas ou elle n’est pas configurée correctement. |Cela indique que la ressource, si elle existe, n’a pas été configurée dans le client. L’application peut proposer à l’utilisateur des instructions pour installer l’application et l’ajouter à Azure AD. |
| interaction_required |La demande nécessite une interaction utilisateur. Par exemple, une étape d’authentification supplémentaire est nécessaire. | Au lieu d’une demande non interactive, réessayez avec une demande d’autorisation interactive pour la même ressource. |
| temporarily_unavailable |Le serveur est temporairement trop occupé pour traiter la demande. |relancez la requête. L’application cliente peut expliquer à l’utilisateur que sa réponse est reportée en raison d’une condition temporaire. |

## <a name="use-the-access-token-to-access-the-resource"></a>Utiliser le jeton d’accès pour accéder à la ressource
Maintenant que vous avez acquis un jeton `access_token`, vous pouvez l'utiliser dans des requêtes dirigées vers des API Web en l'incluant dans l'en-tête `Authorization`. La spécification [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt) explique comment utiliser des jetons du porteur dans les requêtes HTTP pour accéder aux ressources protégées.

### <a name="sample-request"></a>Exemple de requête
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### <a name="error-response"></a>Réponse d’erreur
Les ressources sécurisées qui implémentent la spécification RFC 6750 émettent des codes d’état HTTP. Si la demande n’inclut pas d’informations d’authentification ou ne contient pas le jeton, la réponse inclut un en-tête `WWW-Authenticate` . Lorsqu’une requête échoue, le serveur de ressources répond avec un code d’état HTTP et un code d’erreur.

Voici un exemple de réponse qui échoue lorsque la demande du client n’inclut pas le jeton du porteur :

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="The access token is missing.",
```

#### <a name="error-parameters"></a>Paramètres d’erreur
| Paramètre | DESCRIPTION |
| --- | --- |
| authorization_uri |L’URI (point de terminaison physique) du serveur d’autorisation. Cette valeur est également utilisée comme clé de recherche pour obtenir plus d’informations sur le serveur à partir d’un point de terminaison de détection. <p><p> Le client doit valider l’approbation du serveur d’autorisation. Quand la ressource est protégée par Azure AD, il suffit de vérifier que l’URL commence par https://login.microsoftonline.com ou un autre nom d’hôte pris en charge par Azure AD. Une ressource spécifique au client doit toujours retourner un URI d’autorisation spécifique au client. |
| error |Une valeur de code d’erreur définie dans la section 5.2 du document [OAuth 2.0 Authorization Framework](http://tools.ietf.org/html/rfc6749)(Infrastructure d’autorisation OAuth 2.0). |
| error_description |Une description plus détaillée de l’erreur. Ce message n’est pas destiné à offrir une description claire à l’utilisateur final. |
| resource_id |Retourne l’identificateur unique de la ressource. L’application cliente peut utiliser cet identificateur en tant que valeur du paramètre `resource` lorsqu’elle demande un jeton pour la ressource. <p><p> Il est important pour l’application cliente de vérifier cette valeur. Sinon, un service malveillant peut être en mesure de provoquer une attaque **par élévation de privilèges** <p><p> La stratégie recommandée pour empêcher une attaque consiste à vérifier que le paramètre `resource_id` correspond à la base de l’URL de l’API web faisant l’objet de l’accès. Par exemple, si https://service.contoso.com/data fait l’objet d’un accès, `resource_id` peut être htttps://service.contoso.com/. L’application cliente doit rejeter un `resource_id` qui ne commence pas par l’URL de base sauf s’il existe une autre façon fiable de vérifier l’ID. |

#### <a name="bearer-scheme-error-codes"></a>Codes d’erreur du schéma de porteur
La spécification RFC 6750 définit les erreurs suivantes pour les ressources qui utilisent l’en-tête WWW-Authenticate et le schéma de porteur dans la réponse.

| Code d’état HTTP | Code d'erreur | DESCRIPTION | Action du client |
| --- | --- | --- | --- |
| 400 |invalid_request |La demande n’est pas correcte. Par exemple, un paramètre est manquant ou elle utilise deux fois le même paramètre. |Corrigez l’erreur et relancez la demande. Ce type d’erreur doit se produire uniquement lors du développement et doit être détecté lors du test initial. |
| 401 |invalid_token |Le jeton d’accès est manquant, non valide ou révoqué. La valeur du paramètre error_description fournit des détails supplémentaires. |Demandez un nouveau jeton auprès du serveur d’autorisation. Si le nouveau jeton échoue, une erreur inattendue s’est produite. Envoyez un message d’erreur à l’utilisateur et effectuez une nouvelle tentative après un délai aléatoire. |
| 403 |insufficient_scope |Le jeton d’accès ne contient pas les autorisations d’emprunt d’identité requises pour accéder à la ressource. |Envoyez une nouvelle demande d’autorisation au point de terminaison d’autorisation. Si la réponse contient le paramètre d’étendue, utilisez la valeur d’étendue dans la demande à la ressource. |
| 403 |insufficient_access |Le sujet du jeton n’a pas les autorisations requises pour accéder à la ressource. |Invitez l’utilisateur à utiliser un compte différent ou à demander des autorisations pour la ressource spécifiée. |

## <a name="refreshing-the-access-tokens"></a>Actualisation des jetons d’accès
Les jetons d’accès présentent une durée de vie courte. Après leur expiration, vous devez les actualiser afin de pouvoir continuer à accéder aux ressources. Pour actualiser le `access_token`, envoyez une nouvelle requête `POST` au point de terminaison `/token` en fournissant l’élément `refresh_token` au lieu de l’élément `code`.

Les jetons d’actualisation n’ont pas de durée de vie spécifiée. En règle générale, leur durée de vie est relativement longue. Toutefois, dans certains cas, les jetons d’actualisation expirent, sont révoqués ou ne disposent pas de privilèges suffisants pour l’action souhaitée. Votre application doit envisager et gérer correctement les erreurs retournées par le point de terminaison d’émission de jeton.

Lorsque vous recevez une réponse avec une erreur de jeton d’actualisation, ignorez le jeton d’actualisation actuel et demandez un nouveau code d’autorisation ou un nouveau jeton d’accès. C’est particulièrement le cas lorsque vous utilisez un jeton d’actualisation dans le flux d’octroi de code d’autorisation : si vous recevez une réponse avec le code d’erreur `interaction_required` ou `invalid_grant`, ignorez le jeton d’actualisation et demandez un nouveau code d’autorisation.

Voici un exemple de demande au point de terminaison **propre au client** (vous pouvez également utiliser le point de terminaison **commun**) pour obtenir un nouveau jeton d’accès à l’aide d’un jeton d’actualisation :

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

### <a name="successful-response"></a>Réponse correcte
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
| Paramètre | DESCRIPTION |
| --- | --- |
| token_type |Le type de jeton. La seule valeur prise en charge est **bearer**. |
| expires_in |La durée de vie restante du jeton en secondes. 3600 (une heure) est une valeur courante. |
| expires_on |La date et l’heure auxquelles le jeton expire. La date est représentée en nombre de secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu’au moment de l’expiration. |
| resource |Identifie la ressource sécurisée accessible à l’aide du jeton d’accès. |
| scope |Autorisations d’emprunt d’identité accordées à l’application cliente native. L’autorisation par défaut est **user_impersonation**. Le propriétaire de la ressource cible peut enregistrer des valeurs alternatives dans Azure AD. |
| access_token |Le nouveau jeton d’accès qui a été demandé. |
| refresh_token |Un nouveau jeton d’actualisation OAuth 2.0 pouvant être utilisé pour demander de nouveaux jetons d’accès lorsque celui de cette réponse expire. |

### <a name="error-response"></a>Réponse d’erreur
Une réponse d’erreur se présenterait ainsi :

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: The application named https://foo.microsoft.com/mail.read was not found in the tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if the application has not been installed by the administrator of the tenant or consented to by any user in the tenant.  You might have sent your authentication request to the wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
}
```

| Paramètre | DESCRIPTION |
| --- | --- |
| error |Une chaîne de code d’erreur pouvant être utilisée pour classer les types d’erreur se produisant, et pouvant être utilisée pour intervenir face aux erreurs. |
| error_description |Un message d’erreur spécifique qui peut aider un développeur à identifier la cause principale d’une erreur d’authentification. |
| error_codes |Liste des codes d’erreur STS spécifiques pouvant être utiles dans les tests de diagnostic. |
| timestamp |Heure à laquelle l’erreur s’est produite. |
| trace_id |Identifiant unique de la demande pouvant être utile dans les tests de diagnostic. |
| correlation_id |Identifiant unique de la demande pouvant être utile dans les tests de diagnostic sur les divers composants. |

Pour obtenir une description des codes d’erreur et connaître l’action client recommandée, consultez [Codes d’erreur pour les erreurs de point de terminaison de jeton](#error-codes-for-token-endpoint-errors).
