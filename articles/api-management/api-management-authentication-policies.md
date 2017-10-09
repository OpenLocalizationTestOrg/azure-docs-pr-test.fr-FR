---
title: "stratégies d’authentification de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les stratégies d’authentification disponibles pour une utilisation dans la gestion des API Azure hello."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a>Stratégies d’authentification dans Gestion des API
Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API. Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AuthenticationPolicies"></a> Stratégies d’authentification  
  
-   [Authenticate with Basic](api-management-authentication-policies.md#Basic) : authentification avec un service principal à l’aide de l’authentification de base.  
  
-   [Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) : authentification avec un service principal à l’aide de certificats clients.  
  
##  <a name="Basic"></a> Authenticate with Basic  
 Hello d’utilisation `authentication-basic` tooauthenticate de stratégie avec un service principal à l’aide de l’authentification de base. Cette stratégie définit efficacement hello d’autorisation HTTP en-tête toohello valeur correspondante toohello informations d’identification fournies dans la stratégie de hello.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|authentification-basic|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|username|Spécifie le nom d’utilisateur hello des informations d’identification de base hello.|Oui|N/A|  
|password|Spécifie le mot de passe hello des informations d’identification de base hello.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** API  
  
##  <a name="ClientCertificate"></a> Authenticate with client certificate  
 Hello d’utilisation `authentication-certificate` tooauthenticate de stratégie avec un service principal à l’aide du certificat client. certificat de Hello doit toobe [installé dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=511599) premier et est identifiée par son empreinte numérique.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|authentication-certificate|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|thumbprint|Bonjour à l’empreinte numérique du certificat client hello.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** API  
  

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).  