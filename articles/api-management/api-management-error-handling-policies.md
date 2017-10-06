---
title: "aaaError la gestion des stratégies de gestion des API Azure | Documents Microsoft"
description: "Découvrez comment toorespond tooerror conditions qui peuvent se produire pendant hello le traitement des demandes de gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 002c65f21e763fd644da61b6a11685ffd97488c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-api-management-policies"></a>Gestion des erreurs dans les stratégies de la Gestion des API
Gestion des API Azure permet aux éditeurs toorespond tooerror conditions qui peuvent se produire lors du traitement de hello du proxy toohello de demandes en fournissant un `ProxyError` objet. Hello `ProxyError` objet est accessible via hello [contexte. Dernière erreur](api-management-policy-expressions.md#ContextVariables) propriété et peut être utilisé par les stratégies Bonjour `on-error` section de la stratégie. Cette rubrique fournit une référence pour l’erreur de hello dans Gestion des API Azure, les fonctions de gestion.  
  
## <a name="error-handling-in-api-management"></a>Gestion des erreurs dans la Gestion des API  
 Stratégies de gestion des API Azure sont divisés en `inbound`, `backend`, `outbound`, et `on-error` sections comme indiqué dans hello l’exemple suivant.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements toobe applied toohello request go here -->  
  </inbound>  
  <backend>  
    <!-- statements toobe applied before hello request is   
         forwarded toohello backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements toobe applied toohello response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements toobe applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 Pendant le traitement de hello d’une demande, les étapes intégrées sont exécutées en même temps que toutes les stratégies qui sont dans l’étendue de la demande de hello. Si une erreur se produit, le traitement immédiatement accède toohello `on-error` section de la stratégie. Hello `on-error` section de la stratégie peut être utilisée dans toutes les portées et éditeurs d’API peuvent configurer un comportement personnalisé comme concentrateurs de tooevent hello erreur de journalisation ou la création de nouvelle réponse tooreturn toohello l’appelant.  
  
> [!NOTE]
>  Hello `on-error` section n’est pas présente dans les stratégies par défaut. tooadd hello `on-error` section tooa stratégie, parcourir stratégie toohello souhaité dans l’éditeur de stratégie hello et l’ajouter. Pour plus d’informations sur la configuration des stratégies, consultez la page [Stratégies dans la Gestion des API](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
>   
>  En l’absence de section `on-error`, les appelants recevront des messages de réponse HTTP 400 ou 500 si une condition d’erreur se produit.  
  
### <a name="policies-allowed-in-on-error"></a>Stratégies autorisées on-error  
 Hello stratégies suivantes peuvent être utilisés dans hello `on-error` section de la stratégie.  
  
-   [choose](api-management-advanced-policies.md#choose)  
  
-   [set-variable](api-management-advanced-policies.md#set-variable)  
  
-   [find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [return-response](api-management-advanced-policies.md#ReturnResponse)  
  
-   [set-header](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [set-method](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [set-status](api-management-advanced-policies.md#SetStatus)  
  
-   [send-request](api-management-advanced-policies.md#SendRequest)  
  
-   [send-one-way-request](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [log-to-eventhub](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [json-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [xml-to-json](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>LastError  
 Lorsqu’une erreur se produit et le contrôle passe toohello `on-error` section de la stratégie, l’erreur de hello est stocké dans [contexte. Dernière erreur](api-management-policy-expressions.md#ContextVariables) propriété qui est accessible par les stratégies Bonjour `on-error` section et a les propriétés suivantes de hello.  
  
|Nom|Type|Description|Requis|  
|----------|----------|-----------------|--------------|  
|Source|string|Élément de hello de noms où hello s’est produite. Peut être une stratégie ou un nom d’étape de pipeline intégrée.|Oui|  
|Motif|string|Code d’erreur informatique, utilisable dans la gestion des erreurs.|Non|  
|Message|string|Description lisible de l’erreur.|Oui|  
|Étendue|string|Nom d’étendue hello où les erreurs hello s’est produite et peut être un des « globaux », « product », « api » ou « opération »|Non|  
|Section|string|Nom de la section où l’erreur s’est produite. Peut être « inbound », « backend », « outbound » ou « on-error ».|Non|  
|Chemin|string|Spécifie la stratégie imbriquée, par exemple, « choose[3]/when[2] ».|Non|  
|PolicyId|string|Valeur de hello `id` d’attribut, s’il est spécifié par le client hello, sur la politique de hello où l’erreur s’est produite|Non|  
  
> [!NOTE]
>  Toutes les stratégies ont facultatif `id` attribut qui peut être ajouté élément racine de toohello de stratégie de hello. Si cet attribut est présent dans une stratégie lorsqu’une condition d’erreur se produit, valeur hello d’attribut de hello permettre être récupérée à l’aide de hello `context.LastError.PolicyId` propriété.  
  
## <a name="predefined-errors-for-built-in-steps"></a>Erreurs prédéfinies pour les étapes intégrées  
 Hello erreurs suivantes sont prédéfinis pour les conditions d’erreur qui peuvent se produire lors de l’évaluation de hello des étapes de traitement intégré.  
  
|Source|Condition|Motif|Message|  
|------------|---------------|------------|-------------|  
|configuration|URI ne correspond pas à tooany Api ou l’opération|OperationNotFound|Opération de tooan demande entrante toomatch impossible.|  
|autorisation|Clé d’abonnement non fournie.|SubscriptionKeyNotFound|Accès refusé en raison de la clé d’abonnement toomissing. Assurez-vous que clé d’abonnement tooinclude lors de l’établissement des demandes toothis API.|  
|autorisation|La valeur de la clé d’abonnement n’est pas valide.|SubscriptionKeyInvalid|Accès refusé en raison de la clé d’abonnement tooinvalid. Assurez-vous que tooprovide une clé valide pour un abonnement actif.|  
  
## <a name="predefined-errors-for-policies"></a>Erreurs prédéfinies pour les stratégies  
 Hello erreurs suivantes sont prédéfinis pour les conditions d’erreur qui peuvent se produire lors de l’évaluation de stratégie.  
  
|Source|Condition|Motif|Message|  
|------------|---------------|------------|-------------|  
|rate-limit|Limite de débit dépassée.|RateLimitExceeded|Limite de débit dépassée.|  
|quota|Quota dépassé|QuotaExceeded|Quota de volume d’appels dépassé. Le quota sera réapprovisionné dans xx:xx:xx. - ou - Quota de bande passante dépassé. Le quota sera réapprovisionné dans xx:xx:xx.|  
|jsonp|La valeur du paramètre de rappel n’est pas valide (contient des caractères incorrects).|CallbackParameterInvalid|La valeur du paramètre de rappel {callback-parameter-name} n’est pas un identificateur JavaScript valide.|  
|ip-filter|IP d’appelant tooparse Échec de la demande|FailedToParseCallerIP|Échec de l’adresse IP de tooestablish de l’appelant de hello. Accès refusé.|  
|ip-filter|L’adresse IP de l’appelant ne figure pas dans la liste autorisée.|CallerIpNotAllowed|L’adresse IP de l’appelant {ip-address} n’est pas autorisée. Accès refusé.|  
|ip-filter|L’adresse IP de l’appelant figure dans la liste de blocage.|CallerIpBlocked|L’adresse IP de l’appelant est bloquée. Accès refusé.|  
|check-header|L’en-tête requis n’est pas présenté ou sa valeur est manquante.|HeaderNotFound|En-tête {en-tête-name} dans la demande hello est introuvable. Accès refusé.|  
|check-header|L’en-tête requis n’est pas présenté ou sa valeur est manquante.|HeaderValueNotAllowed|La valeur {header-value} de l’en-tête {header-name} n’est pas autorisée. Accès refusé.|  
|validate-jwt|Jeton JWT manquant dans la demande.|TokenNotFound|JWT introuvable dans la demande de hello. Accès refusé.|  
|validate-jwt|Échec de validation de la signature.|TokenSignatureInvalid|<message from jwt library\>. Accès refusé.|  
|validate-jwt|Audience non valide.|TokenAudienceNotAllowed|<message from jwt library\>. Accès refusé.|  
|validate-jwt|Émetteur non valide.|TokenIssuerNotAllowed|<message from jwt library\>. Accès refusé.|  
|validate-jwt|Jeton expiré.|TokenExpired|<message from jwt library\>. Accès refusé.|  
|validate-jwt|La clé de la signature n’a pas été résolue par l’ID.|TokenSignatureKeyNotFound|<message from jwt library\>. Accès refusé.|  
|validate-jwt|Revendications requises manquantes dans le jeton.|TokenClaimNotFound|Jeton Web JSON est manquant hello suivant revendications : < c1\>, < c2\>,... Accès refusé.|  
|validate-jwt|Incompatibilité des valeurs des revendications.|TokenClaimValueNotAllowed|La valeur {claim-value} de la revendication {revendication-name} n’est pas autorisée. Accès refusé.|  
|validate-jwt|Autres échecs de validation.|JwtInvalid|<message from jwt library\>|

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).  