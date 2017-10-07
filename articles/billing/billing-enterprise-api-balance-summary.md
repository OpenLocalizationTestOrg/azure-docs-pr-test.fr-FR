---
title: "aaaAzure API d’entreprise facturation - solde et résumé | Documents Microsoft"
description: "En savoir plus sur l’utilisation de facturation d’Azure et RateCard APIs, qui sont utilisés tooprovide connaître la consommation des ressources Azure et les tendances."
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a>API de création de rapports pour les clients Enterprise - Balance and Summary

Hello solde et résumé API offre un résumé mensuel d’informations sur les soldes, nouveaux achats, des frais de service Azure Marketplace, ajustements et frais de dépassement.


##<a name="request"></a>Demande 
Propriétés d’en-tête commun nécessitant toobe ajouté sont spécifiées [ici](billing-enterprise-api.md). Si une période de facturation n’est pas spécifiée, puis les données de facturation actuel de hello période sont retournées.

|Méthode | URI de demande|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary|

> [!Note]
> version d’évaluation hello toouse de l’API, remplacez v2 v1 Bonjour au-dessus des URL.
>

## <a name="response"></a>Réponse

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


**Définitions des propriétés de réponse**

|Nom de la propriété| Type| Description
|-|-|-|
|id|string|Hello Id unique pour une période de facturation donnée et l’inscription|
|billingPeriodId|string |Hello Id période de facturation|
|currencyCode|string |code de devise Hello|
|beginningBalance|Décimal| Solde de début Hello pour la période de facturation hello|
|endingBalance|Décimal| Hello solde de fin pour la période de facturation hello (pour les périodes ouvertes que cela sera mise à jour tous les jours)|
|newPurchases|Décimal| Montant total des nouveaux achats|
|adjustments|Décimal| Montant total d’ajustement|
|utilized|Décimal| Utilisation totale par de l’engagement|
|serviceOverage|Décimal| Dépassement des services Azure|
|chargesBilledSeparately|Décimal| Frais facturés séparément|
|totalOverage|Décimal| serviceOverage + chargesBilledSeparately|
|totalUsage|Décimal| Engagement de service Azure + total du dépassement|
|azureMarketplaceServiceCharges|Décimal| Total des frais pour la Place de marché Azure|
|newPurchasesDetails|Tableau de chaînes JSON de paires nom/valeur|Liste de nouveaux achats|
|adjustmentDetails|Tableau de chaînes JSON de paires nom/valeur|Liste d’ajustements (crédit de promotion, crédit SIE, etc.) |


<br/>
## <a name="see-also"></a>Voir aussi

* [API Périodes de facturation](billing-enterprise-api-billing-periods.md)

* [API Détails de l’utilisation](billing-enterprise-api-usage-detail.md) 

* [API Frais de la Place de marché](billing-enterprise-api-marketplace-storecharge.md) 

* [API Grille tarifaire](billing-enterprise-api-pricesheet.md)