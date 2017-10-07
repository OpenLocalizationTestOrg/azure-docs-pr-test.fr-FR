---
title: "aaaAzure API d’entreprise facturation - PriceSheet | Documents Microsoft"
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>API de création de rapports pour les clients en entreprise - Grille tarifaire

Hello API de feuille de prix fournit les taux applicable hello pour chacun des compteurs pour hello donné d’inscription et la période de facturation.

##<a name="request"></a>Demande
Propriétés d’en-tête commun nécessitant toobe ajouté sont spécifiées [ici](billing-enterprise-api.md). Si une période de facturation n’est pas spécifiée, puis les données de facturation actuel de hello période sont retournées.

|Méthode | URI de demande|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet|

> [!Note]
> version d’évaluation hello toouse de l’API, remplacez v2 v1 Bonjour au-dessus des URL.
>

## <a name="response"></a>Réponse

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
>Si vous utilisez hello API d’aperçu, le champ d’ID de jauge n’est pas disponible.
>

**Définitions des propriétés de réponse**

|Nom de la propriété| Type| Description
|-|-|-|
|id| string| Hello Id unique qui représente un élément particulier de PriceSheet (compteur par période de facturation)|
|billingPeriodId| string| Hello Id unique qui représente une période de facturation particulière|
|meterId| string| Identificateur Hello pour le compteur de hello. Il peut être mappé toohello utilisation de l’ID de jauge.|
|meterName| string| nom de compteur Hello|
|unitOfMeasure| string| Hello unité de mesure de service de hello|
|includedQuantity| décimal| Quantité incluse |
|partNumber| string| numéro de référence Hello associé hello compteur|
|unitPrice| Décimal| prix unitaire Hello pour le compteur de hello|
|currencyCode| string| code de devise Hello hello UnitPrice|
<br/>
## <a name="see-also"></a>Voir aussi

* [API Périodes de facturation](billing-enterprise-api-billing-periods.md)

* [API Détails de l’utilisation](billing-enterprise-api-usage-detail.md)

* [API Solde et résumé](billing-enterprise-api-balance-summary.md)

* [API Frais de la Place de marché](billing-enterprise-api-marketplace-storecharge.md)
