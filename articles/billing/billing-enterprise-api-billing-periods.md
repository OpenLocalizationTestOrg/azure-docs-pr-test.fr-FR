---
title: "aaaAzure API Enterprise sur la facturation - périodes de facturation | Documents Microsoft"
description: "Découvrez hello API de Reporting qui permettent aux données de consommation de toopull clients entreprise Azure par programme."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>API de création de rapports pour les clients Enterprise : périodes de facturation

Hello API de périodes de facturation retourne une liste de facturation des périodes qui contiennent des données de consommation pour hello spécifiée d’inscription dans l’ordre chronologique inverse. Chaque période contient une propriété pointant itinéraire d’API toohello pour hello quatre ensembles de données - BalanceSummary, UsageDetails, les frais de Marktplace et PriceSheet. Si la période de hello n’a pas de données, la propriété correspondante de hello est null. 


##<a name="request"></a>Demande 
Propriétés d’en-tête commun nécessitant toobe ajouté sont spécifiées [ici](billing-enterprise-api.md). 

|Méthode | URI de demande|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods|

> [!Note]
> version d’évaluation hello toouse de l’API, remplacez v2 v1 Bonjour au-dessus des URL.
>

## <a name="response"></a>Réponse
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

**Définitions des propriétés de réponse**

|Nom de la propriété| Type| Description
|-|-|-|
|billingPeriodId| string| Hello Id unique qui représente une période de facturation particulière|
|billingStart| datetime| Chaîne ISO 8601 représentant la date de début de la période de hello|
|billingEnd| datetime| Chaîne ISO 8601 représentant la date de fin de la période de hello|
|balanceSummary| string| chemin d’accès URL Hello qui achemine les données de résumé de solde toohello pour cette période|
|usageDetails| string| chemin d’accès URL Hello qui achemine les données des détails d’utilisation de toohello pour cette période|
|marketplaceCharges| string| chemin d’accès URL Hello qui achemine les données de frais Marketplace toohello pour cette période|
|priceSheet| string| chemin d’accès URL Hello qui achemine les données de PriceSheet toohello pour cette période|

<br/>
## <a name="see-also"></a>Voir aussi

* [API Solde et résumé](billing-enterprise-api-balance-summary.md)

* [API Détails de l’utilisation](billing-enterprise-api-usage-detail.md) 

* [API Frais de la Place de marché](billing-enterprise-api-marketplace-storecharge.md) 

* [API Grille tarifaire](billing-enterprise-api-pricesheet.md)