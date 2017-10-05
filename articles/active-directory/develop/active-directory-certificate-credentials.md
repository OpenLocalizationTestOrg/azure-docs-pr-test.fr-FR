---
title: "Informations d’identification de certificat dans Azure AD | Microsoft Docs"
description: "Cet article traite de l’inscription et de l’utilisation des informations d’identification de certificat pour l’authentification d’application."
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
ms.openlocfilehash: 08bb5140bb35bbd120aaa506afeab8ad247f81e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="f2b16-103">Informations d’identification de certificat pour l’authentification d’application</span><span class="sxs-lookup"><span data-stu-id="f2b16-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="f2b16-104">Azure Active Directory permet à une application d’utiliser ses propres informations d’identification pour l’authentification (par exemple, le flux d’octroi d’informations d’identification du client d’OAuth 2.0 ou le flux On-Behalf-Of).</span><span class="sxs-lookup"><span data-stu-id="f2b16-104">Azure Active Directory allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow and the On-Behalf-Of flow.</span></span>
<span data-ttu-id="f2b16-105">Parmi les types d’informations d’identification que vous pouvez utiliser figure l’assertion JSON Web Token signée avec un certificat dont est propriétaire l’application.</span><span class="sxs-lookup"><span data-stu-id="f2b16-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span></span>

