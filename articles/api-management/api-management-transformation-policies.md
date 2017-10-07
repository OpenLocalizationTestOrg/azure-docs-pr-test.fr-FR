---
title: "stratégies de transformation de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les stratégies de transformation hello disponibles pour une utilisation dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a>Stratégies de transformation de la Gestion des API
Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API. Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="TransformationPolicies"></a> Stratégies de transformation  
  
-   [Convertir en JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - convertit demande ou le corps de la réponse de JSON tooXML.  
  
-   [Convertir XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - convertit demande ou le corps de la réponse à partir de XML tooJSON.  
  
-   [Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) : recherche une sous-chaîne de demande ou de réponse et la remplace par une autre sous-chaîne.  
  
-   [Masquer des URL dans le contenu](api-management-transformation-policies.md#MaskURLSContent) -réécrit (masque) des liens dans la réponse de hello corps afin qu’ils pointent toohello le lien équivalent via une passerelle de hello.  
  
-   [Définir le service principal](api-management-transformation-policies.md#SetBackendService) -modifie le service principal de hello pour une demande entrante.  
  
-   [Définir le corps](api-management-transformation-policies.md#SetBody) -définit le corps du message hello pour les demandes entrantes et sortantes.  
  
-   [En-tête HTTP](api-management-transformation-policies.md#SetHTTPheader) - assigne une réponse existante de valeur tooan et/ou d’un en-tête de demande ou ajoute un nouvel en-tête de réponse et/ou de demande.  
  
-   [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) : ajoute, supprime un paramètre de chaîne de requête de la demande ou le remplace par une autre valeur.  
  
-   [Réécriture d’URL](api-management-transformation-policies.md#RewriteURL) -convertit une URL de demande à partir de sa forme toohello de formulaire public attendu par le service web hello.  
  
-   [Transformer du code XML à l’aide d’une transformation XSLT](api-management-transformation-policies.md#XSLTransform) -applique un tooXML de la transformation XSL dans le corps de demande ou réponse hello.  
  
##  <a name="ConvertJSONtoXML"></a>Convertir en JSON tooXML  
 Hello `json-to-xml` stratégie convertit un corps de demande ou de réponse de JSON tooXML.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|json-to-xml|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|apply|attribut de Hello doit être définie tooone Hello valeurs suivantes.<br /><br /> -   always : toujours appliquer la conversion.<br />-   content-type-json : ne convertir que si l’en-tête de réponse Content-Type indique la présence de JSON.|Oui|N/A|  
|consider-accept-header|attribut de Hello doit être définie tooone Hello valeurs suivantes.<br /><br /> -   true : appliquer la conversion si le format JSON est demandé dans l’en-tête d’acceptation de la demande.<br />-   false : toujours appliquer la conversion.|Non|true|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, on-error  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="ConvertXMLtoJSON"></a>Convertir XML tooJSON  
 Hello `xml-to-json` stratégie convertit un corps de demande ou de réponse XML tooJSON. Cette stratégie peut être utilisé toomodernize API basé sur les services web principaux uniquement XML.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|xml-to-json|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|kind|attribut de Hello doit être définie tooone Hello valeurs suivantes.<br /><br /> -javascript friendly : hello converti JSON a un tooJavaScript convivial aux développeurs.<br />-direct - hello JSON converti reflète la structure de hello XML document d’origine.|Oui|N/A|  
|apply|attribut de Hello doit être définie tooone Hello valeurs suivantes.<br /><br /> -   always : toujours convertir.<br />-   content-type-xml : ne convertir que si l’en-tête de réponse Content-Type indique la présence de XML.|Oui|N/A|  
|consider-accept-header|attribut de Hello doit être définie tooone Hello valeurs suivantes.<br /><br /> -   true : appliquer la conversion si le format XML est demandé dans l’en-tête d’acceptation de la demande.<br />-   false : toujours appliquer la conversion.|Non|true|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, on-error  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="Findandreplacestringinbody"></a> Find and replace string in body  
 Hello `find-and-replace` stratégie recherche une sous-chaîne de demande ou de réponse et le remplace par une autre sous-chaîne.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|find-and-replace|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|from|toosearch de chaîne Hello pour.|Oui|N/A|  
|to|chaîne de remplacement Hello. Spécifiez une remplacement chaîne tooremove hello recherche chaîne de longueur zéro.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="MaskURLSContent"></a> Mask URLs in content  
 Hello `redirect-content-urls` stratégie réécrit (masque) des liens dans le corps de la réponse hello afin qu’ils pointent toohello le lien équivalent via une passerelle de hello. Utilisez-les dans toomake des liens des corps de réponse hello section sortante toore-écriture toohello de point de passerelle. Utilisation de hello entrants de section d’un effet opposé.  
  
> [!NOTE]
>  Cette stratégie ne change pas les valeurs d’en-têtes, notamment des en-têtes `Location`. les valeurs d’en-tête toochange, utilisez hello [-en-tête](api-management-transformation-policies.md#SetHTTPheader) stratégie.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|redirect-content-urls|Élément racine.|Oui|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="SetBackendService"></a> Set backend service  
 Hello d’utilisation `set-backend-service` stratégie tooredirect un entrant demande principal différent de tooa que celui spécifié dans les paramètres de hello API pour cette opération hello. Cette stratégie modifie hello URL du service principal de toohello demande entrants hello celui spécifié dans la stratégie de hello.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
Bonjour de cet exemple stratégie de service principal définie achemine les demandes en fonction de la valeur de la version hello passé hello requête chaîne tooa service principal différent hello hello spécifié dans une API.
  
Initialement hello URL du service principal est dérivée de paramètres de l’API hello. Hello par conséquent, les URL de demande `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` devient `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` où `http://contoso.com/api/10.4/` est l’URL du service principal hello spécifié dans les paramètres de l’API de hello.  
  
Hello lorsque [< choisissez\> ](api-management-advanced-policies.md#choose) l’instruction de stratégie est appliquée hello URL du service principal peut changer à nouveau trop`http://contoso.com/api/8.2` ou `http://contoso.com/api/9.1`, selon la valeur hello hello version demande du paramètre de requête. Par exemple, si hello valeur est `"2013-15"` hello dernière demande URL devient `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.  
  
Si davantage la transformation de requête de hello est souhaitée, d’autres [stratégies de Transformation](api-management-transformation-policies.md#TransformationPolicies) peut être utilisé. Par exemple, tooremove hello version requête routé maintenant que hello demande est en cours de paramètre hello tooa version principales, [définir le paramètre de chaîne de requête](api-management-transformation-policies.md#SetQueryStringParameter) stratégie peut être l’attribut de version désormais redondant hello tooremove utilisé.  
  
### <a name="example"></a>Exemple  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
Dans cet exemple hello stratégie itinéraires hello demande tooa service fabric service principal, à l’aide de la chaîne de requête userId hello en tant que clé de partition hello et à l’aide de hello réplica principal de la partition de hello.  

### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|set-backend-service|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|base-url|Nouvelle URL de base du service principal.|Non|N/A|  
|id de principal|Identificateur de tooroute de back-end hello pour.|Non|N/A|  
|clé de partition SF|S’applique seulement lorsque hello principal est un service Service Fabric et qu’il est spécifié à l’aide de 'id principal'. Utilisé tooresolve une partition spécifique à partir du service de résolution de noms hello.|Non|N/A|  
|type de réplica SF|S’applique seulement lorsque hello principal est un service Service Fabric et qu’il est spécifié à l’aide de 'id principal'. Contrôle si la demande de hello doit devenir toohello un réplica principal ou secondaire d’une partition. |Non|N/A|    
|condition de résolution SF|Applicable uniquement lorsque hello principal est un service Service Fabric. Identifiant de condition Si hello appelez principal de l’ensemble fibre optique tooService a toobe répété avec la nouvelle résolution.|Non|N/A|    
|nom d’instance de service DF|Applicable uniquement lorsque hello principal est un service Service Fabric. Permet des instances de service toochange lors de l’exécution. |Non|N/A |    

### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, backend  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="SetBody"></a> Set body  
 Hello d’utilisation `set-body` corps du message stratégie tooset hello pour les demandes entrantes et sortantes. tooaccess hello corps de message que vous pouvez utiliser hello `context.Request.Body` propriété ou hello `context.Response.Body`, selon que la stratégie de hello est Bonjour section entrante ou sortante.  
  
> [!IMPORTANT]
>  Notez que, par défaut lorsque vous accédez à hello du corps du message à l’aide `context.Request.Body` ou `context.Response.Body`, message d’origine de type hello corps est perdu et doit être défini en renvoyant le corps de hello dans expression de hello. corps de hello toopreserve contenu, définissez hello `preserveContent` paramètre trop`true` lors de l’accès de message de type hello. Si `preserveContent` est défini trop`true` et un corps différent est renvoyé par l’expression de hello, hello corps est utilisé.  
>   
>  Veuillez noter hello suivant Considérations lors de l’utilisation de hello `set-body` stratégie.  
>   
>  -   Si vous utilisez hello `set-body` stratégie tooreturn un corps de nouveau ou mis à jour que vous n’avez pas besoin de tooset `preserveContent` trop`true` parce que vous fournissez explicitement contenu du corps de la nouvelle hello.  
> -   En conservant le contenu d’une réponse hello dans pipeline entrant de hello n’a aucune signification, car il n’existe encore aucune réponse.  
> -   En conservant le contenu d’une demande de hello dans le pipeline de sortie hello n’a aucune signification car hello demande a déjà été envoyée toohello principal à ce stade.  
> -   Si cette stratégie est utilisée en l’absence de corps de message, par exemple dans une requête GET inbound, une exception est levée.  
  
 Pour plus d’informations, consultez hello `context.Request.Body`, `context.Response.Body`et hello `IMessage` sections Bonjour [variable contextuelle](api-management-policy-expressions.md#ContextVariables) table.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>Exemples  
  
#### <a name="literal-text-example"></a>Exemple de texte littéral  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a>Exemple d’accès au corps hello sous forme de chaîne. Notez que nous allons conserver les corps de la demande d’origine hello afin que nous pouvons accéder à plus tard dans le pipeline de hello.
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a>Exemple d’accès au corps hello en tant que JObject. Notez qu’étant donné que nous ne sommes pas réservation hello d’origine corps de la demande, accès plus loin dans le pipeline de hello entraîne une exception.  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a>Filtrer la réponse en fonction du produit  
 Cet exemple montre comment tooperform le filtrage de contenu en supprimant des éléments de données à partir de la réponse de hello reçu hello principal service lors de l’utilisation de hello `Starter` produit. Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too34:30. Démarrer à 31:50 toosee une vue d’ensemble de [hello API de prévision ciel foncé](https://developer.forecast.io/) utilisée pour cette démonstration.  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a>Utilisation de modèles Liquid avec Set body 
Hello `set-body` stratégie peut être configurée toouse hello [liquide](https://shopify.github.io/liquid/basics/introduction/) corps de création de modèles language tootransfom hello d’une demande ou réponse. Cela peut être très efficace si vous avez besoin de format de hello toocompletely la mise en forme du message.

> [!IMPORTANT]
> Hello d’implémentation de liquide utilisé Bonjour `set-body` stratégie est configurée en « mode C# ». Cela est particulièrement important lors d’opérations telles que le filtrage. Par exemple, à l’aide d’un filtre de date nécessite l’utilisation de hello de Pascal casse et C# date mise en forme, par exemple :
>
> {{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}

> [!IMPORTANT]
> Dans l’ordre toocorrectly bind tooan corps de XML à l’aide du modèle de liquide hello, utilisez un `set-header` stratégie tooset Content-Type tooeither application/xml, texte/xml (ou n’importe quel type se terminant par + xml) ; pour un corps JSON, il doit être application/json, texte/json (ou fin de n’importe quel type avec + json).

#### <a name="convert-json-toosoap-using-a-liquid-template"></a>Convertir tooSOAP JSON à l’aide d’un modèle liquide
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a>Transformation de JSON à l’aide d’un modèle Liquid
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|set-body|Élément racine. Contient hello corps du texte ou une expression qui renvoie un corps.|Oui|  

### <a name="properties"></a>Propriétés  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|template|Mode de création de modèles toochange utilisé hello hello ensemble corps de la stratégie s’exécutera dans. Valeur de hello uniquement pris en charge actuellement est :<br /><br />hello - liquide - définir une stratégie corps utilisera le moteur de création de modèles liquide hello |Non|liquid|  

Pour accéder aux informations sur la demande de hello et de réponse, hello liquide peut liez par modèle objet de contexte tooa avec hello propriétés suivantes : <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="SetHTTPheader"></a> Set HTTP header  
 Hello `set-header` stratégie affecte une réponse existante de valeur tooan et/ou d’un en-tête de demande ou ajoute un nouvel en-tête de réponse et/ou de demande.  
  
 Insère une liste d'en-têtes HTTP dans un message HTTP. Lorsqu’elle est placée dans un pipeline entrant, cette stratégie définit les en-têtes HTTP hello pour demande hello transmise service cible de toohello. Lorsqu’elle est placée dans un pipeline sortant, cette stratégie définit les en-têtes HTTP hello pour réponse hello envoyée client de la passerelle toohello.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>Exemples  
  
#### <a name="example"></a>Exemple  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Transférer le service principal de contexte informations toohello  
 Cet exemple montre comment stratégie tooapply à hello API niveau le service principal toohello toosupply contexte plus d’informations. Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too10:30. À 12:10, il existe une démonstration de l’appel à une opération dans le portail des développeurs hello où vous pouvez consulter la stratégie hello au travail.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 Pour plus d’informations, consultez les pages [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|set-header|Élément racine.|Oui|  
|value|Spécifie la valeur hello hello en-tête toobe ensemble. Pour plusieurs en-têtes hello avec le même nom, ajoutez des `value` éléments.|Oui|  
  
### <a name="properties"></a>Propriétés  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|exists-action|Spécifie quelles tootake action lorsque hello en-tête est déjà spécifié. Cet attribut doit avoir une des valeurs suivantes de hello.<br /><br /> -remplacer - valeur de hello remplace d’en-tête existant de hello.<br />-ignorer - ne remplace pas la valeur d’en-tête hello existant.<br />-Ajouter - ajoute la valeur d’en-tête existant hello valeur toohello.<br />-Supprimer - supprime les en-tête de hello de demande de hello.<br /><br /> Lorsque la valeur trop`override` l’inscription de plusieurs entrées avec hello même nom que les résultats dans l’en-tête de hello en cours en fonction tooall entrées (qui apparaissent plusieurs fois) ; seules les valeurs inscrites seront définies dans le résultat de hello.|Non|override|  
|name|Spécifie le nom du jeu de toobe en-tête hello.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="SetQueryStringParameter"></a> Set query string parameter  
 Hello `set-query-parameter` ajoute de la stratégie, remplace la valeur, ou paramètre de chaîne de requête de demande de suppressions. Peut être utilisé toopass paramètres de requête attendus par le service principal hello, qui sont facultatifs ou toujours absents dans la demande de hello.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>Exemples  
  
#### <a name="example"></a>Exemple  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Transférer le service principal de contexte informations toohello  
 Cet exemple montre comment stratégie tooapply à hello API niveau le service principal toohello toosupply contexte plus d’informations. Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too10:30. À 12:10, il existe une démonstration de l’appel à une opération dans le portail des développeurs hello où vous pouvez consulter la stratégie hello au travail.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 Pour plus d’informations, consultez les pages [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|set-query-parameter|Élément racine.|Oui|  
|value|Spécifie la valeur hello hello paramètre toobe du jeu de requête. Plusieurs paramètres de requête par hello même nom, ajoutez des `value` éléments.|Oui|  
  
### <a name="properties"></a>Propriétés  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|exists-action|Spécifie quelles tootake action lorsque le paramètre de requête hello est déjà spécifié. Cet attribut doit avoir une des valeurs suivantes de hello.<br /><br /> -remplacer - valeur hello remplace paramètre existant hello.<br />-ignorer - ne remplace pas la valeur de paramètre de requête existant hello.<br />-Ajouter - ajoute la valeur du paramètre requête existant hello valeur toohello.<br />-Supprimer - supprime le paramètre de requête hello à partir de la demande de hello.<br /><br /> Lorsque la valeur trop`override` l’inscription de plusieurs entrées avec hello même nom que les résultats dans le paramètre de requête hello en cours en fonction tooall entrées (qui apparaissent plusieurs fois) ; seules les valeurs inscrites seront définies dans le résultat de hello.|Non|override|  
|name|Spécifie le nom du jeu de toobe de paramètre de requête hello.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, backend  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
##  <a name="RewriteURL"></a> Rewrite URL  
 Hello `rewrite-uri` stratégie convertit une URL de demande à partir de sa forme toohello de formulaire public attendu par le service web hello, comme illustré dans hello l’exemple suivant.  
  
-   URL publique : `http://api.example.com/storenumber/ordernumber`  
  
-   URL de la demande : `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`  
  
 Cette stratégie peut être utilisée lorsqu’une URL de l’opérateur humaine et/ou le nom convivial de l’Explorateur doit être transformée en format d’URL hello attendu par le service web hello. Cette stratégie ne doit toobe appliqué lors de l’exposition d’un autre format d’URL, tels que les URL propre, URL RESTful, une URL conviviale ou les URL compatibles avec les moteurs de recherche qui sont des URL purement structurelles qui ne contient pas une chaîne de requête et à la place contenir uniquement hello chemin d’accès de hello ressources (après le schéma de hello et autorité de hello). C'est souvent le cas pour des raisons d'esthétique, de simplicité d'utilisation ou bien pour l'optimisation des résultats de recherche (SEO).  
  
> [!NOTE]
>  Vous pouvez uniquement ajouter des paramètres de chaîne de requête à l’aide de la stratégie de hello. Vous ne pouvez pas ajouter de paramètres de chemin d’accès de modèle supplémentaire dans hello réécriture d’URL.  

### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|rewrite-uri|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|-------------|  
|template|URL du service web réel Hello avec les paramètres de chaîne de requête. Lorsque vous utilisez des expressions, toute valeur de hello doit être une expression.|Oui|N/A|  
|copy-unmatched-params|Spécifie si les paramètres de requête dans la demande entrante de hello ne figure pas dans le modèle d’URL d’origine hello sont ajoutés les URL toohello définie par hello rédigez à nouveau modèle|Non|true|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** product, API, operation  
  
##  <a name="XSLTransform"></a> Transform XML using an XSLT  
 Hello `Transform XML using an XSLT` stratégie s’applique à une tooXML de la transformation XSL dans le corps de demande ou réponse hello.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|xsl-transform|Élément racine.|Oui|  
|paramètre|Variables utilisées toodefine utilisées dans une transformation hello|Non|  
|xsl:stylesheet|Élément feuille de style racine. Tous les éléments et attributs définis dans suivent standard de hello [spécification XSLT](http://www.w3.org/TR/xslt)|Oui|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound  
  
-   **Étendues de la stratégie :** global, product, API, operation  
  
## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).  
