---
title: aaaScheduler authentification sortante
description: Authentification sortante de Scheduler
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="be973-103">Authentification sortante de Scheduler</span><span class="sxs-lookup"><span data-stu-id="be973-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="be973-104">Tâches du planificateur peut-être toocall out tooservices qui requièrent une authentification.</span><span class="sxs-lookup"><span data-stu-id="be973-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="be973-105">De cette manière, un service appelé peut déterminer si la tâche du planificateur hello peut accéder à ses ressources.</span><span class="sxs-lookup"><span data-stu-id="be973-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="be973-106">Certains de ces services incluent d'autres services Azure, Salesforce.com, Facebook et des sites Web personnalisés sécurisés.</span><span class="sxs-lookup"><span data-stu-id="be973-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="be973-107">Ajout et suppression de l'authentification</span><span class="sxs-lookup"><span data-stu-id="be973-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="be973-108">Ajout de la tâche du planificateur d’authentification tooa est simple : ajouter un élément enfant JSON `authentication` toohello `request` élément lors de la création ou mise à jour d’un travail.</span><span class="sxs-lookup"><span data-stu-id="be973-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="be973-109">Les secrets transmis toohello planificateur dans une demande POST, PATCH ou PUT – dans le cadre de hello `authentication` de l’objet : ne sont jamais renvoyées dans les réponses.</span><span class="sxs-lookup"><span data-stu-id="be973-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="be973-110">Dans les réponses, les informations secrètes a la valeur toonull ou peuvent avoir un jeton public qui représente l’entité de hello authentifié.</span><span class="sxs-lookup"><span data-stu-id="be973-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="be973-111">l’authentification tooremove, PUT ou de corriger hello tâche explicitement, paramètre hello `authentication` toonull de l’objet.</span><span class="sxs-lookup"><span data-stu-id="be973-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="be973-112">Vous ne verrez pas de propriétés d'authentification en réponse.</span><span class="sxs-lookup"><span data-stu-id="be973-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="be973-113">Actuellement, hello pris en charge uniquement les types d’authentification sont hello `ClientCertificate` le modèle (pour utiliser des certificats de client SSL/TLS hello), hello `Basic` de modèle (pour l’authentification de base) et hello `ActiveDirectoryOAuth` (pour OAuth Active Directory authentification).</span><span class="sxs-lookup"><span data-stu-id="be973-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="be973-114">Corps de la requête pour l'authentification ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="be973-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="be973-115">Lors de l’ajout de l’authentification à l’aide de hello `ClientCertificate` du modèle, spécifiez hello suivant des éléments supplémentaires dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="be973-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="be973-116">Élément</span><span class="sxs-lookup"><span data-stu-id="be973-116">Element</span></span> | <span data-ttu-id="be973-117">Description</span><span class="sxs-lookup"><span data-stu-id="be973-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="be973-118">*authentification (élément parent)*</span><span class="sxs-lookup"><span data-stu-id="be973-118">*authentication (parent element)*</span></span> |<span data-ttu-id="be973-119">Objet d'authentification pour l'utilisation d'un certificat client SSL.</span><span class="sxs-lookup"><span data-stu-id="be973-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="be973-120">*type*</span><span class="sxs-lookup"><span data-stu-id="be973-120">*type*</span></span> |<span data-ttu-id="be973-121">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-121">Required.</span></span> <span data-ttu-id="be973-122">Type d’authentification. Pour les certificats clients SSL, la valeur de hello doit être `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="be973-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="be973-123">*pfx*</span><span class="sxs-lookup"><span data-stu-id="be973-123">*pfx*</span></span> |<span data-ttu-id="be973-124">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-124">Required.</span></span> <span data-ttu-id="be973-125">Codé en base 64 le contenu du fichier PFX de hello.</span><span class="sxs-lookup"><span data-stu-id="be973-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="be973-126">*mot de passe*</span><span class="sxs-lookup"><span data-stu-id="be973-126">*password*</span></span> |<span data-ttu-id="be973-127">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-127">Required.</span></span> <span data-ttu-id="be973-128">Fichier de mot de passe tooaccess hello PFX.</span><span class="sxs-lookup"><span data-stu-id="be973-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="be973-129">Corps de la réponse pour l'authentification ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="be973-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="be973-130">Lorsqu’une demande est envoyée avec les informations d’authentification, réponse de hello contient hello suit les éléments relatifs à l’authentification.</span><span class="sxs-lookup"><span data-stu-id="be973-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="be973-131">Élément</span><span class="sxs-lookup"><span data-stu-id="be973-131">Element</span></span> | <span data-ttu-id="be973-132">Description</span><span class="sxs-lookup"><span data-stu-id="be973-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="be973-133">*authentification (élément parent)*</span><span class="sxs-lookup"><span data-stu-id="be973-133">*authentication (parent element)*</span></span> |<span data-ttu-id="be973-134">Objet d'authentification pour l'utilisation d'un certificat client SSL.</span><span class="sxs-lookup"><span data-stu-id="be973-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="be973-135">*type*</span><span class="sxs-lookup"><span data-stu-id="be973-135">*type*</span></span> |<span data-ttu-id="be973-136">Type d'authentification.</span><span class="sxs-lookup"><span data-stu-id="be973-136">Type of authentication.</span></span> <span data-ttu-id="be973-137">Pour les certificats clients SSL, valeur de hello est `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="be973-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="be973-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="be973-138">*certificateThumbprint*</span></span> |<span data-ttu-id="be973-139">Hello empreinte numérique du certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="be973-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="be973-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="be973-140">*certificateSubjectName*</span></span> |<span data-ttu-id="be973-141">nom unique du sujet Hello du certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="be973-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="be973-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="be973-142">*certificateExpiration*</span></span> |<span data-ttu-id="be973-143">Hello date d’expiration hello certificat.</span><span class="sxs-lookup"><span data-stu-id="be973-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="be973-144">Exemple de requête REST pour l’authentification ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="be973-144">Sample REST Request for ClientCertificate Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="be973-145">Exemple de réponse REST pour l’authentification ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="be973-145">Sample REST Response for ClientCertificate Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="be973-146">Corps de la requête pour l'authentification de base</span><span class="sxs-lookup"><span data-stu-id="be973-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="be973-147">Lors de l’ajout de l’authentification à l’aide de hello `Basic` du modèle, spécifiez hello suivant des éléments supplémentaires dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="be973-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="be973-148">Élément</span><span class="sxs-lookup"><span data-stu-id="be973-148">Element</span></span> | <span data-ttu-id="be973-149">Description</span><span class="sxs-lookup"><span data-stu-id="be973-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="be973-150">*authentification (élément parent)*</span><span class="sxs-lookup"><span data-stu-id="be973-150">*authentication (parent element)*</span></span> |<span data-ttu-id="be973-151">Objet d'authentification pour l'authentification de base.</span><span class="sxs-lookup"><span data-stu-id="be973-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="be973-152">*type*</span><span class="sxs-lookup"><span data-stu-id="be973-152">*type*</span></span> |<span data-ttu-id="be973-153">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-153">Required.</span></span> <span data-ttu-id="be973-154">Type d'authentification.</span><span class="sxs-lookup"><span data-stu-id="be973-154">Type of authentication.</span></span> <span data-ttu-id="be973-155">L’authentification de base, la valeur de hello doit être `Basic`.</span><span class="sxs-lookup"><span data-stu-id="be973-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="be973-156">*nom d’utilisateur*</span><span class="sxs-lookup"><span data-stu-id="be973-156">*username*</span></span> |<span data-ttu-id="be973-157">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-157">Required.</span></span> <span data-ttu-id="be973-158">Nom d’utilisateur tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="be973-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="be973-159">*mot de passe*</span><span class="sxs-lookup"><span data-stu-id="be973-159">*password*</span></span> |<span data-ttu-id="be973-160">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-160">Required.</span></span> <span data-ttu-id="be973-161">Tooauthenticate de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="be973-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="be973-162">Corps de la réponse pour l'authentification de base</span><span class="sxs-lookup"><span data-stu-id="be973-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="be973-163">Lorsqu’une demande est envoyée avec les informations d’authentification, réponse de hello contient hello suit les éléments relatifs à l’authentification.</span><span class="sxs-lookup"><span data-stu-id="be973-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="be973-164">Élément</span><span class="sxs-lookup"><span data-stu-id="be973-164">Element</span></span> | <span data-ttu-id="be973-165">Description</span><span class="sxs-lookup"><span data-stu-id="be973-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="be973-166">*authentification (élément parent)*</span><span class="sxs-lookup"><span data-stu-id="be973-166">*authentication (parent element)*</span></span> |<span data-ttu-id="be973-167">Objet d'authentification pour l'authentification de base.</span><span class="sxs-lookup"><span data-stu-id="be973-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="be973-168">*type*</span><span class="sxs-lookup"><span data-stu-id="be973-168">*type*</span></span> |<span data-ttu-id="be973-169">Type d'authentification.</span><span class="sxs-lookup"><span data-stu-id="be973-169">Type of authentication.</span></span> <span data-ttu-id="be973-170">L’authentification de base, la valeur de hello est `Basic`.</span><span class="sxs-lookup"><span data-stu-id="be973-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="be973-171">*nom d’utilisateur*</span><span class="sxs-lookup"><span data-stu-id="be973-171">*username*</span></span> |<span data-ttu-id="be973-172">Hello authentifié un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="be973-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="be973-173">Exemple de requête REST pour l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="be973-173">Sample REST Request for Basic Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="be973-174">Exemple de réponse REST pour l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="be973-174">Sample REST Response for Basic Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="be973-175">Corps de la requête pour l'authentification ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="be973-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="be973-176">Lors de l’ajout de l’authentification à l’aide de hello `ActiveDirectoryOAuth` du modèle, spécifiez hello suivant des éléments supplémentaires dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="be973-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="be973-177">Élément</span><span class="sxs-lookup"><span data-stu-id="be973-177">Element</span></span> | <span data-ttu-id="be973-178">Description</span><span class="sxs-lookup"><span data-stu-id="be973-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="be973-179">*authentification (élément parent)*</span><span class="sxs-lookup"><span data-stu-id="be973-179">*authentication (parent element)*</span></span> |<span data-ttu-id="be973-180">Objet d'authentification pour l'authentification ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="be973-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="be973-181">*type*</span><span class="sxs-lookup"><span data-stu-id="be973-181">*type*</span></span> |<span data-ttu-id="be973-182">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-182">Required.</span></span> <span data-ttu-id="be973-183">Type d'authentification.</span><span class="sxs-lookup"><span data-stu-id="be973-183">Type of authentication.</span></span> <span data-ttu-id="be973-184">Pour l’authentification ActiveDirectoryOAuth, la valeur de hello doit être `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="be973-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="be973-185">*client*</span><span class="sxs-lookup"><span data-stu-id="be973-185">*tenant*</span></span> |<span data-ttu-id="be973-186">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-186">Required.</span></span> <span data-ttu-id="be973-187">Identificateur du locataire Hello pour le client de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be973-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="be973-188">*public ciblé*</span><span class="sxs-lookup"><span data-stu-id="be973-188">*audience*</span></span> |<span data-ttu-id="be973-189">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-189">Required.</span></span> <span data-ttu-id="be973-190">A la valeur toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="be973-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="be973-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="be973-191">*clientId*</span></span> |<span data-ttu-id="be973-192">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-192">Required.</span></span> <span data-ttu-id="be973-193">Identificateur de client hello prévoir de hello application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be973-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="be973-194">*secret*</span><span class="sxs-lookup"><span data-stu-id="be973-194">*secret*</span></span> |<span data-ttu-id="be973-195">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="be973-195">Required.</span></span> <span data-ttu-id="be973-196">Clé secrète du client hello qui demande hello jeton.</span><span class="sxs-lookup"><span data-stu-id="be973-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="be973-197">Déterminer votre identificateur de client</span><span class="sxs-lookup"><span data-stu-id="be973-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="be973-198">Vous pouvez trouver l’identificateur du locataire hello pour le client de hello Azure AD en exécutant `Get-AzureAccount` dans Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be973-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="be973-199">Corps de la réponse pour l'authentification ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="be973-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="be973-200">Lorsqu’une demande est envoyée avec les informations d’authentification, réponse de hello contient hello suit les éléments relatifs à l’authentification.</span><span class="sxs-lookup"><span data-stu-id="be973-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="be973-201">Élément</span><span class="sxs-lookup"><span data-stu-id="be973-201">Element</span></span> | <span data-ttu-id="be973-202">Description</span><span class="sxs-lookup"><span data-stu-id="be973-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="be973-203">*authentification (élément parent)*</span><span class="sxs-lookup"><span data-stu-id="be973-203">*authentication (parent element)*</span></span> |<span data-ttu-id="be973-204">Objet d'authentification pour l'authentification ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="be973-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="be973-205">*type*</span><span class="sxs-lookup"><span data-stu-id="be973-205">*type*</span></span> |<span data-ttu-id="be973-206">Type d'authentification.</span><span class="sxs-lookup"><span data-stu-id="be973-206">Type of authentication.</span></span> <span data-ttu-id="be973-207">Pour l’authentification ActiveDirectoryOAuth, valeur de hello est `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="be973-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="be973-208">*client*</span><span class="sxs-lookup"><span data-stu-id="be973-208">*tenant*</span></span> |<span data-ttu-id="be973-209">Identificateur du locataire Hello pour le client de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be973-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="be973-210">*public ciblé*</span><span class="sxs-lookup"><span data-stu-id="be973-210">*audience*</span></span> |<span data-ttu-id="be973-211">A la valeur toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="be973-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="be973-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="be973-212">*clientId*</span></span> |<span data-ttu-id="be973-213">Bonjour identificateur de client pour l’application hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be973-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="be973-214">Exemple de requête REST pour l’authentification ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="be973-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="be973-215">Exemple de réponse REST pour l’authentification ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="be973-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="be973-216">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="be973-216">See Also</span></span>
 [<span data-ttu-id="be973-217">Présentation d'Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="be973-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="be973-218">Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="be973-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="be973-219">Prise en main du planificateur Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="be973-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="be973-220">Plans et facturation dans Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="be973-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="be973-221">Informations de référence sur l’API REST d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="be973-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="be973-222">Informations de référence sur les applets de commande PowerShell d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="be973-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="be973-223">Haute disponibilité et fiabilité d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="be973-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="be973-224">Limites, valeurs par défaut et codes d’erreur d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="be973-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

