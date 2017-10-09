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
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a>Comment toosecure API client à l’aide de certificat d’authentification dans Gestion des API

Gestion des API fournit hello capacité toosecure accès tooAPIs (par exemple, client tooAPI Management) à l’aide de certificats clients. Actuellement, vous pouvez vérifier l’empreinte numérique hello d’un certificat client par rapport à la valeur souhaitée. Vous pouvez également vérifier l’empreinte numérique hello contre les certificats existants téléchargés tooAPI Management.  

Pour plus d’informations sur la sécurisation des accès toohello back-end d’une API à l’aide de certificats de client (par exemple, gestion des API tooback-fin), consultez [comment toosecure services de back-end à l’aide du client de certificat d’authentification](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)

## <a name="checking-hello-expiration-date"></a>La vérification de la date d’expiration de hello

Sous stratégies peut être configuré toocheck si le certificat de hello est arrivé à expiration :

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a>La vérification de sujet et l’émetteur de hello

Sous stratégies peut être configuré toocheck hello émetteur et l’objet d’un certificat client :

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a>La vérification de l’empreinte numérique hello

Sous stratégies peut être l’empreinte numérique de hello toocheck configuré d’un certificat client :

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a>La vérification d’une empreinte numérique contre les certificats téléchargés tooAPI gestion

Hello suivant montre comment l’empreinte numérique de hello toocheck d’un certificat client contre les certificats téléchargés tooAPI gestion : 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a>Étape suivante

*  [Comment l’authentification des certificats toosecure services de back-end à l’aide du client](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [Comment les certificats tooupload](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

