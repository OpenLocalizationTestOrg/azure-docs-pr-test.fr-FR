---
title: "authentification de tooservice service aaaAzure AD à l’aide d’OAuth2.0 spécification préliminaire de la part de | Documents Microsoft"
description: "Cet article décrit comment la toouse HTTP messages tooimplement service tooservice d’authentification à l’aide de hello OAuth2.0 sur la part de flux."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 55b7fcfe6c0223bddedd8d8fa2defcb5769b43c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Service tooservice appelle à l’aide d’identité de l’utilisateur délégué Bonjour de la part de flux
Hello les flux OAuth 2.0 On-Behalf-Of fait Office de cas d’usage hello où une application appelle un service/API web, qui à son tour doit toocall une autre service web API. Hello est toopropagate hello déléguée l’identité des utilisateurs et des autorisations via la chaîne de demande hello. Pour hello service de couche intermédiaire toomake authentifié demandes toohello service en aval, elle doit toosecure un jeton d’accès d’Azure Active Directory (Azure AD), pour le compte d’utilisateur de hello.

## Diagramme du flux Pour le compte de
Supposons que l’utilisateur hello a été authentifié sur une application à l’aide de hello [flux d’octroi de code d’autorisation OAuth 2.0](active-directory-protocols-oauth-code.md). À ce stade, application hello possède un jeton d’accès (jeton A) avec les revendications de l’utilisateur hello et web de niveau intermédiaire hello consentement tooaccess API (API A). Désormais, les API A doit toomake une API web en aval du toohello demande authentifiée (API B).

les étapes de Hello qui suivent constituent hello sur à la place de flux et sont décrites à l’aide de hello de hello suivant schéma.

