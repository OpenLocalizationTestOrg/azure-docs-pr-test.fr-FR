---
title: "Gestion des API d’aaaAzure stratégies inter-domaines | Documents Microsoft"
description: "Découvrez hello stratégies disponibles pour une utilisation dans la gestion des API Azure inter-domaines."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a>Gestion des API dans les stratégies de domaine
Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API. Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CrossDomainPolicies"></a> Stratégies inter-domaines  
  
-   [Autoriser les appels inter-domaines](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -rend hello API accessible à partir de clients basés sur navigateur Adobe Flash et Microsoft Silverlight.  
  
-   [CORS](api-management-cross-domain-policies.md#CORS) -ajoute le partage de ressources cross-origin (CORS) prend en charge les tooan opération ou une API tooallow entre domaines appelle à partir de clients de navigateur.  
  
-   [JSONP](api-management-cross-domain-policies.md#JSONP) - ajoute JSON padding (JSONP) de prise en charge tooan opération ou une API tooallow entre domaines appelle à partir de clients basés sur navigateur JavaScript.  
  
##  <a name="AllowCrossDomainCalls"></a> Allow cross-domain calls  
 Hello d’utilisation `cross-domain` hello toomake de stratégie API accessible à partir de clients basés sur navigateur Adobe Flash et Microsoft Silverlight.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|inter-domaines|Élément racine. Éléments enfants doivent être conformes toohello [spécification de fichier de stratégie inter-domaines Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).|Oui|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** globale (globale)  
  
##  <a name="CORS"></a> CORS  
 Hello `cors` stratégie ajoute le partage de ressources cross-origin (CORS) prend en charge les tooan opération ou une API tooallow entre domaines appelle à partir de clients de navigateur.  
  
 CORS permet à un navigateur et un serveur toointeract et déterminer ou non de requêtes tooallow spécifique cross-origine (c'est-à-dire des appels xmlhttprequests établis à partir de JavaScript sur une page web des domaines tooother). Cette stratégie offre plus de flexibilité que de simplement autoriser les demandes de même origine, mais elle est plus sûre que d'autoriser toutes les demandes cross-origin.  
  
### <a name="policy-statement"></a>Déclaration de stratégie  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a>Exemple  
 Cet exemple montre comment les demandes avant le vol toosupport, telles que celles comportant des en-têtes personnalisés ou de méthodes autres que GET et POST. les en-têtes personnalisés toosupport et autres verbes HTTP, utilisez hello `allowed-methods` et `allowed-headers` sections comme indiqué dans hello l’exemple suivant.  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|cors|Élément racine.|Oui|N/A|  
|allowed-origins|Contient `origin` éléments qui décrivent les hello autorisé origines pour les demandes inter-domaines. `allowed-origins`peut contenir un seul `origin` élément spécifie `*` tooallow toute origine, ou une ou plusieurs `origin` éléments contenant un URI.|Oui|N/A|  
|origin|Hello valeur peut être `*` tooallow toutes les origines, ou un URI qui spécifie une origine unique. Hello URI doit inclure un schéma, hôte et port.|Oui|Si le port de hello est omis dans un URI, le port 80 est utilisé pour HTTP et utilise le port 443 pour HTTPS.|  
|allowed-methods|Cet élément est requis si les méthodes autres que GET ou POST sont autorisées. Contient des `method` des éléments qui spécifient hello pris en charge les verbes HTTP.|Non|Si cette section n’est pas présente, les méthodes GET et POST sont prises en charge.|  
|statique|Spécifie un verbe HTTP.|Au moins un `method` élément est requis si hello `allowed-methods` section est présente.|N/A|  
|allowed-headers|Cet élément contient `header` éléments spécifiant les noms des en-têtes hello qui peuvent être inclus dans la demande hello.|Non|N/A|  
|expose-headers|Cet élément contient `header` éléments spécifiant les noms des en-têtes hello qui seront accessibles par le client de hello.|Non|N/A|  
|en-tête|Spécifie un nom d’en-tête.|Au moins un `header` élément est requis dans `allowed-headers` ou `expose-headers` si hello section est présente.|N/A|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|allow-credentials|Hello `Access-Control-Allow-Credentials` en-tête dans la réponse préliminaire de hello sera toohello de valeur de cet attribut et affectent les informations d’identification de toosubmit de capacité du client hello dans les demandes inter-domaines.|Non|false|  
|preflight-result-max-age|Hello `Access-Control-Max-Age` en-tête dans la réponse préliminaire de hello sera toohello de valeur de cet attribut et affectent la réponse de l’agent de l’utilisateur hello capacité toocache préliminaire.|Non|0|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** API, operation (API, opération)  
  
##  <a name="JSONP"></a> JSONP  
 Hello `jsonp` ajoute la stratégie avec remplissage opération tooan de support (JSONP) ou une API tooallow les appels interdomaines à partir des clients basés sur navigateur JavaScript. JSONP est une méthode utilisée dans les données de toorequest programmes JavaScript à partir d’un serveur dans un domaine différent. JSONP contourne la limitation de hello imposée par la plupart des navigateurs web où les pages d’accès aux tooweb doivent être Bonjour même domaine.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 Si vous appelez la méthode hello sans paramètre de rappel hello ? cb = XXX, elle renvoie un code JSON brut (sans un wrapper d’appel de fonction).  
  
 Si vous ajoutez le paramètre de rappel hello `?cb=XXX` il retournera un résultat JSONP, en encapsulant les résultats JSON d’origine hello autour de fonction de rappel hello comme`XYZ('<json result goes here>');`  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|jsonp|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|callback-parameter-name|Hello appel de fonction JavaScript inter-domaines préfixé avec le nom de domaine complet de hello où hello fonction réside.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** outbound (sortant)  
  
-   **Étendues de la stratégie :** global, product, API, operation (global, produit, API, opération)  
  
## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).  