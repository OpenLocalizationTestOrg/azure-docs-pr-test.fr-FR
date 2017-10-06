---
title: "aaaAzure tooService de AD Service d’authentification à l’aide d’OAuth2.0 | Documents Microsoft"
description: "Cet article décrit comment toouse HTTP messages tooimplement service tooservice l’authentification à l’aide de flux d’octroi d’informations d’identification client hello OAuth2.0."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f4bfd4ea8a7de1929c7dcf7ad65a156edff74f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Appels de tooservice service à l’aide des informations d’identification du client (secret partagé ou certificat)
Hello flux d’octroi d’informations d’identification OAuth 2.0 Client permet à un service web (*client confidentiel*) toouse service web de ses propres informations d’identification au lieu d’emprunter l’identité d’un utilisateur, tooauthenticate lors de l’appel à un autre. Dans ce scénario, le client de hello est généralement un service web de couche intermédiaire, un service démon ou un site web. Pour augmenter le niveau d’assurance, Azure AD permet également hello appelant service toouse un certificat (au lieu d’un secret partagé) en tant qu’informations d’identification.

## Diagramme représentant le flux d’octroi des informations d’identification du client
Hello diagramme suivant explique comment les informations d’identification du client hello allouer works de flux dans Azure Active Directory (Azure AD).

![Flux d’octroi des informations d’identification du client OAuth2.0](media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. application cliente de Hello authentifie le point de terminaison d’émission de jeton de Azure AD toohello et demande un jeton d’accès.
2. problèmes de point de terminaison d’émission de jeton Azure AD de Hello hello jeton d’accès.
3. jeton d’accès Hello est toohello tooauthenticate utilisé ressource sécurisée.
4. Les données à partir de la ressource sécurisée de hello sont retournées d’application web de toohello.

## Inscrire les Services hello dans Azure AD
Enregistrer hello appel du service et hello réception service dans Azure Active Directory (Azure AD). Pour obtenir des instructions détaillées, consultez [Intégration d’applications dans Azure Active Directory](active-directory-integrating-applications.md).

## Demander un jeton d’accès
toorequest un jeton d’accès, utilisez un point de terminaison HTTP POST toohello spécifique au locataire Azure AD.

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## Demande de jeton d’accès de service à service
Il existe deux cas selon si application cliente de hello choisit toobe sécurisé par un secret partagé ou un certificat.

### Premier cas : demande de jeton d’accès avec un secret partagé
Lorsque vous utilisez un secret partagé, une demande de jeton d’accès de service à service contient hello paramètres suivants :

| Paramètre |  | Description |
| --- | --- | --- |
| grant_type |required |Spécifie les hello demandé accorder le type. Dans un flux d’octroi des informations d’identification du Client, la valeur de hello doit être **valeur client_credentials**. |
| client_id |required |Spécifie l’id de client Azure AD hello Hello appel de service web. hello toofind ID de client de l’application, l’appel Bonjour [portail Azure](https://portal.azure.com), cliquez sur **Active Directory**, commutateur active, cliquez sur l’application hello. les client_id Hello est hello *ID d’Application* |
| client_secret |required |Entrez une clé inscrite pour hello appel d’application de service ou démon web dans Azure AD. toocreate une clé, Bonjour portail Azure, cliquez sur **Active Directory**, commutateur active, cliquez sur l’application hello, cliquez sur **paramètres**, cliquez sur **clés**, et ajouter une clé.|
| resource |required |Entrez hello URI ID d’application de réception du service web de hello. toofind hello URI ID d’application Bonjour portail Azure, cliquez sur **Active Directory**, commutateur active, cliquez sur l’application hello service, puis cliquez sur **paramètres** et **propriétés** |

#### Exemple
Hello requête HTTP POST suivante demande un jeton d’accès pour le service web de hello https://service.contoso.com/. Hello `client_id` identifie le service web hello qui demande le jeton d’accès hello.

```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

### Deuxième cas : demande de jeton d’accès avec un certificat
Une demande de jeton d’accès de service à service avec un certificat contient hello paramètres suivants :

| Paramètre |  | Description |
| --- | --- | --- |
| grant_type |required |Spécifie hello a demandé le type de réponse. Dans un flux d’octroi des informations d’identification du Client, la valeur de hello doit être **valeur client_credentials**. |
| client_id |required |Spécifie l’id de client Azure AD hello Hello appel de service web. hello toofind ID de client de l’application, l’appel Bonjour [portail Azure](https://portal.azure.com), cliquez sur **Active Directory**, commutateur active, cliquez sur l’application hello. les client_id Hello est hello *ID d’Application* |
| client_assertion_type |required |la valeur Hello doit être`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |required | Une assertion (un jeton Web JSON) que vous avez besoin de toocreate et signe avec hello certificat que vous avez enregistré en tant qu’informations d’identification pour votre application. En savoir plus sur [informations d’identification de certificat](active-directory-certificate-credentials.md) toolearn comment tooregister votre format de certificat et hello d’assertion de hello.|
| resource | required |Entrez hello URI ID d’application de réception du service web de hello. toofind hello URI ID d’application Bonjour portail Azure, cliquez sur **Active Directory**, cliquez sur le répertoire hello, cliquez sur l’application hello, puis cliquez sur **configurer**. |

Notez que les paramètres de hello sont presque identiques, comme dans les cas de hello de demande de hello hello par secret partagé, sauf que le paramètre de client_secret hello est remplacé par deux paramètres : un client_assertion_type et un client_assertion.

#### Exemple
Hello suivant HTTP POST demande un jeton d’accès pour le service de web https://service.contoso.com/ hello avec un certificat. Hello `client_id` identifie le service web hello qui demande le jeton d’accès hello.

```
POST /<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

resource=https%3A%2F%contoso.onmicrosoft.com%2Ffc7664b4-cdd6-43e1-9365-c2e1c4e1b3bf&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

### Réponse de jeton d’accès de service à service

Une réponse de réussite contient une réponse JSON OAuth 2.0 avec hello paramètres suivants :

| Paramètre | Description |
| --- | --- |
| access_token |jeton d’accès demandé Hello. Hello, appel de service web peut utiliser cette toohello tooauthenticate jeton réception de service web. |
| token_type |Indique la valeur de jeton de type hello. Hello uniquement le type qui prend en charge d’Azure AD est **support**. Pour plus d’informations sur les jetons de support, consultez hello [OAuth 2.0 Authorization Framework : Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| expires_in |La durée pendant laquelle le jeton d’accès hello est valide (en secondes). |
| expires_on |Hello date d’expiration jeton d’accès hello. date de Hello est représenté en tant que nombre hello de secondes entre 1970-01-01T0:0:0Z UTC jusqu'à ce que le délai d’expiration de hello. Cette valeur est la durée de vie utilisé toodetermine hello de jetons mis en cache. |
| not_before |heure de Hello à partir de quels hello le jeton d’accès peut être utilisé. date de Hello est représenté en tant que nombre hello de secondes entre 1970-01-01T0:0:0Z UTC jusqu’au moment de validité de jeton de hello.|
| resource |Hello URI ID d’application de réception du service web de hello. |

#### Exemple de réponse
Hello exemple suivant illustre une demande de tooa de réponse de réussite pour un service web de jeton tooa accès.

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## Voir aussi
* [OAuth 2.0 dans Azure AD](active-directory-protocols-oauth-code.md)
* [Exemple en c# de hello service tooservice appel avec un secret partagé](https://github.com/Azure-Samples/active-directory-dotnet-daemon) et [exemple en c# de hello service tooservice appel avec un certificat](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)