## <a name="format-of-the-assertion"></a><span data-ttu-id="f2b16-106">Format de l’assertion</span><span class="sxs-lookup"><span data-stu-id="f2b16-106">Format of the assertion</span></span>
<span data-ttu-id="f2b16-107">Pour calculer l’assertion, vous souhaiterez probablement utiliser l’une des nombreuses bibliothèques [JSON Web Token](https://jwt.io/) dans la langue de votre choix.</span><span class="sxs-lookup"><span data-stu-id="f2b16-107">To compute the assertion, you probably want to use one of the many [JSON Web Token](https://jwt.io/) libraries in the language of your choice.</span></span> <span data-ttu-id="f2b16-108">Les informations contenues dans le jeton sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2b16-108">The information carried by the token is:</span></span>

#### <a name="header"></a><span data-ttu-id="f2b16-109">En-tête</span><span class="sxs-lookup"><span data-stu-id="f2b16-109">Header</span></span>

| <span data-ttu-id="f2b16-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f2b16-110">Parameter</span></span> |  <span data-ttu-id="f2b16-111">Remarque</span><span class="sxs-lookup"><span data-stu-id="f2b16-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="f2b16-112">Doit être **RS256**</span><span class="sxs-lookup"><span data-stu-id="f2b16-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="f2b16-113">Doit être **JWT**</span><span class="sxs-lookup"><span data-stu-id="f2b16-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="f2b16-114">Doit être l’empreinte SHA-1 du certificat X.509</span><span class="sxs-lookup"><span data-stu-id="f2b16-114">Should be the X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="f2b16-115">Revendications (charge utile)</span><span class="sxs-lookup"><span data-stu-id="f2b16-115">Claims (Payload)</span></span>

| <span data-ttu-id="f2b16-116">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f2b16-116">Parameter</span></span> |  <span data-ttu-id="f2b16-117">Remarque</span><span class="sxs-lookup"><span data-stu-id="f2b16-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="f2b16-118">Public : doit être **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="f2b16-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="f2b16-119">Date d’expiration : date d’expiration du jeton.</span><span class="sxs-lookup"><span data-stu-id="f2b16-119">Expiration date: the date when the token expires.</span></span> <span data-ttu-id="f2b16-120">L’heure est représentée en nombre de secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu’à l’expiration du jeton.</span><span class="sxs-lookup"><span data-stu-id="f2b16-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span></span>|
| `iss` | <span data-ttu-id="f2b16-121">Émetteur : doit être le paramètre client_id (ID de l’application du service client)</span><span class="sxs-lookup"><span data-stu-id="f2b16-121">Issuer: should be the client_id (Application Id of the client service)</span></span> |
| `jti` | <span data-ttu-id="f2b16-122">GUID : ID JWT</span><span class="sxs-lookup"><span data-stu-id="f2b16-122">GUID: the JWT ID</span></span> |
| `nbf` | <span data-ttu-id="f2b16-123">Pas avant : date avant laquelle le jeton ne peut pas être utilisé.</span><span class="sxs-lookup"><span data-stu-id="f2b16-123">Not Before: the date before which the token cannot be used.</span></span> <span data-ttu-id="f2b16-124">L’heure est représentée en nombre de secondes à partir du 1er janvier 1970 (1970-01-01T0:0:0Z) UTC jusqu’au moment de l’émission du jeton.</span><span class="sxs-lookup"><span data-stu-id="f2b16-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span></span> |
| `sub` | <span data-ttu-id="f2b16-125">Objet : comme pour `iss`, doit être le paramètre client_id (ID de l’application du service client)</span><span class="sxs-lookup"><span data-stu-id="f2b16-125">Subject: As for `iss`, should be the client_id (Application Id of the client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="f2b16-126">Signature</span><span class="sxs-lookup"><span data-stu-id="f2b16-126">Signature</span></span>
<span data-ttu-id="f2b16-127">La signature est calculée en appliquant le certificat, conformément à la [spécification TFC7519 sur les jetons Web JSON](https://tools.ietf.org/html/rfc7519).</span><span class="sxs-lookup"><span data-stu-id="f2b16-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="f2b16-128">Exemple d’une assertion JWT décodée</span><span class="sxs-lookup"><span data-stu-id="f2b16-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="f2b16-129">Exemple d’une assertion JWT encodée</span><span class="sxs-lookup"><span data-stu-id="f2b16-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="f2b16-130">La chaîne suivante est un exemple d’assertion encodée.</span><span class="sxs-lookup"><span data-stu-id="f2b16-130">The following string is an example of encoded assertion.</span></span> <span data-ttu-id="f2b16-131">Si vous regardez attentivement, vous remarquerez les trois sections séparées par des points (.).</span><span class="sxs-lookup"><span data-stu-id="f2b16-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="f2b16-132">La première section encode l’en-tête ; la deuxième, la charge utile ; et la dernière, la signature calculée avec les certificats à partir du contenu des deux premières sections.</span><span class="sxs-lookup"><span data-stu-id="f2b16-132">The first section encodes the header, the second the payload, and the last is the signature computed with the certificates from the content of the first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="f2b16-133">Inscrire votre certificat dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2b16-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="f2b16-134">Pour associer les informations d’identification du certificat à l’application cliente dans Azure AD, vous devez modifier le manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="f2b16-134">To associate the certificate credential with the client application in Azure AD, you need to edit the application manifest.</span></span>
<span data-ttu-id="f2b16-135">Sur la base de votre certificat, vous devez calculer :</span><span class="sxs-lookup"><span data-stu-id="f2b16-135">Having hold of a certificate, you need to compute:</span></span>
- <span data-ttu-id="f2b16-136">`$base64Thumbprint`, qui est l’encodage en base64 du hachage de certificat</span><span class="sxs-lookup"><span data-stu-id="f2b16-136">`$base64Thumbprint`, which is the base64 encoding of the certificate Hash</span></span>
- <span data-ttu-id="f2b16-137">`$base64Value`, qui est l’encodage en base64 des données brutes du certificat</span><span class="sxs-lookup"><span data-stu-id="f2b16-137">`$base64Value`, which is the base64 encoding of the certificate raw data</span></span>

<span data-ttu-id="f2b16-138">Vous devez également fournir un GUID pour identifier la clé dans le manifeste d’application (`$keyId`).</span><span class="sxs-lookup"><span data-stu-id="f2b16-138">you also need to provide a GUID to identify the key in the application manifest (`$keyId`)</span></span>

<span data-ttu-id="f2b16-139">Dans la page d’inscription d’application Azure de l’application cliente, ouvrez le manifeste de l’application et remplacez la propriété *keyCredentials* par vos nouvelles informations de certificat en utilisant le schéma suivant :</span><span class="sxs-lookup"><span data-stu-id="f2b16-139">In the Azure app registration for the client application, open the application manifest, and replace the *keyCredentials* property with your new certificate information using the following schema:</span></span>
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

<span data-ttu-id="f2b16-140">Enregistrez les modifications du manifeste de l’application, puis chargez-le dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2b16-140">Save the edits to the application manifest, and upload to Azure AD.</span></span> <span data-ttu-id="f2b16-141">La propriété keyCredentials peut avoir plusieurs valeurs. Vous pouvez donc télécharger plusieurs certificats pour une gestion plus élaborée des clés.</span><span class="sxs-lookup"><span data-stu-id="f2b16-141">The keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
