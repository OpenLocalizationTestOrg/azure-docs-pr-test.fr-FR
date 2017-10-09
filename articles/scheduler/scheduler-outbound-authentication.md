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
# <a name="scheduler-outbound-authentication"></a>Authentification sortante de Scheduler
Tâches du planificateur peut-être toocall out tooservices qui requièrent une authentification. De cette manière, un service appelé peut déterminer si la tâche du planificateur hello peut accéder à ses ressources. Certains de ces services incluent d'autres services Azure, Salesforce.com, Facebook et des sites Web personnalisés sécurisés.

## <a name="adding-and-removing-authentication"></a>Ajout et suppression de l'authentification
Ajout de la tâche du planificateur d’authentification tooa est simple : ajouter un élément enfant JSON `authentication` toohello `request` élément lors de la création ou mise à jour d’un travail. Les secrets transmis toohello planificateur dans une demande POST, PATCH ou PUT – dans le cadre de hello `authentication` de l’objet : ne sont jamais renvoyées dans les réponses. Dans les réponses, les informations secrètes a la valeur toonull ou peuvent avoir un jeton public qui représente l’entité de hello authentifié.

l’authentification tooremove, PUT ou de corriger hello tâche explicitement, paramètre hello `authentication` toonull de l’objet. Vous ne verrez pas de propriétés d'authentification en réponse.

Actuellement, hello pris en charge uniquement les types d’authentification sont hello `ClientCertificate` le modèle (pour utiliser des certificats de client SSL/TLS hello), hello `Basic` de modèle (pour l’authentification de base) et hello `ActiveDirectoryOAuth` (pour OAuth Active Directory authentification).

## <a name="request-body-for-clientcertificate-authentication"></a>Corps de la requête pour l'authentification ClientCertificate
Lors de l’ajout de l’authentification à l’aide de hello `ClientCertificate` du modèle, spécifiez hello suivant des éléments supplémentaires dans le corps de la demande hello.  

| Élément | Description |
|:--- |:--- |
| *authentification (élément parent)* |Objet d'authentification pour l'utilisation d'un certificat client SSL. |
| *type* |Obligatoire. Type d’authentification. Pour les certificats clients SSL, la valeur de hello doit être `ClientCertificate`. |
| *pfx* |Obligatoire. Codé en base 64 le contenu du fichier PFX de hello. |
| *mot de passe* |Obligatoire. Fichier de mot de passe tooaccess hello PFX. |

## <a name="response-body-for-clientcertificate-authentication"></a>Corps de la réponse pour l'authentification ClientCertificate
Lorsqu’une demande est envoyée avec les informations d’authentification, réponse de hello contient hello suit les éléments relatifs à l’authentification.

| Élément | Description |
|:--- |:--- |
| *authentification (élément parent)* |Objet d'authentification pour l'utilisation d'un certificat client SSL. |
| *type* |Type d'authentification. Pour les certificats clients SSL, valeur de hello est `ClientCertificate`. |
| *certificateThumbprint* |Hello empreinte numérique du certificat de hello. |
| *certificateSubjectName* |nom unique du sujet Hello du certificat de hello. |
| *certificateExpiration* |Hello date d’expiration hello certificat. |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a>Exemple de requête REST pour l’authentification ClientCertificate
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a>Exemple de réponse REST pour l’authentification ClientCertificate
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

## <a name="request-body-for-basic-authentication"></a>Corps de la requête pour l'authentification de base
Lors de l’ajout de l’authentification à l’aide de hello `Basic` du modèle, spécifiez hello suivant des éléments supplémentaires dans le corps de la demande hello.

| Élément | Description |
|:--- |:--- |
| *authentification (élément parent)* |Objet d'authentification pour l'authentification de base. |
| *type* |Obligatoire. Type d'authentification. L’authentification de base, la valeur de hello doit être `Basic`. |
| *nom d’utilisateur* |Obligatoire. Nom d’utilisateur tooauthenticate. |
| *mot de passe* |Obligatoire. Tooauthenticate de mot de passe. |