![Flux Pour le compte de OAuth 2.0](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. application du client Hello effectue une demande de tooAPI avec A. jeton de hello
2. API A authentifie le point de terminaison d’émission de jeton de Azure AD toohello et demande un jeton tooaccess API B.
3. point de terminaison d’émission de jeton de Azure AD Hello valide les informations d’identification de l’API A avec un jeton et problèmes hello le jeton d’accès pour l’API B (jeton B).
4. le jeton Hello B est défini dans l’en-tête d’autorisation de hello de hello demande tooAPI B.
5. Données à partir de la ressource sécurisée de hello sont retournées par les API B.

## Inscrire une application hello et le service dans Azure AD
Inscrire une application cliente de hello et service de niveau intermédiaire hello dans Azure AD.
### Inscrire le service de couche intermédiaire hello
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte et sous hello **répertoire** , sélectionnez le client Active Directory de hello où vous souhaitez tooregister votre application.
3. Cliquez sur **plus Services** dans hello de navigation de gauche, puis choisissez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications** et choisissez **Nouvelle inscription d’application**.
5. Entrez un nom convivial pour l’application hello et sélectionnez le type d’application hello. Selon le type d’application hello ensemble hello URL de connexion ou les URL de l’URL de redirection toohello base. Cliquez sur **créer** application hello de toocreate.
6. Tout en Bonjour portail Azure, choisissez votre application, puis cliquez sur **paramètres**. Hello paramètres choisissez **clés** et ajouter une clé - sélectionner une durée de clé de 1 an ou 2 ans. Quand vous enregistrez cette page, valeur de clé hello s’affichera, copier et enregistrer la valeur de hello dans un emplacement sûr, vous aurez besoin cette clé ultérieure tooconfigure hello paramètres de l’application dans votre implémentation - cette valeur de clé pas sera à nouveau affichées ni récupérables par les Autrement, veuillez enregistrement il dès qu’il est visible à partir de hello portail Azure.

### Inscrire l’application cliente de hello
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte et sous hello **répertoire** , sélectionnez le client Active Directory de hello où vous souhaitez tooregister votre application.
3. Cliquez sur **plus Services** dans hello de navigation de gauche, puis choisissez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications** et choisissez **Nouvelle inscription d’application**.
5. Entrez un nom convivial pour l’application hello et sélectionnez le type d’application hello. Selon le type d’application hello ensemble hello URL de connexion ou les URL de l’URL de redirection toohello base. Cliquez sur **créer** application hello de toocreate.
6. Configurer des autorisations pour votre application - dans le menu Paramètres de hello, choisissez hello **autorisations requises** section, cliquez sur **ajouter**, puis **sélectionner une API**et type Bonjour nom du service de couche intermédiaire hello dans la zone de texte hello. Ensuite, cliquez sur **Sélectionner les autorisations**, puis sélectionnez Accéder à *nom du service*.

### Configurer les applications clientes connues
Dans ce scénario, service de niveau intermédiaire hello n’a aucune interaction tooobtain hello utilisateur API en aval de hello tooaccess de consentement. Par conséquent, hello option toogrant accès toohello API en aval doit être présenté initial dans le cadre de l’étape de consentement hello lors de l’authentification.
tooachieve, enregistrement tooexplicitly liaison hello d’une application cliente dans Azure AD avec l’enregistrement du service de couche intermédiaire hello, qui fusionne le consentement hello requis par hello client et le niveau intermédiaire dans une boîte de dialogue unique hello suit hello de suivi.
1. Accédez de l’inscription du service de couche intermédiaire toohello, puis cliquez sur **manifeste** éditeur de manifeste tooopen hello.
2. Dans le manifeste de hello, recherchez hello `knownClientApplications` propriété de tableau et d’ajouter un élément hello ID Client de l’application cliente de hello.
3. Enregistrer le manifeste de hello en cliquant sur hello bouton Enregistrer.

## Demande de jeton d’accès service tooservice
toorequest un jeton d’accès, faire un point de terminaison HTTP POST toohello spécifique au locataire Azure AD à hello paramètres suivants.

```
https://login.microsoftonline.com/<tenant>/oauth2/token
```
Il existe deux cas selon si application cliente de hello choisit toobe sécurisé par un secret partagé ou un certificat.

### Premier cas : demande de jeton d’accès avec un secret partagé
Lorsque vous utilisez un secret partagé, une demande de jeton d’accès de service à service contient hello paramètres suivants :

| Paramètre |  | Description |
| --- | --- | --- |
| grant_type |required | type de Hello de demande de jeton hello. Pour une demande à l’aide d’un jeton Web JSON, la valeur de hello doit être **urn : ietf:params:oauth:grant-type : jwt-support**. |
| assertion |required | valeur Hello du jeton hello utilisé dans la demande de hello. |
| client_id |required | Hello ID d’application assigné toohello service d’appel pendant l’inscription auprès d’Azure AD. toofind hello ID d’application Bonjour portail de gestion Azure, cliquez sur **Active Directory**, cliquez sur le répertoire hello, puis cliquez sur le nom de l’application hello. |
| client_secret |required | clé de Hello enregistrée pour hello appel de service dans Azure AD. Cette valeur doit avoir été indiquée lors de l’inscription hello. |
| resource |required | Hello URI ID d’application de service (ressource sécurisée) qui reçoit des hello. toofind hello URI ID d’application Bonjour portail de gestion Azure, cliquez sur **Active Directory**, cliquez sur le répertoire de hello, cliquez sur le nom de l’application hello **tous les paramètres** puis cliquez sur **propriétés** . |
| requested_token_use |required | Spécifie le mode de traitement de demande de hello. Bonjour de la part de flux, la valeur de hello doit être **on_behalf_of**. |
| scope |required | Un espace de liste séparée par des étendues de demande de jeton hello. Pour OpenID Connect, hello étendue **openid** doit être spécifié.|

#### Exemple
Hello requête HTTP POST suivante demande un jeton d’accès pour l’API web de https://graph.windows.net hello. Hello `client_id` identifie le service hello qui demande le jeton d’accès hello.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_secret=0Y1W%2BY3yYb3d9N8vSjvm8WrGzVZaAaHbHHcGbcgG%2BoI%3D
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

### Deuxième cas : demande de jeton d’accès avec un certificat
Une demande de jeton d’accès de service à service avec un certificat contient hello paramètres suivants :

| Paramètre |  | Description |
| --- | --- | --- |
| grant_type |required | type de Hello de demande de jeton hello. Pour une demande à l’aide d’un jeton Web JSON, la valeur de hello doit être **urn : ietf:params:oauth:grant-type : jwt-support**. |
| assertion |required | valeur Hello du jeton hello utilisé dans la demande de hello. |
| client_id |required | Hello ID d’application assigné toohello service d’appel pendant l’inscription auprès d’Azure AD. toofind hello ID d’application Bonjour portail de gestion Azure, cliquez sur **Active Directory**, cliquez sur le répertoire hello, puis cliquez sur le nom de l’application hello. |
| client_assertion_type |required |la valeur Hello doit être`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |required | Une assertion (un jeton Web JSON) que vous avez besoin de toocreate et signe avec hello certificat que vous avez enregistré en tant qu’informations d’identification pour votre application.  En savoir plus sur [informations d’identification de certificat](active-directory-certificate-credentials.md) toolearn comment tooregister votre format de certificat et hello d’assertion de hello.|
| resource |required | Hello URI ID d’application de service (ressource sécurisée) qui reçoit des hello. toofind hello URI ID d’application Bonjour portail de gestion Azure, cliquez sur **Active Directory**, cliquez sur le répertoire de hello, cliquez sur le nom de l’application hello **tous les paramètres** puis cliquez sur **propriétés** . |
| requested_token_use |required | Spécifie le mode de traitement de demande de hello. Bonjour de la part de flux, la valeur de hello doit être **on_behalf_of**. |
| scope |required | Un espace de liste séparée par des étendues de demande de jeton hello. Pour OpenID Connect, hello étendue **openid** doit être spécifié.|

Notez que les paramètres de hello sont presque identiques, comme dans les cas de hello de demande de hello hello par secret partagé, sauf que le paramètre de client_secret hello est remplacé par deux paramètres : un client_assertion_type et un client_assertion.

#### Exemple
Hello suivant HTTP POST demande un jeton d’accès pour le web hello https://graph.windows.net API avec un certificat. Hello `client_id` identifie le service hello qui demande le jeton d’accès hello.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

## Réponse de jeton service tooservice d’accès
Une réponse de réussite est une réponse JSON OAuth 2.0 avec les paramètres suivants de hello.

| Paramètre | Description |
| --- | --- |
| token_type |Indique la valeur de jeton de type hello. Hello uniquement le type qui prend en charge d’Azure AD est **support**. Pour plus d’informations sur les jetons de support, consultez hello [OAuth 2.0 Authorization Framework : Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| scope |étendue Hello d’accès accordé dans un jeton de hello. |
| expires_in |la longueur de jeton d’accès temps hello Hello est valide (en secondes). |
| expires_on |Hello date d’expiration jeton d’accès hello. date de Hello est représenté en tant que nombre hello de secondes entre 1970-01-01T0:0:0Z UTC jusqu'à ce que le délai d’expiration de hello. Cette valeur est la durée de vie utilisé toodetermine hello de jetons mis en cache. |
| resource |Hello URI ID d’application de service (ressource sécurisée) qui reçoit des hello. |
| access_token |jeton d’accès demandé Hello. Hello appel du service peut utiliser ce service de réception toohello tooauthenticate jeton. |
| id_token |jeton d’id demandée Hello. Hello appel du service peut utiliser l’identité de cet utilisateur hello tooverify et démarrer une session avec l’utilisateur de hello. |
| refresh_token |jeton d’actualisation Hello pour hello demandé un jeton d’accès. Hello appel du service peut utiliser ce jeton toorequest un autre jeton d’accès après l’expiration du jeton d’accès actuel hello. |

### Exemple de réponse correspondant à une réussite
Hello exemple suivant illustre une demande de tooa de réponse de réussite pour un jeton d’accès pour l’API web de https://graph.windows.net hello.

```
{
    "token_type":"Bearer",
    "scope":"User.Read",
    "expires_in":"43482",
    "ext_expires_in":"302683",
    "expires_on":"1493466951",
    "not_before":"1493423168",
    "resource":"https://graph.windows.net",
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ",
    "refresh_token":"AQABAAAAAABnfiG-mA6NTae7CdWW7QfdjKGu9-t1scy_TDEmLi4eLQMjJGt_nAoVu6A4oSu1KsRiz8XyQIPKQxSGfbf2FoSK-hm2K8TYzbJuswYusQpJaHUQnSqEvdaCeFuqXHBv84wjFhuanzF9dQZB_Ng5za9xKlUENrNtlq9XuLNVKzxEyeUM7JyxzdY7JiEphWImwgOYf6II316d0Z6-H3oYsFezf4Xsjz-MOBYEov0P64UaB5nJMvDyApV-NWpgklLASfNoSPGb67Bc02aFRZrm4kLk-xTl6eKE6hSo0XU2z2t70stFJDxvNQobnvNHrAmBaHWPAcC3FGwFnBOojpZB2tzG1gLEbmdROVDp8kHEYAwnRK947Py12fJNKExUdN0njmXrKxNZ_fEM33LHW1Tf4kMX_GvNmbWHtBnIyG0w5emb-b54ef5AwV5_tGUeivTCCysgucEc-S7G8Cz0xNJ_BOiM_4bAv9iFmrm9STkltpz0-Tftg8WKmaJiC0xXj6uTf4ZkX79mJJIuuM7XP4ARIcLpkktyg2Iym9jcZqymRkGH2Rm9sxBwC4eeZXM7M5a7TJ-5CqOdfuE3sBPq40RdEWMFLcrAzFvP0VDR8NKHIrPR1AcUruat9DETmTNJukdlJN3O41nWdZOVoJM-uKN3uz2wQ2Ld1z0Mb9_6YfMox9KTJNzRzcL52r4V_y3kB6ekaOZ9wQ3HxGBQ4zFt-2U0mSszIAA",
    "id_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IvIiwiaWF0IjoxNDkzNDIzMTY4LCJuYmYiOjE0OTM0MjMxNjgsImV4cCI6MTQ5MzQ2Njk1MSwiYW1yIjpbInB3ZCJdLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXRpIjoieEN3ZnpoYS1QMFdKUU9MeENHZ0tBQSIsInZlciI6IjEuMCJ9."
}
```

### Exemple de réponse d’erreur
Une réponse d’erreur est retournée par le point de terminaison de jeton Azure AD lors de la tentative de tooacquire un jeton d’accès pour les API en aval hello, si les API en aval hello possède une stratégie d’accès conditionnel telles que l’authentification multifacteur activée. service de niveau intermédiaire Hello devrait apparaître cette application cliente de toohello erreur afin que l’application cliente de hello peut fournir la stratégie d’accès conditionnel hello utilisateur interaction toosatisfy hello.

```
{
    "error":"interaction_required",
    "error_description":"AADSTS50079: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must enroll in multi-factor authentication tooaccess 'bf8d80f9-9098-4972-b203-500f535113b1'.\r\nTrace ID: b72a68c3-0926-4b8e-bc35-3150069c2800\r\nCorrelation ID: 73d656cf-54b1-4eb2-b429-26d8165a52d7\r\nTimestamp: 2017-05-01 22:43:20Z",
    "error_codes":[50079],
    "timestamp":"2017-05-01 22:43:20Z",
    "trace_id":"b72a68c3-0926-4b8e-bc35-3150069c2800",
    "correlation_id":"73d656cf-54b1-4eb2-b429-26d8165a52d7",
    "claims":"{\"access_token\":{\"polids\":{\"essential\":true,\"values\":[\"9ab03e19-ed42-4168-b6b7-7001fb3e933a\"]}}}"
}
```

## Utilisez hello de tooaccess de jeton d’accès hello ressource sécurisée
Service de niveau intermédiaire hello pouvez désormais utiliser toohello de demandes de jeton toomake acquis ci-dessus authentifié hello en aval web API, en définissant le jeton hello Bonjour `Authorization` en-tête.

### Exemple
```
GET /me?api-version=2013-11-08 HTTP/1.1
Host: graph.windows.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ
```

## Étapes suivantes
En savoir plus sur le protocole de hello OAuth 2.0 et une autre façon tooperform service tooservice d’authentification à l’aide des informations d’identification du client.
* [Authentification tooservice de service à l’aide d’octroi des informations d’identification du client OAuth 2.0 dans Azure AD](active-directory-protocols-oauth-service-to-service.md)
* [OAuth 2.0 dans Azure AD](active-directory-protocols-oauth-code.md)
