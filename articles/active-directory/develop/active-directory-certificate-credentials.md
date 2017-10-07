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
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="17c18-103">Informations d’identification de certificat pour l’authentification d’application</span><span class="sxs-lookup"><span data-stu-id="17c18-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="17c18-104">Azure Active Directory permet un toouse application ses propres informations d’identification pour l’authentification, par exemple, dans le flux d’octroi d’informations d’identification clientes OAuth 2.0 hello et hello sur à la place de flux.</span><span class="sxs-lookup"><span data-stu-id="17c18-104">Azure Active Directory allows an application toouse its own credentials for authentication, for example, in hello OAuth 2.0 Client Credentials Grant flow and hello On-Behalf-Of flow.</span></span>
<span data-ttu-id="17c18-105">Une forme d’informations d’identification qui peuvent être utilisée est une assertion de JSON Web Token(JWT) signée avec un certificat qui possède de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="17c18-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that hello application owns.</span></span>

## <a name="format-of-hello-assertion"></a><span data-ttu-id="17c18-106">Format de hello assertion</span><span class="sxs-lookup"><span data-stu-id="17c18-106">Format of hello assertion</span></span>
<span data-ttu-id="17c18-107">assertion de hello toocompute, vous souhaitez probablement que toouse d'entre hello nombreux [jeton Web JSON](https://jwt.io/) bibliothèques en langage hello de votre choix.</span><span class="sxs-lookup"><span data-stu-id="17c18-107">toocompute hello assertion, you probably want toouse one of hello many [JSON Web Token](https://jwt.io/) libraries in hello language of your choice.</span></span> <span data-ttu-id="17c18-108">les informations par le jeton de hello Hello sont :</span><span class="sxs-lookup"><span data-stu-id="17c18-108">hello information carried by hello token is:</span></span>

#### <a name="header"></a><span data-ttu-id="17c18-109">En-tête</span><span class="sxs-lookup"><span data-stu-id="17c18-109">Header</span></span>

| <span data-ttu-id="17c18-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="17c18-110">Parameter</span></span> |  <span data-ttu-id="17c18-111">Remarque</span><span class="sxs-lookup"><span data-stu-id="17c18-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="17c18-112">Doit être **RS256**</span><span class="sxs-lookup"><span data-stu-id="17c18-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="17c18-113">Doit être **JWT**</span><span class="sxs-lookup"><span data-stu-id="17c18-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="17c18-114">Doit être une empreinte numérique SHA-1 de certificat X.509 de hello</span><span class="sxs-lookup"><span data-stu-id="17c18-114">Should be hello X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="17c18-115">Revendications (charge utile)</span><span class="sxs-lookup"><span data-stu-id="17c18-115">Claims (Payload)</span></span>

