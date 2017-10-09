---
title: "expressions de stratégie de gestion des API aaaAzure | Documents Microsoft"
description: "Découvrez les expressions de stratégie dans la Gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: ea160028-fc04-4782-aa26-4b8329df3448
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 79da0d6ca3963307ec811a33aaac3d63a7abd97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policy-expressions"></a>Expressions de stratégie de la Gestion des API
La syntaxe des expressions de stratégie est C# 6.0. Chaque expression a toohello d’accès fourni implicitement [contexte](api-management-policy-expressions.md#ContextVariables) variable et une liste autorisée [sous-ensemble](api-management-policy-expressions.md#CLRTypes) de types .NET Framework.  
  
> [!NOTE]
>  Pour plus d’informations sur les expressions de stratégie, consultez hello [Expressions de stratégie](https://azure.microsoft.com/documentation/videos/policy-expressions-in-azure-api-management/) vidéo.  
>   
>  Pour une démonstration de la configuration des stratégies avec des expressions de stratégie, consultez la page [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, épisode 177 : Plus de fonctionnalités de la Gestion des API avec Vlad Vinogradsky). Cette vidéo contient hello suivant démonstrations d’expression de stratégie.  
>   
>  -   10:30 - voir la stratégie tooapply à hello API de niveau service toosupply contexte informations toohello principal à l’aide de hello [définir le paramètre de chaîne de requête](api-management-transformation-policies.md#SetQueryStringParameter) et [en-tête HTTP de définir](api-management-transformation-policies.md#SetHTTPheader) stratégies. À 12:10, il existe une démonstration de l’appel à une opération dans le portail des développeurs hello où vous pouvez consulter ces stratégies au travail.  
> -   13:50 - voir comment toouse hello [valider les jetons Web JSON](api-management-access-restriction-policies.md#ValidateJWT) stratégie toopre-autoriser toooperations d’accès basées sur les revendications de jeton. Avance rapide too15:00 les stratégies de hello toosee configurées dans l’éditeur de stratégie hello et puis too18:50 pour une démonstration de l’appel d’une opération à partir du portail des développeurs hello avec et sans hello requis jeton d’autorisation.  
> -   21:00 - voir comment toouse un [API inspecteur](https://azure.microsoft.com/documentation/articles/api-management-howto-api-inspector/) toosee comment les stratégies sont évaluées et hello les résultats des évaluations de hello de trace.  
> -   25:25 - voir comment les expressions de stratégie toouse avec hello [obtenir à partir du cache](api-management-caching-policies.md#GetFromCache) et [magasin toocache](api-management-caching-policies.md#StoreToCache) réponse de gestion des API tooconfigure stratégies que correspondances hello la réponse mise en cache de hello de durée de mise en cache service principal comme spécifié par hello sauvegardé du service `Cache-Control` directive.  
> -   34:30 - voir comment contenu tooperform filtrage en supprimant des éléments de données à partir de la réponse de hello provenant du service principal de hello à l’aide de hello [flux de contrôle](api-management-advanced-policies.md#choose) et [définir corps](api-management-transformation-policies.md#SetBody) stratégies. Démarrer à 31:50 toosee une vue d’ensemble de [hello API de prévision ciel foncé](https://developer.forecast.io/) utilisée pour cette démonstration.  
> -   les instructions de stratégie hello toodownload utilisées dans cette vidéo, consultez hello [api--exemples/stratégies de gestion](https://github.com/Azure/api-management-samples/tree/master/policies) référentiel github.  
  
  
##  <a name="Syntax"></a> Syntaxe  
 Les expressions à instruction unique sont entre `@(expression)`, où `expression` est une instruction d’expression C# bien formée.  
  
 Les expressions à instructions multiples sont entre `@{expression}`. Tous les chemins d’accès de code au sein des expressions à instructions multiples doivent se terminer par une instruction `return`.  
  
##  <a name="PolicyExpressionsExamples"></a> Exemples  
  
```  
@(true)  
  
@((1+1).ToString())  
  
@("Hi There".Length)  
  
@(Regex.Match(context.Response.Headers.GetValueOrDefault("Cache-Control",""), @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value)  
  
@(context.Variables.ContainsKey("maxAge") ? int.Parse((string)context.Variables["maxAge"]) : 3600)  
  
@{   
  string value;   
  if (context.Request.Headers.TryGetValue("Authorization", out value))   
  {   
    return Encoding.UTF8.GetString(Convert.FromBase64String(value));  
  }   
  else   
  {   
    return null;  
  }  
}  
```  
  
##  <a name="PolicyExpressionsUsage"></a> Utilisation  
 Expressions peuvent être utilisées en tant que valeurs d’attribut ou valeurs de texte dans un des hello gestion des API [stratégies](api-management-policies.md), sauf indication contraire de la référence de la stratégie hello.  
  
> [!IMPORTANT]
>  Notez que lorsque vous utilisez des expressions de stratégie, il existe uniquement une vérification limitée des expressions de stratégie hello lors de la stratégie de hello est définie. Étant donné que les expressions hello sont exécutées au moment de l’exécution dans le pipeline entrant ou sortant de hello par la passerelle de hello, toutes les exceptions d’exécution générées par les expressions de stratégie hello entraîne une erreur d’exécution dans l’appel d’API de hello.  
  
##  <a name="CLRTypes"></a> Types .NET Framework autorisés dans les expressions de stratégie  
 Hello tableau suivant répertorie les types .NET Framework hello et leurs membres sont autorisés dans les expressions de stratégie.  
  
|Type CLR|Méthodes prises en charge|  
|--------------|-----------------------|  
|Newtonsoft.Json.Linq.Extensions|Toutes les méthodes sont prises en charge.|  
|Newtonsoft.Json.Linq.JArray|Toutes les méthodes sont prises en charge.|  
|Newtonsoft.Json.Linq.JConstructor|Toutes les méthodes sont prises en charge.|  
|Newtonsoft.Json.Linq.JContainer|Toutes les méthodes sont prises en charge.|  
|Newtonsoft.Json.Linq.JObject|Toutes les méthodes sont prises en charge.|  
|Newtonsoft.Json.Linq.JProperty|Toutes les méthodes sont prises en charge.|  
|Newtonsoft.Json.Linq.JRaw|Toutes les méthodes sont prises en charge.|  
|Newtonsoft.Json.Linq.JToken|Toutes les méthodes sont prises en charge.|  
|Newtonsoft.Json.Linq.JTokenType|Toutes les méthodes sont prises en charge.|  
|Newtonsoft.Json.Linq.JValue|Toutes les méthodes sont prises en charge.|  
|System.Collections.Generic.IReadOnlyCollection<T\>|Tout|  
|System.Collections.Generic.IReadOnlyDictionary<TKey,  TValue>|Tout|  
|System.Collections.Generic.ISet<TKey, TValue>|Tout|  
|System.Collections.Generic.KeyValuePair<TKey,  TValue>|Key, Value|  
|System.Collections.Generic.List<TKey, TValue>|Tout|  
|System.Collections.Generic.Queue<TKey, TValue>|Tout|  
|System.Collections.Generic.Stack<TKey, TValue>|Tout|  
|System.Convert|Tout|  
|System.DateTime|Tout|  
|System.DateTimeKind|Utc|  
|System.DateTimeOffset|Tout|  
|System.Decimal|Tout|  
|System.Double|Tout|  
|System.Guid|Tout|  
|System.IEnumerable<T\>|Tout|  
|System.IEnumerator<T\>|Tout|  
|System.Int16|Tout|  
|System.Int32|Tout|  
|System.Int64|Tout|  
|System.Linq.Enumerable<T\>|Toutes les méthodes sont prises en charge.|  
|System.Math|Tout|  
|System.MidpointRounding|Tout|  
|System.Nullable<T\>|Tout|  
|System.Random|Tout|  
|System.SByte|Tout|  
|System.Security.Cryptography. HMACSHA384|Tout|  
|System.Security.Cryptography. HMACSHA512|Tout|  
|System.Security.Cryptography.HashAlgorithm|Tout|  
|System.Security.Cryptography.HMAC|Tout|  
|System.Security.Cryptography.HMACMD5|Tout|  
|System.Security.Cryptography.HMACSHA1|Tout|  
|System.Security.Cryptography.HMACSHA256|Tout|  
|System.Security.Cryptography.KeyedHashAlgorithm|Tout|  
|System.Security.Cryptography.MD5|Tout|  
|System.Security.Cryptography.RNGCryptoServiceProvider|Tout|  
|System.Security.Cryptography.SHA1|Tout|  
|System.Security.Cryptography.SHA1Managed|Tout|  
|System.Security.Cryptography.SHA256|Tout|  
|System.Security.Cryptography.SHA256Managed|Tout|  
|System.Security.Cryptography.SHA384|Tout|  
|System.Security.Cryptography.SHA384Managed|Tout|  
|System.Security.Cryptography.SHA512|Tout|  
|System.Security.Cryptography.SHA512Managed|Tout|  
|System.Single|Tout|  
|System.String|Tout|  
|System.StringSplitOptions|Tout|  
|System.Text.Encoding|Tout|  
|System.Text.RegularExpressions.Capture|Index, Length, Value|  
|System.Text.RegularExpressions.CaptureCollection|Count, Item|  
|System.Text.RegularExpressions.Group|Captures, Success|  
|System.Text.RegularExpressions.GroupCollection|Count, Item|  
|System.Text.RegularExpressions.Match|Empty, Groups, Result|  
|System.Text.RegularExpressions.Regex|.ctor, IsMatch, Match, Matches, Replace|  
|System.Text.RegularExpressions.RegexOptions|Compiled, IgnoreCase, IgnorePatternWhitespace, Multiline, None, RightToLeft, Singleline|  
|System.TimeSpan|Tout|  
|System.Tuple|Tout|  
|System.UInt16|Tout|  
|System.UInt32|Tout|  
|System.UInt64|Tout|  
|System.Uri|Tout|  
|System.Xml.Linq.Extensions|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XAttribute|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XCData|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XComment|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XContainer|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XDeclaration|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XDocument|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XDocumentType|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XElement|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XName|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XNamespace|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XNode|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XNodeDocumentOrderComparer|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XNodeEqualityComparer|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XObject|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XProcessingInstruction|Toutes les méthodes sont prises en charge.|  
|System.Xml.Linq.XText|Toutes les méthodes sont prises en charge.|  
|System.Xml.XmlNodeType|Tout|  
  
##  <a name="ContextVariables"></a> Variable de contexte  
 Une variable nommée `context` est implicitement disponible dans toutes les [expressions](api-management-policy-expressions.md#Syntax) de stratégie. Ses membres fournissent toohello pertinentes des informations `\request`. Tous les hello `context` membres sont en lecture seule.  
  
|Variable de contexte|Méthodes, propriétés et valeurs de paramètres autorisées|  
|----------------------|-------------------------------------------------------|  
|context|Api: IApi<br /><br /> Déploiement<br /><br /> LastError<br /><br /> Opération<br /><br /> Produit<br /><br /> Demande<br /><br /> RequestId: string<br /><br /> Réponse<br /><br /> Abonnement<br /><br /> Tracing: bool<br /><br /> Utilisateur<br /><br /> Variables:IReadOnlyDictionary<string, object><br /><br /> void Trace(message: string)|  
|context.Api|Id: string<br /><br /> Name: string<br /><br /> Path: string<br /><br /> ServiceUrl: IUrl|  
|context.Deployment|Region: string<br /><br /> ServiceName: string|  
|context.LastError|Source: string<br /><br /> Reason: string<br /><br /> Message: string<br /><br /> Scope: string<br /><br /> Section: string<br /><br /> Path: string<br /><br /> PolicyId: string<br /><br /> Pour plus d’informations sur context.LastError, consultez la page [Gestion des erreurs](api-management-error-handling-policies.md).|  
|context.Operation|Id: string<br /><br /> Method: string<br /><br /> Name: string<br /><br /> UrlTemplate: string|  
|context.Product|Apis: IEnumerable<IApi\><br /><br /> ApprovalRequired: bool<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: string<br /><br /> Name: string<br /><br /> State: enum ProductState {NotPublished, Published}<br /><br /> SubscriptionLimit: int?<br /><br /> SubscriptionRequired: bool|  
|context.Request|Body: IMessageBody<br /><br /> Certificate: System.Security.Cryptography.X509Certificates.X509Certificate2<br /><br /> Headers: IReadOnlyDictionary<string, string[]><br /><br /> IpAddress: string<br /><br /> MatchedParameters: IReadOnlyDictionary<string, string><br /><br /> Method: string<br /><br /> OriginalUrl:IUrl<br /><br /> Url: IUrl|  
|string context.Request.Headers.GetValueOrDefault(headerName: string, defaultValue: string)|headerName: string<br /><br /> defaultValue: string<br /><br /> Valeurs d’en-tête de demande séparées par des virgules de retours ou `defaultValue` si hello en-tête est introuvable.|  
|context.Response|Body: IMessageBody<br /><br /> Headers: IReadOnlyDictionary<string, string[]><br /><br /> StatusCode: int<br /><br /> StatusReason: string|  
|string context.Response.Headers.GetValueOrDefault(headerName: string, defaultValue: string)|headerName: string<br /><br /> defaultValue: string<br /><br /> Retourne des valeurs d’en-tête de réponse de séparés par des virgules ou `defaultValue` si hello en-tête est introuvable.|  
|context.Subscription|CreatedTime: DateTime<br /><br /> EndDate: DateTime?<br /><br /> Id: string<br /><br /> Key: string<br /><br /> Name: string<br /><br /> PrimaryKey: string<br /><br /> SecondaryKey: string<br /><br /> StartDate: DateTime?|  
|context.User|Email: string<br /><br /> FirstName: string<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: string<br /><br /> Identities: IEnumerable<IUserIdentity\><br /><br /> LastName: string<br /><br /> Note: string<br /><br /> RegistrationDate: DateTime|  
|IApi|Id: string<br /><br /> Name: string<br /><br /> Path: string<br /><br /> Protocols: IEnumerable<string\><br /><br /> ServiceUrl: IUrl<br /><br /> SubscriptionKeyParameterNames: ISubscriptionKeyParameterNames|  
|IGroup|Id: string<br /><br /> Name: string|  
|IMessageBody|As<T\>(preserveContent: bool = false): Where T: string, JObject, JToken, JArray, XNode, XElement, XDocument<br /><br /> Hello `context.Request.Body.As<T>` et `context.Response.Body.As<T>` méthodes sont utilisée tooread corps d’un message de demande et de réponse dans un type spécifié `T`. Hello flux du corps du message d’origine (méthode) utilise hello et reneders elle retourne par défaut indisponibles après elle. tooavoid qui, en demandant la méthode hello ne fonctionne pas sur une copie du flux de corps hello, jeu hello `preserveContent` paramètre trop`true`. Accédez [ici](api-management-transformation-policies.md#SetBody) toosee un exemple.|  
|IUrl|Host: string<br /><br /> Path: string<br /><br /> Port: int<br /><br /> Query: IReadOnlyDictionary<string, string[]><br /><br /> QueryString: string<br /><br /> Scheme: string|  
|IUserIdentity|Id: string<br /><br /> Provider: string|  
|ISubscriptionKeyParameterNames|Header: string<br /><br /> Query: string|  
|string IUrl.Query.GetValueOrDefault(queryParameterName: string, defaultValue: string)|queryParameterName: string<br /><br /> defaultValue: string<br /><br /> Les valeurs de paramètre de requête séparées par des virgules de retours ou `defaultValue` si le paramètre hello est introuvable.|  
|T context.Variables.GetValueOrDefault<T\>(variableName: string, defaultValue: T)|variableName: string<br /><br /> defaultValue: T<br /><br /> Retourne la valeur de la variable cast tootype `T` ou `defaultValue` si hello variable est introuvable.<br /><br /> Cette méthode lève une exception si hello type spécifié ne correspond pas hello réel type Hello retourné variable.|  
|BasicAuthCredentials AsBasic(input: this string)|input: string<br /><br /> Si le paramètre d’entrée hello contient une valeur d’en-tête de demande valide l’authentification de base HTTP d’autorisation, méthode hello retourne un objet de type `BasicAuthCredentials`; sinon, méthode hello retourne la valeur null.|  
|bool TryParseBasic(input: this string, result: out BasicAuthCredentials)|input: string<br /><br /> result: out BasicAuthCredentials<br /><br /> Si le paramètre d’entrée hello contient une valeur d’en-tête de demande valide l’authentification de base HTTP d’autorisation, de méthode de hello retourne `true` et paramètre de résultat hello contient une valeur de type `BasicAuthCredentials`; sinon, retourne méthode hello `false`.|  
|BasicAuthCredentials|Password: string<br /><br /> UserId: string|  
|Jwt AsJwt(input: this string)|input: string<br /><br /> Si le paramètre d’entrée hello contient une valeur valide de jeton Web JSON, méthode hello retourne un objet de type `Jwt`; sinon, retourne méthode hello `null`.|  
|bool TryParseJwt(input: this string, result: out Jwt)|input: string<br /><br /> result: out Jwt<br /><br /> Retourne de méthode hello si le paramètre d’entrée hello contient une valeur valide de jeton JWT, `true` et paramètre de résultat hello contient une valeur de type `Jwt`; sinon, retourne méthode hello `false`.|  
|Jwt|Algorithm: string<br /><br /> Audience: IEnumerable<string\><br /><br /> Claims: IReadOnlyDictionary<string, string[]><br /><br /> ExpirationTime: DateTime?<br /><br /> Id: string<br /><br /> Issuer: string<br /><br /> NotBefore: DateTime?<br /><br /> Subject: string<br /><br /> Type: string|  
|string Jwt.Claims.GetValueOrDefault(claimName: string, defaultValue: string)|claimName: string<br /><br /> defaultValue: string<br /><br /> Retourne les valeurs de revendication séparées par des virgules ou `defaultValue` si hello en-tête est introuvable.|

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).  
