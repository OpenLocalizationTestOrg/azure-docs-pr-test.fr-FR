---
title: "informations d’identification aaaCertificate dans Azure AD | Documents Microsoft"
description: "Cet article traite de l’inscription de hello et l’utilisation des informations d’identification de certificat pour l’authentification de l’application"
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a>Informations d’identification de certificat pour l’authentification d’application

Azure Active Directory permet un toouse application ses propres informations d’identification pour l’authentification, par exemple, dans le flux d’octroi d’informations d’identification clientes OAuth 2.0 hello et hello sur à la place de flux.
Une forme d’informations d’identification qui peuvent être utilisée est une assertion de JSON Web Token(JWT) signée avec un certificat qui possède de l’application hello.

## <a name="format-of-hello-assertion"></a>Format de hello assertion
assertion de hello toocompute, vous souhaitez probablement que toouse d'entre hello nombreux [jeton Web JSON](https://jwt.io/) bibliothèques en langage hello de votre choix. les informations par le jeton de hello Hello sont :

#### <a name="header"></a>En-tête

| Paramètre |  Remarque |
| --- | --- | --- |
| `alg` | Doit être **RS256** |
| `typ` | Doit être **JWT** |
| `x5t` | Doit être une empreinte numérique SHA-1 de certificat X.509 de hello |

#### <a name="claims-payload"></a>Revendications (charge utile)

| Paramètre |  Remarque |
| --- | --- | --- |
| `aud` | Public : doit être **https://login.microsoftonline.com/*tenant_Id*/oauth2/token** |
| `exp` | Date d’expiration : date hello d’expiration du jeton de hello. temps de Hello est représenté en hello secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC avant l’expiration de la validité du jeton hello temps hello.|
| `iss` | Émetteur : doit être hello client_id (Id d’Application de service du client hello) |
| `jti` | GUID : hello JWT ID |
| `nbf` | Pas avant : hello date avant le hello jeton ne peut pas être utilisé. temps de Hello est représenté en hello secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu'à ce que le jeton de hello hello temps a été émis. |
| `sub` | Objet : comme pour `iss`, doit être hello client_id (Id d’Application de service du client hello) |

#### <a name="signature"></a>Signature
signature de Hello est calculée appliquer certificat de hello, comme décrit dans hello [RFC7519 de jeton Web JSON spécification](https://tools.ietf.org/html/rfc7519)

### <a name="example-of-a-decoded-jwt-assertion"></a>Exemple d’une assertion JWT décodée
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a>Exemple d’une assertion JWT encodée
Hello suivant de chaîne est un exemple d’assertion encodé. Si vous regardez attentivement, vous remarquerez les trois sections séparées par des points (.).
première section de Hello encode en-tête hello, hello deuxième hello charge utile, et hello est dernière signature hello calculée avec des certificats à partir du contenu hello des deux premières sections de hello hello.
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a>Inscrire votre certificat dans Azure AD
tooassociate hello certificat informations d’identification avec l’application cliente de hello dans Azure AD, vous devez le manifeste de l’application hello tooedit.
De blocage d’un certificat, vous devez toocompute :
- `$base64Thumbprint`, qui est hello encodage base64 du certificat de hello hachage
- `$base64Value`, qui est hello encodage base64 de données brutes du certificat hello

Vous devez également tooprovide une clé de hello tooidentify GUID dans le manifeste de l’application hello (`$keyId`)

Bonjour inscription d’une application Azure pour l’application cliente de hello, ouvrez le manifeste de l’application hello et remplacez hello *keyCredentials* propriété avec vos nouvelles informations de certificat à l’aide de hello suivant le schéma :
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

Enregistrer le manifeste de l’application hello modifications toohello et téléchargez tooAzure AD. propriété de keyCredentials Hello est à valeurs multiples, vous risquez de télécharger plusieurs certificats de gestion de clés plus riche.