| <span data-ttu-id="17c18-116">Paramètre</span><span class="sxs-lookup"><span data-stu-id="17c18-116">Parameter</span></span> |  <span data-ttu-id="17c18-117">Remarque</span><span class="sxs-lookup"><span data-stu-id="17c18-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="17c18-118">Public : doit être **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="17c18-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="17c18-119">Date d’expiration : date hello d’expiration du jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="17c18-119">Expiration date: hello date when hello token expires.</span></span> <span data-ttu-id="17c18-120">temps de Hello est représenté en hello secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC avant l’expiration de la validité du jeton hello temps hello.</span><span class="sxs-lookup"><span data-stu-id="17c18-120">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token validity expires.</span></span>|
| `iss` | <span data-ttu-id="17c18-121">Émetteur : doit être hello client_id (Id d’Application de service du client hello)</span><span class="sxs-lookup"><span data-stu-id="17c18-121">Issuer: should be hello client_id (Application Id of hello client service)</span></span> |
| `jti` | <span data-ttu-id="17c18-122">GUID : hello JWT ID</span><span class="sxs-lookup"><span data-stu-id="17c18-122">GUID: hello JWT ID</span></span> |
| `nbf` | <span data-ttu-id="17c18-123">Pas avant : hello date avant le hello jeton ne peut pas être utilisé.</span><span class="sxs-lookup"><span data-stu-id="17c18-123">Not Before: hello date before which hello token cannot be used.</span></span> <span data-ttu-id="17c18-124">temps de Hello est représenté en hello secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu'à ce que le jeton de hello hello temps a été émis.</span><span class="sxs-lookup"><span data-stu-id="17c18-124">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token was issued.</span></span> |
| `sub` | <span data-ttu-id="17c18-125">Objet : comme pour `iss`, doit être hello client_id (Id d’Application de service du client hello)</span><span class="sxs-lookup"><span data-stu-id="17c18-125">Subject: As for `iss`, should be hello client_id (Application Id of hello client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="17c18-126">Signature</span><span class="sxs-lookup"><span data-stu-id="17c18-126">Signature</span></span>
<span data-ttu-id="17c18-127">signature de Hello est calculée appliquer certificat de hello, comme décrit dans hello [RFC7519 de jeton Web JSON spécification](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="17c18-127">hello signature is computed applying hello certificate as described in hello [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="17c18-128">Exemple d’une assertion JWT décodée</span><span class="sxs-lookup"><span data-stu-id="17c18-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="17c18-129">Exemple d’une assertion JWT encodée</span><span class="sxs-lookup"><span data-stu-id="17c18-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="17c18-130">Hello suivant de chaîne est un exemple d’assertion encodé.</span><span class="sxs-lookup"><span data-stu-id="17c18-130">hello following string is an example of encoded assertion.</span></span> <span data-ttu-id="17c18-131">Si vous regardez attentivement, vous remarquerez les trois sections séparées par des points (.).</span><span class="sxs-lookup"><span data-stu-id="17c18-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="17c18-132">première section de Hello encode en-tête hello, hello deuxième hello charge utile, et hello est dernière signature hello calculée avec des certificats à partir du contenu hello des deux premières sections de hello hello.</span><span class="sxs-lookup"><span data-stu-id="17c18-132">hello first section encodes hello header, hello second hello payload, and hello last is hello signature computed with hello certificates from hello content of hello first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="17c18-133">Inscrire votre certificat dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="17c18-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="17c18-134">tooassociate hello certificat informations d’identification avec l’application cliente de hello dans Azure AD, vous devez le manifeste de l’application hello tooedit.</span><span class="sxs-lookup"><span data-stu-id="17c18-134">tooassociate hello certificate credential with hello client application in Azure AD, you need tooedit hello application manifest.</span></span>
<span data-ttu-id="17c18-135">De blocage d’un certificat, vous devez toocompute :</span><span class="sxs-lookup"><span data-stu-id="17c18-135">Having hold of a certificate, you need toocompute:</span></span>
- <span data-ttu-id="17c18-136">`$base64Thumbprint`, qui est hello encodage base64 du certificat de hello hachage</span><span class="sxs-lookup"><span data-stu-id="17c18-136">`$base64Thumbprint`, which is hello base64 encoding of hello certificate Hash</span></span>
- <span data-ttu-id="17c18-137">`$base64Value`, qui est hello encodage base64 de données brutes du certificat hello</span><span class="sxs-lookup"><span data-stu-id="17c18-137">`$base64Value`, which is hello base64 encoding of hello certificate raw data</span></span>

<span data-ttu-id="17c18-138">Vous devez également tooprovide une clé de hello tooidentify GUID dans le manifeste de l’application hello (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="17c18-138">you also need tooprovide a GUID tooidentify hello key in hello application manifest (`$keyId`)</span></span>

<span data-ttu-id="17c18-139">Bonjour inscription d’une application Azure pour l’application cliente de hello, ouvrez le manifeste de l’application hello et remplacez hello *keyCredentials* propriété avec vos nouvelles informations de certificat à l’aide de hello suivant le schéma :</span><span class="sxs-lookup"><span data-stu-id="17c18-139">In hello Azure app registration for hello client application, open hello application manifest, and replace hello *keyCredentials* property with your new certificate information using hello following schema:</span></span>
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

<span data-ttu-id="17c18-140">Enregistrer le manifeste de l’application hello modifications toohello et téléchargez tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="17c18-140">Save hello edits toohello application manifest, and upload tooAzure AD.</span></span> <span data-ttu-id="17c18-141">propriété de keyCredentials Hello est à valeurs multiples, vous risquez de télécharger plusieurs certificats de gestion de clés plus riche.</span><span class="sxs-lookup"><span data-stu-id="17c18-141">hello keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
