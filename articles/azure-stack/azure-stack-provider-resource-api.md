---
title: "API de l’utilisation des ressources d’aaaProvider | Documents Microsoft"
description: "Informations de référence sur l’utilisation de ressources API, lesquelles récupèrent des informations relatives à l’utilisation d’Azure Stack."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b6055923-b6a6-45f0-8979-225b713150ae
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: alfredop
ms.openlocfilehash: 7cc2d7af27e6abc86e247b2ed0ab1bc236fdb1af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provider-resource-usage-api"></a>API d’utilisation des ressources de fournisseur
fournisseur de terme Hello s’applique toohello administrateur du service et les fournisseurs de tooany déléguée. Administrateurs de service et les fournisseurs de délégués permet l’utilisation de hello tooview API de fournisseur d’utilisation de leurs clients directs. Par exemple, P0 peut appeler des informations sur l’utilisation de hello API fournisseur tooget de P1 et de P2 utilisation directe et P1 peut appeler pour obtenir des informations sur P3 et P4.

![Modèle conceptuel de la hiérarchie des fournisseurs](media/azure-stack-provider-resource-api/image1.png)

## <a name="api-call-reference"></a>Référence de l’appel d’API
### <a name="request"></a>Demande
Détails de la consommation Obtient la demande Hello pour hello demandé des abonnements et hello demandée laps de temps. Il n’existe aucun corps de demande.

L’utilisation de cette API est une API de fournisseur, donc appelant de hello doit être affectée à un rôle de propriétaire, collaborateur ou lecteur dans l’abonnement du fournisseur hello.

| **Méthode** | **URI de la requête** |
| --- | --- |
| GET |https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&subscriberId={sub1.1}&api-version=2015-06-01-preview&continuationToken={token-value} |

### <a name="arguments"></a>Arguments
| **Argument** | **Description** |
| --- | --- |
| *armendpoint* |Point de terminaison Azure Resource Manager de votre environnement Azure Stack. Hello convention de Azure pile désigne le nom hello du Gestionnaire de ressources Azure point de terminaison est au format de hello `https://adminmanagement.{domain-name}`. Par exemple, si hello nom de domaine est local.azurestack.external, hello Gestionnaire de ressources du point de terminaison est `https://adminmanagement.local.azurestack.external`. |
| *subId* |ID d’abonnement de l’utilisateur hello appel hello. |
| *reportedStartTime* |Heure de début de requête de hello. Hello valeur pour *DateTime* doit être au format UTC et au début de hello d’heure hello, par exemple, 13:00. Pour l’agrégation quotidienne, définissez cette minuit tooUTC de valeur. format de Hello est *échappé* ISO 8601, par exemple, 2015-06-16T18 % 3a53 % 3a11 % 2b00 % 3a00Z, où le signe deux-points sont échappé trop % 3 a et ainsi que la séquence d’échappement trop % 2 b afin qu’il soit URI convivial. |
| *reportedEndTime* |Heure de fin de la requête de hello. Hello des contraintes qui s’appliquent trop*reportedStartTime* également appliquer toothis argument. Hello valeur pour *reportedEndTime* ne peut pas être hello futures ou hello date actuelle. S’il s’agit, le résultat de hello est défini trop « traitement ne pas terminée. » |
| *aggregationGranularity* |Paramètre facultatif qui a deux valeurs potentielles discrètes : quotidienne et horaire. Comme les valeurs hello suggèrent, un retourne les données de salutation dans une granularité journalière et hello autres est une résolution de toutes les heures. quotidien Hello est par défaut de hello. |
| *subscriberId* |l'ID d'abonnement. tooget les données filtrées, ID d’abonnement hello d’un locataire direct du fournisseur de hello est requis. Si aucun paramètre de ID d’abonnement est spécifié, appel de hello retourne les données d’utilisation pour les locataires directe du fournisseur du hello. |
| *api-version* |Version de protocole hello toomake utilisé cette demande. Cette valeur est définie à too2015-06-01-preview. |
| *continuationToken* |Jeton récupéré à partir de hello dernier appel toohello utilisation de l’API fournisseur. Ce jeton est nécessaire lorsqu’une réponse est supérieure à 1 000 lignes et agit comme un signet pour les cours hello. Si ce n’est pas le cas présent, hello données sont récupérées à partir du début hello hello ou les heures, en fonction de la granularité hello passée dans. |

### <a name="response"></a>Réponse
GET /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&subscriberId=sub1.1&api-version=1.0

{

"value": \[

{

"id": "/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-

meterID1",

"name": "sub1.1-meterID1",

"type": "Microsoft.Commerce/UsageAggregate",

"properties": {

"subscriptionId":"sub1.1",

"usageStartTime": "2015-03-03T00:00:00+00:00",

"usageEndTime": "2015-03-04T00:00:00+00:00",

"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\

":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",

"quantity":2.4000000000,

"meterId":"meterID1"

}

},

…

### <a name="response-details"></a>Détails de la réponse
| **Argument** | **Description** |
| --- | --- |
| *id* |ID unique de l’utilisation de hello d’agrégation |
| *name* |Nom de l’utilisation de hello d’agrégation |
| *type* |Définition de la ressource |
| *subscriptionId* |Identificateur d’abonnement de l’utilisateur d’Azure pile hello |
| *usageStartTime* |UTC heure de début de hello utilisation compartiment toowhich cet agrégat d’utilisation appartient |
| *usageEndTime* |UTC fin de hello utilisation compartiment toowhich cet agrégat d’utilisation appartient |
| *instanceData* |Paires clé-valeur des détails de l’instance (dans un nouveau format) :<br> *resourceUri*: complet des ID de ressource, qui inclut les groupes de ressources hello et nom de l’instance hello <br> *location* : région dans laquelle ce service a été exécuté <br> *balises*: les balises de ressources qui sont spécifiées par l’utilisateur de hello <br> *additionalInfo*: plus d’informations sur la ressource hello consommé, par exemple, le type d’image ou de la version du système d’exploitation |
| *quantity* |Quantité de ressources consommées au cours de cette période |
| *meterId* |ID unique pour la ressource hello qui a été consommée (également appelé *ResourceID*) |

## <a name="next-steps"></a>Étapes suivantes
[Informations de référence sur l’API d’utilisation des ressources de locataire](azure-stack-tenant-resource-usage-api.md)

[Questions fréquentes (FAQ) relatives à l’utilisation](azure-stack-usage-related-faq.md)

