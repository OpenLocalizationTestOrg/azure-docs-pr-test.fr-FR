---
title: "Sécuriser les API avec l’authentification de certificat client dans la gestion des API - Gestion des API Azure | Microsoft Docs"
description: "Apprenez à sécuriser l’accès aux API à l’aide des certificats clients"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: d3d51d0575a6d2dacced931601d48eb1e51a4051
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="f0d77-103">Comment sécuriser les API à l'aide d'une authentification par certificat client dans la Gestion des API</span><span class="sxs-lookup"><span data-stu-id="f0d77-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="f0d77-104">La Gestion des API permet de sécuriser l'accès aux API (par ex. client à gestion des API) en utilisant des certificats client.</span><span class="sxs-lookup"><span data-stu-id="f0d77-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="f0d77-105">Actuellement, vous pouvez vérifier l’empreinte numérique d’un certificat client par rapport à une valeur souhaitée.</span><span class="sxs-lookup"><span data-stu-id="f0d77-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="f0d77-106">Vous pouvez également vérifier l’empreinte numérique par rapport aux certificats existants téléchargés dans la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f0d77-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="f0d77-107">Pour plus d’informations sur la sécurisation de l’accès au service principal d’une API à l’aide de certificats clients (par exemple, gestion des API vers service principal), consultez [Comment sécuriser les services principaux à l’aide d’une authentification par certificat client](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates).</span><span class="sxs-lookup"><span data-stu-id="f0d77-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="f0d77-108">Vérification de la date d’expiration</span><span class="sxs-lookup"><span data-stu-id="f0d77-108">Checking the expiration date</span></span>

<span data-ttu-id="f0d77-109">Les stratégies ci-dessous peuvent être configurées pour vérifier si le certificat a expiré :</span><span class="sxs-lookup"><span data-stu-id="f0d77-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="f0d77-110">Vérification de l’émetteur et du sujet</span><span class="sxs-lookup"><span data-stu-id="f0d77-110">Checking the issuer and subject</span></span>

<span data-ttu-id="f0d77-111">Les stratégies suivantes peuvent être configurées pour vérifier l’émetteur et le sujet d’un certificat client :</span><span class="sxs-lookup"><span data-stu-id="f0d77-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="f0d77-112">Vérification de l’empreinte numérique</span><span class="sxs-lookup"><span data-stu-id="f0d77-112">Checking the thumbprint</span></span>

<span data-ttu-id="f0d77-113">Les stratégies suivantes peuvent être configurées pour vérifier l’empreinte d’un certificat client :</span><span class="sxs-lookup"><span data-stu-id="f0d77-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="f0d77-114">Vérification d’une empreinte par rapport aux certificats téléchargés dans la gestion des API</span><span class="sxs-lookup"><span data-stu-id="f0d77-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="f0d77-115">L’exemple suivant montre comment vérifier l’empreinte d’un certificat client par rapport aux certificats téléchargés dans la gestion des API :</span><span class="sxs-lookup"><span data-stu-id="f0d77-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="f0d77-116">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="f0d77-116">Next step</span></span>

*  [<span data-ttu-id="f0d77-117">Comment sécuriser les services principaux à l'aide d'une authentification par certificat client</span><span class="sxs-lookup"><span data-stu-id="f0d77-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="f0d77-118">Comment télécharger des certificats</span><span class="sxs-lookup"><span data-stu-id="f0d77-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

