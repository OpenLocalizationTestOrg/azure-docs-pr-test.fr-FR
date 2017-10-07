---
title: "stratégies de restriction de l’accès de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les stratégies de restriction hello accès disponibles pour une utilisation dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a>Stratégies de restriction des accès de la Gestion des API
Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API. Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AccessRestrictionPolicies"></a> Stratégies de restriction des accès  
  
-   [Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) : applique l’existence et/ou la valeur d’un en-tête HTTP.  
  
-   [Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par abonnement.  
  
-   [Limit call rate by key](#LimitCallRateByKey) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par clé.  
  
-   [Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtre (autorise/rejette) les appels de certaines adresses IP spécifiques et/ou de certaines plages d’adresses.  
  
-   [Définir le quota d’utilisation par abonnement](api-management-access-restriction-policies.md#SetUsageQuota) -vous permet de tooenforce un quota renouvelable ou à durée de vie appel volume et/ou de la bande passante, sur une base par abonnement.  
  
-   [Définir le quota d’utilisation par clé](#SetUsageQuotaByKey) -vous permet de tooenforce un quota renouvelable ou à durée de vie appel volume et/ou de la bande passante, sur une base par clé.  
  
-   [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) : applique l’existence et la validité d’un JWT extrait d’un en-tête HTTP ou d’un paramètre de requête spécifié.  
  
##  <a name="CheckHTTPHeader"></a> Check HTTP header  
 Hello d’utilisation `check-header` tooenforce stratégie qu’une demande ait un en-tête HTTP. Vous pouvez éventuellement vérifier toosee si l’en-tête hello a une valeur spécifique ou une vérification pour une plage de valeurs autorisées. Si hello vérification échoue, stratégie de hello termine le traitement de la demande et renvoie hello erreur et le code message d’état HTTP spécifié par la stratégie de hello.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|check-header|Élément racine.|Oui|  
|value|Valeur autorisée de l’en-tête HTTP. Lorsque plusieurs éléments de valeur sont spécifiées, la vérification de hello est considérée comme un succès si l’une des valeurs de hello est une correspondance.|Non|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|failed-check-error-message|Erreur tooreturn de message dans le corps de la réponse hello HTTP si l’en-tête de hello n’existe pas ou a une valeur non valide. Les éventuels caractères spéciaux de ce message doivent être correctement placés dans une séquence d’échappement.|Oui|N/A|  
|failed-check-httpcode|État HTTP code tooreturn si l’en-tête de hello n’existe pas ou a une valeur non valide.|Oui|N/A|  
|header-name|nom Hello Hello toocheck d’en-tête HTTP.|Oui|N/A|  
|ignore-case|Peut être défini tooTrue ou False. Si le cas de tooTrue set est ignoré lorsque la valeur d’en-tête hello est comparée à ensemble hello des valeurs acceptables.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="LimitCallRate"></a> Limit call rate by subscription  
 Hello `rate-limit` stratégie empêche l’utilisation de l’API pics sur une base par abonnement en limitant hello numéro d’appel de tooa taux spécifié par une période de temps. Lorsque cette stratégie est déclenchée appelant de hello reçoit un `429 Too Many Requests` code d’état de réponse.  
  
> [!IMPORTANT]
>  Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.  
>   
>  [Expressions de stratégie](api-management-policy-expressions.md) ne peut pas être utilisé dans un des attributs de stratégie hello pour cette stratégie.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|set-limit|Élément racine.|Oui|  
|api|Ajoutez un ou plusieurs de ces éléments de tooimpose une limite de taux d’appels sur les API au sein du produit de hello. Les limites de débit d’appels au niveau du produit et de l’API s’appliquent indépendamment les unes des autres.|Non|  
|operation|Ajouter un ou plusieurs de ces éléments de tooimpose une limite de taux d’appels sur les opérations à l’intérieur d’une API. Les limites de débit d’appels au niveau du produit, de l’API et de l’opération s’appliquent indépendamment les unes des autres.|Non|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|name|nom de Hello Hello API pour lesquelles limite de taux tooapply hello.|Oui|N/A|  
|calls|Hello nombre maximal d’appels autorisés au cours de l’intervalle de temps hello spécifié dans hello `renewal-period`.|Oui|N/A|  
|renewal-period|Hello laps de temps en secondes après lequel hello quota est réinitialisé.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** product  
  
##  <a name="LimitCallRateByKey"></a> Limite de débit d’appels par clé  
 Hello `rate-limit-by-key` stratégie empêche l’utilisation de l’API pics sur une base par clé en limitant hello numéro d’appel de tooa taux spécifié par une période de temps. clé de Hello peut avoir une valeur de chaîne arbitraire et est généralement fourni à l’aide d’une expression de stratégie. Condition d’incrément facultatif peut être ajoutée toospecify les requêtes qui doivent être comptés dans nombre maximal de hello. Lorsque cette stratégie est déclenchée appelant de hello reçoit un `429 Too Many Requests` code d’état de réponse.  
  
 Pour plus d’informations et d’exemples sur cette stratégie, consultez la page [Limitation avancée des demandes dans la Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a>Exemple  
 Dans l’exemple suivant de hello, limite de taux hello est indexé par adresse IP de l’appelant hello.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|set-limit|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|calls|Hello nombre maximal d’appels autorisés au cours de l’intervalle de temps hello spécifié dans hello `renewal-period`.|Oui|N/A|  
|counter-key|Hello toouse clé pour la stratégie de limite de taux de hello.|Oui|N/A|  
|increment-condition|expression booléenne de Hello spécifiant si la demande de hello doit être comptée vers le quota de hello (`true`).|Non|N/A|  
|renewal-period|Hello laps de temps en secondes après lequel hello quota est réinitialisé.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="RestrictCallerIPs"></a> Restrict caller IPs  
 Hello `ip-filter` stratégie filtre (autorise/refuse) des appels à partir de plages d’adresses et/ou des adresses IP spécifiques.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|ip-filter|Élément racine.|Oui|  
|address|Spécifie une adresse IP unique sur le toofilter.|Au moins un élément `address` ou `address-range` est requis.|  
|address-range from="address" to="address"|Spécifie une plage d’adresses IP sur quel toofilter.|Au moins un élément `address` ou `address-range` est requis.|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|address-range from="address" to="address"|Une plage d’adresse IP, adresses tooallow ou refuser l’accès.|Obligatoire lorsque hello `address-range` élément est utilisé.|N/A|  
|ip-filter action="allow &#124; forbid"|Spécifie si les appels doivent être autorisés ou non pour hello spécifié adresses IP et plages.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="SetUsageQuota"></a> Set usage quota by subscription  
 Hello `quota` stratégie applique un quota renouvelable ou durée de vie appel volume et/ou de la bande passante, sur une base par abonnement.  
  
> [!IMPORTANT]
>  Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.  
>   
>  [Expressions de stratégie](api-management-policy-expressions.md) ne peut pas être utilisé dans un des attributs de stratégie hello pour cette stratégie.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|quota|Élément racine.|Oui|  
|api|Ajoutez un ou plusieurs de ces éléments de tooimpose un quota sur les API au sein du produit de hello. Les quotas au niveau du produit et de l’API s’appliquent indépendamment les uns des autres.|Non|  
|operation|Ajouter un ou plusieurs de ces éléments de tooimpose un quota sur les opérations à l’intérieur d’une API. Les quotas au niveau du produit, de l’API et de l’opération s’appliquent indépendamment les uns des autres.|Non|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|name|nom de Hello de hello API ou l’opération pour le hello quota s’applique.|Oui|N/A|  
|bandwidth|Hello nombre total maximal de kilo-octets autorisé durant la période hello spécifié dans hello `renewal-period`.|Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.|N/A|  
|calls|Hello nombre maximal d’appels autorisés au cours de l’intervalle de temps hello spécifié dans hello `renewal-period`.|Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.|N/A|  
|renewal-period|Hello laps de temps en secondes après lequel hello quota est réinitialisé.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** product  
  
##  <a name="SetUsageQuotaByKey"></a> Set usage quota by key  
 Hello `quota-by-key` stratégie applique un quota renouvelable ou durée de vie appel volume et/ou de la bande passante, sur une base par clé. clé de Hello peut avoir une valeur de chaîne arbitraire et est généralement fourni à l’aide d’une expression de stratégie. Condition d’incrément facultatif peut être ajoutée toospecify quelles demandes doivent être comptabilisées dans le quota de hello.  
  
 Pour plus d’informations et d’exemples sur cette stratégie, consultez la page [Limitation avancée des demandes dans la Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.  
>   
>  [Expressions de stratégie](api-management-policy-expressions.md) ne peut pas être utilisé dans un des attributs de stratégie hello pour cette stratégie.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>Exemple  
 Dans l’exemple suivant de hello, quota de hello est indexé par adresse IP de l’appelant hello.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|quota|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|bandwidth|Hello nombre total maximal de kilo-octets autorisé durant la période hello spécifié dans hello `renewal-period`.|Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.|N/A|  
|calls|Hello nombre maximal d’appels autorisés au cours de l’intervalle de temps hello spécifié dans hello `renewal-period`.|Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.|N/A|  
|counter-key|Hello toouse clé pour la stratégie de quota hello.|Oui|N/A|  
|increment-condition|expression booléenne de Hello spécifiant si la demande de hello doit être comptée vers le quota de hello (`true`)|Non|N/A|  
|renewal-period|Hello laps de temps en secondes après lequel hello quota est réinitialisé.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="ValidateJWT"></a> Validate JWT  
 Hello `validate-jwt` stratégie applique l’existence et la validité d’un jeton JWT extrait de soit un en-tête HTTP ou un paramètre de requête spécifié.  
  
> [!IMPORTANT]
>  Hello `validate-jwt` stratégie nécessite que hello `exp` revendication inscrite est inclus dans le jeton JWT de hello, sauf si `require-expiration-time` attribut est spécifié et possède trop`false`.  
> Hello `validate-jwt` stratégie prend en charge les algorithmes de signature HS256 et RS256. Pour HS256 clé de hello doit être fourni inline dans la stratégie hello sous forme de codé en base64 hello. Pour RS256 hello fait clé toobe fournir via un point de terminaison de configuration Open ID.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a>Exemples  
  
#### <a name="azure-mobile-services-token-validation"></a>Validation d’un jeton Azure Mobile Services  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a>Validation d’un jeton Azure Active Directory  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a>Validation d’un jeton Azure Active Directory B2C  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a>Autoriser les toooperations d’accès basées sur les revendications de jeton  
 Cet exemple montre comment toouse hello [valider les jetons Web JSON](api-management-access-restriction-policies.md#ValidateJWT) stratégie toopre-autoriser toooperations d’accès basées sur les revendications de jeton. Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too13:50. Avance rapide too15:00 les stratégies de hello toosee configurées dans l’éditeur de stratégie hello et puis too18:50 pour une démonstration de l’appel d’une opération à partir du portail des développeurs hello avec et sans hello requis jeton d’autorisation.  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|validate-jwt|Élément racine.|Oui|  
|audiences|Contient une liste de revendications d’audience acceptables qui peuvent être présents sur le jeton de hello. Si plusieurs valeurs d’audience sont présentes, chacune est tentée jusqu’à ce que toutes soient épuisées (auquel cas la validation échoue) ou que l’une d’elles réussisse. Au moins une audience doit être spécifiée.|Non|  
|issuer-signing-keys|Une liste de codée en Base64 de sécurité clés utilisées toovalidate signé des jetons. Si plusieurs clés de sécurité sont présentes, chacune est tentée jusqu’à ce que toutes soient épuisées (auquel cas la validation échoue) ou que l’une d’elles réussisse (utile pour la substitution de jeton). Éléments clés ont une option `id` toomatch attribut utilisé par rapport à `kid` de revendication.|Non|  
|issuers|Une liste des principaux acceptables qui a émis le jeton de hello. Si plusieurs valeurs d’émetteur sont présentes, chacune est tentée jusqu’à ce que toutes soient épuisées (auquel cas la validation échoue) ou que l’une d’elles réussisse.|Non|  
|openid-config|élément Hello utilisée pour spécifier une extrémité de configuration Open ID conformes à partir de laquelle des clés et l’émetteur de signature peut être obtenue.|Non|  
|required-claims|Contient une liste de toobe attendues des revendications présente sur le jeton de hello pour qu’il toobe considéré comme valide. Hello lorsque `match` attribut est défini trop`all` chaque valeur de revendication dans la stratégie de hello doit être présent dans le jeton de hello pour toosucceed de validation. Hello lorsque `match` attribut est défini trop`any` au moins une revendication doit être présente dans le jeton de hello pour toosucceed de validation.|Non|  
|zumo-master-key|Clé principale pour les jetons émis par Azure Mobile Services.|Non|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|clock-skew|Intervalle de temps. Fournit certains manœuvre petite en cas de revendication d’expiration du jeton hello est présente dans le jeton de hello et est en cours de hello au-delà de date / heure.|Non|0 seconde|  
|failed-validation-error-message|Erreur tooreturn de message dans les corps de réponse HTTP de hello si hello JSON n’est pas validé. Les éventuels caractères spéciaux de ce message doivent être correctement placés dans une séquence d’échappement.|Non|Le message d’erreur par défaut dépend du problème de validation, par exemple « JWT absent ».|  
|failed-validation-httpcode|État HTTP code tooreturn si hello JSON ne sont pas validées.|Non|401|  
|header-name|nom Hello d’en-tête hello HTTP contenant hello jeton.|Soit `header-name`, soit `query-paremeter-name` doit être spécifié, mais pas les deux.|N/A|  
|id|Hello `id` attribut sur hello `key` élément vous permet de chaîne hello toospecify qui sera comparée à `kid` toofind de jeton (le cas échéant) hello out hello approprié toouse clés pour la validation des signatures de revendication.|Non|N/A|  
|match|Hello `match` attribut sur hello `claim` élément indique si chaque valeur de revendication dans la stratégie de hello doit être présent dans le jeton de hello pour toosucceed de validation. Les valeurs possibles sont les suivantes :<br /><br /> -                          `all`-chaque valeur de revendication dans la stratégie de hello doit être présent dans le jeton de hello pour toosucceed de validation.<br /><br /> -                          `any`-valeur d’au moins une revendication doit être présent dans le jeton de hello pour toosucceed de validation.|Non|tout|  
|query-paremeter-name|nom Hello hello hello du paramètre de requête contenant le jeton de hello.|Soit `header-name`, soit `query-paremeter-name` doit être spécifié, mais pas les deux.|N/A|  
|require-expiration-time|Booléen. Spécifie si une revendication d’expiration est requise dans le jeton de hello.|Non|true|
|require-scheme|Hello nom du schéma de jeton hello, par exemple « Support ». Lorsque cet attribut est défini, stratégie de hello garantit que spécifié de schéma est présent dans la valeur de l’en-tête d’autorisation de hello.|Non|N/A|
|require-signed-tokens|Booléen. Spécifie si un jeton est requis toobe signé.|Non|true|  
|url|URL du point de terminaison de configuration Open ID à partir de laquelle les métadonnées de configuration Open ID peuvent être récupérées. Pour Azure Active Directory, utilisez hello suivant URL : `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` en remplaçant votre nom de client de répertoire, par exemple, `contoso.onmicrosoft.com`.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).  
