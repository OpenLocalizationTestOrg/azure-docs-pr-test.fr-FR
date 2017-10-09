---
title: "API de l’utilisation des ressources d’aaaTenant | Documents Microsoft"
description: "Informations de référence sur l’utilisation de ressources API, lesquelles récupèrent des informations relatives à l’utilisation d’Azure Stack."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b9d7c7ee-e906-4978-92a3-a2c52df16c36
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: eb826aba87b3b5b79155d9003162f2b5e6871f82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tenant-resource-usage-api"></a>API d’utilisation des ressources de locataire
Un locataire peut utiliser des données d’utilisation de ressources hello API client tooview hello du client. Cette API méthode est cohérente avec hello API de l’utilisation de Azure (actuellement en aperçu privé).

Vous pouvez utiliser les applets de commande Windows PowerShell hello **Get-UsageAggregates** tooget les données d’utilisation comme dans Azure.

## <a name="api-call"></a>Appel d’API
### <a name="request"></a>Demande
Détails de la consommation Obtient la demande Hello pour hello demandé des abonnements et hello demandée laps de temps. Il n’existe aucun corps de demande.

| **Méthode** | **URI de la requête** |
| --- | --- |
| GET |https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value} |

### <a name="arguments"></a>Arguments
| **Argument** | **Description** |
| --- | --- |
| *Armendpoint* |Point de terminaison Azure Resource Manager de votre environnement Azure Stack. Hello convention de Azure pile désigne le nom hello du Gestionnaire de ressources Azure point de terminaison est au format de hello `https://management.{domain-name}`. Par exemple, si hello nom de domaine est local.azurestack.external, hello Gestionnaire de ressources du point de terminaison est `https://management.local.azurestack.external`. |
| *subId* |ID d’abonnement de l’utilisateur hello appel hello. Vous pouvez utiliser cette tooquery uniquement API à l’usage d’un abonnement unique. Fournisseurs peuvent utiliser l’utilisation de tooquery hello API de l’utilisation de ressources de fournisseur pour tous les clients. |
| *reportedStartTime* |Heure de début de requête de hello. Hello valeur pour *DateTime* doit être au format UTC et au début de hello d’heure hello, par exemple, 13:00. Pour l’agrégation quotidienne, définissez cette minuit tooUTC de valeur. format de Hello est *échappé* ISO 8601, par exemple, 2015-06-16T18 % 3a53 % 3a11 % 2b00 % 3a00Z, où le signe deux-points sont échappé trop % 3 a et ainsi que la séquence d’échappement trop % 2 b afin qu’il soit URI convivial. |
| *reportedEndTime* |Heure de fin de la requête de hello. Hello des contraintes qui s’appliquent trop*reportedStartTime* également appliquer toothis argument. Hello valeur pour *reportedEndTime* ne peut pas être Bonjour futures. |
| *aggregationGranularity* |Paramètre facultatif qui a deux valeurs potentielles discrètes : quotidienne et horaire. Comme les valeurs hello suggèrent, un retourne les données de salutation dans une granularité journalière et hello autres est une résolution de toutes les heures. quotidien Hello est par défaut de hello. |
| *api-version* |Version de protocole hello toomake utilisé cette demande. Vous devez utiliser 2015-06-01-preview. |
| *continuationToken* |Jeton récupéré à partir de hello dernier appel toohello utilisation de l’API fournisseur. Ce jeton est nécessaire quand une réponse comprend plus de 1 000 lignes. Il joue alors le rôle de signet pour la progression. Si ce n’est pas le cas présent, hello données sont récupérées à partir du début hello hello ou les heures, en fonction de la granularité hello passée dans. |

### <a name="response"></a>Réponse
GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0

{

"value": \[

{

"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",

"name": "sub1-meterID1",

"type": "Microsoft.Commerce/UsageAggregate",

"properties": {

"subscriptionId":"sub1",

"usageStartTime": "2015-03-03T00:00:00+00:00",

"usageEndTime": "2015-03-04T00:00:00+00:00",

"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",

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
| *subscriptionId* |Identificateur d’abonnement de hello utilisateur Azure |
| *usageStartTime* |UTC heure de début de hello utilisation compartiment toowhich cet agrégat d’utilisation appartient |
| *usageEndTime* |UTC fin de hello utilisation compartiment toowhich cet agrégat d’utilisation appartient |
| *instanceData* |Paires clé-valeur des détails de l’instance (dans un nouveau format) :<br>  *resourceUri* : ID de ressource complet, notamment les groupes de ressources et le nom de l’instance <br>  *location* : région dans laquelle ce service a été exécuté <br>  *balises*: Spécifie de cet utilisateur hello les balises de ressources <br>  *additionalInfo*: plus d’informations sur la ressource hello consommé, par exemple, le type d’image ou de la version du système d’exploitation |
| *quantity* |Quantité de ressources consommées au cours de cette période |
| *meterId* |ID unique pour la ressource hello qui a été consommée (également appelé *ResourceID*) |

## <a name="next-steps"></a>Étapes suivantes
[API Utilisation des ressources de fournisseur](azure-stack-provider-resource-api.md)

[Questions fréquentes (FAQ) relatives à l’utilisation](azure-stack-usage-related-faq.md)