## <a name="response-body-for-basic-authentication"></a>Corps de la réponse pour l'authentification de base
Lorsqu’une demande est envoyée avec les informations d’authentification, réponse de hello contient hello suit les éléments relatifs à l’authentification.

| Élément | Description |
|:--- |:--- |
| *authentification (élément parent)* |Objet d'authentification pour l'authentification de base. |
| *type* |Type d'authentification. L’authentification de base, la valeur de hello est `Basic`. |
| *nom d’utilisateur* |Hello authentifié un nom d’utilisateur. |

## <a name="sample-rest-request-for-basic-authentication"></a>Exemple de requête REST pour l’authentification de base
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

## <a name="sample-rest-response-for-basic-authentication"></a>Exemple de réponse REST pour l’authentification de base
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a>Corps de la requête pour l'authentification ActiveDirectoryOAuth
Lors de l’ajout de l’authentification à l’aide de hello `ActiveDirectoryOAuth` du modèle, spécifiez hello suivant des éléments supplémentaires dans le corps de la demande hello.

| Élément | Description |
|:--- |:--- |
| *authentification (élément parent)* |Objet d'authentification pour l'authentification ActiveDirectoryOAuth. |
| *type* |Obligatoire. Type d'authentification. Pour l’authentification ActiveDirectoryOAuth, la valeur de hello doit être `ActiveDirectoryOAuth`. |
| *client* |Obligatoire. Identificateur du locataire Hello pour le client de hello Azure AD. |
| *public ciblé* |Obligatoire. A la valeur toohttps://management.core.windows.net/. |
| *clientId* |Obligatoire. Identificateur de client hello prévoir de hello application Azure AD. |
| *secret* |Obligatoire. Clé secrète du client hello qui demande hello jeton. |

### <a name="determining-your-tenant-identifier"></a>Déterminer votre identificateur de client
Vous pouvez trouver l’identificateur du locataire hello pour le client de hello Azure AD en exécutant `Get-AzureAccount` dans Azure PowerShell.

## <a name="response-body-for-activedirectoryoauth-authentication"></a>Corps de la réponse pour l'authentification ActiveDirectoryOAuth
Lorsqu’une demande est envoyée avec les informations d’authentification, réponse de hello contient hello suit les éléments relatifs à l’authentification.

| Élément | Description |
|:--- |:--- |
| *authentification (élément parent)* |Objet d'authentification pour l'authentification ActiveDirectoryOAuth. |
| *type* |Type d'authentification. Pour l’authentification ActiveDirectoryOAuth, valeur de hello est `ActiveDirectoryOAuth`. |
| *client* |Identificateur du locataire Hello pour le client de hello Azure AD. |
| *public ciblé* |A la valeur toohttps://management.core.windows.net/. |
| *clientId* |Bonjour identificateur de client pour l’application hello Azure AD. |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a>Exemple de requête REST pour l’authentification ActiveDirectoryOAuth
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a>Exemple de réponse REST pour l’authentification ActiveDirectoryOAuth
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

## <a name="see-also"></a>Voir aussi
 [Présentation d'Azure Scheduler](scheduler-intro.md)

 [Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler](scheduler-concepts-terms.md)

 [Prise en main du planificateur Bonjour portail Azure](scheduler-get-started-portal.md)

 [Plans et facturation dans Azure Scheduler](scheduler-plans-billing.md)

 [Informations de référence sur l’API REST d’Azure Scheluler](https://msdn.microsoft.com/library/mt629143)

 [Informations de référence sur les applets de commande PowerShell d’Azure Scheluler](scheduler-powershell-reference.md)

 [Haute disponibilité et fiabilité d’Azure Scheluler](scheduler-high-availability-reliability.md)

 [Limites, valeurs par défaut et codes d’erreur d’Azure Scheluler](scheduler-limits-defaults-errors.md)

