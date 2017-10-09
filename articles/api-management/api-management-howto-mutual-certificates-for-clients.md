---
title: "aaaSecure API à l’aide de l’authentification du certificat client dans Gestion des API - gestion des API Azure | Documents Microsoft"
description: "Découvrez comment accéder à toosecure tooAPIs à l’aide de certificats clients"
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
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="beff7-103">Comment toosecure API client à l’aide de certificat d’authentification dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="beff7-103">How toosecure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="beff7-104">Gestion des API fournit hello capacité toosecure accès tooAPIs (par exemple, client tooAPI Management) à l’aide de certificats clients.</span><span class="sxs-lookup"><span data-stu-id="beff7-104">API Management provides hello capability toosecure access tooAPIs (i.e., client tooAPI Management) using client certificates.</span></span> <span data-ttu-id="beff7-105">Actuellement, vous pouvez vérifier l’empreinte numérique hello d’un certificat client par rapport à la valeur souhaitée.</span><span class="sxs-lookup"><span data-stu-id="beff7-105">Currently, you can check hello thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="beff7-106">Vous pouvez également vérifier l’empreinte numérique hello contre les certificats existants téléchargés tooAPI Management.</span><span class="sxs-lookup"><span data-stu-id="beff7-106">You can also check hello thumbprint against existing certificates uploaded tooAPI Management.</span></span>  

<span data-ttu-id="beff7-107">Pour plus d’informations sur la sécurisation des accès toohello back-end d’une API à l’aide de certificats de client (par exemple, gestion des API tooback-fin), consultez [comment toosecure services de back-end à l’aide du client de certificat d’authentification](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="beff7-107">For information about securing access toohello back-end service of an API using client certificates (i.e., API Management tooback-end), see [How toosecure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-hello-expiration-date"></a><span data-ttu-id="beff7-108">La vérification de la date d’expiration de hello</span><span class="sxs-lookup"><span data-stu-id="beff7-108">Checking hello expiration date</span></span>

<span data-ttu-id="beff7-109">Sous stratégies peut être configuré toocheck si le certificat de hello est arrivé à expiration :</span><span class="sxs-lookup"><span data-stu-id="beff7-109">Below policies can be configured toocheck if hello certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a><span data-ttu-id="beff7-110">La vérification de sujet et l’émetteur de hello</span><span class="sxs-lookup"><span data-stu-id="beff7-110">Checking hello issuer and subject</span></span>

<span data-ttu-id="beff7-111">Sous stratégies peut être configuré toocheck hello émetteur et l’objet d’un certificat client :</span><span class="sxs-lookup"><span data-stu-id="beff7-111">Below policies can be configured toocheck hello issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a><span data-ttu-id="beff7-112">La vérification de l’empreinte numérique hello</span><span class="sxs-lookup"><span data-stu-id="beff7-112">Checking hello thumbprint</span></span>

<span data-ttu-id="beff7-113">Sous stratégies peut être l’empreinte numérique de hello toocheck configuré d’un certificat client :</span><span class="sxs-lookup"><span data-stu-id="beff7-113">Below policies can be configured toocheck hello thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a><span data-ttu-id="beff7-114">La vérification d’une empreinte numérique contre les certificats téléchargés tooAPI gestion</span><span class="sxs-lookup"><span data-stu-id="beff7-114">Checking a thumbprint against certificates uploaded tooAPI Management</span></span>

<span data-ttu-id="beff7-115">Hello suivant montre comment l’empreinte numérique de hello toocheck d’un certificat client contre les certificats téléchargés tooAPI gestion :</span><span class="sxs-lookup"><span data-stu-id="beff7-115">hello following example shows how toocheck hello thumbprint of a client certificate against certificates uploaded tooAPI Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="beff7-116">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="beff7-116">Next step</span></span>

*  [<span data-ttu-id="beff7-117">Comment l’authentification des certificats toosecure services de back-end à l’aide du client</span><span class="sxs-lookup"><span data-stu-id="beff7-117">How toosecure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="beff7-118">Comment les certificats tooupload</span><span class="sxs-lookup"><span data-stu-id="beff7-118">How tooupload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

