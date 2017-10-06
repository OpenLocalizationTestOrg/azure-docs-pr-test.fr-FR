---
title: "aaaAzure API d’entreprise facturation - frais Marketplace | Documents Microsoft"
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>API de création de rapports pour les clients Enterprise - Marketplace Store Charge

Hello Marketplace magasin frais API retourne hello basée sur l’utilisation de marketplace frais répartition par jour pour hello spécifié la période de facturation ou les dates de début et de fin (frais d’une seule fois ne sont pas inclus).

##<a name="request"></a>Demande 
Propriétés d’en-tête commun nécessitant toobe ajouté sont spécifiées [ici](billing-enterprise-api.md). Si une période de facturation n’est pas spécifiée, puis les données de facturation actuel de hello période sont retournées. Plages d’heure personnalisé peuvent être spécifiés avec le début de hello et les paramètres de date sont précis hello format AAAA-MM-JJ, hello maximale prise en charge est comprise entre 36 mois de fin.  

|Méthode | URI de demande|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> version d’évaluation hello toouse de l’API, remplacez v2 v1 Bonjour au-dessus des URL.
>

## <a name="response"></a>Réponse
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

**Définitions des propriétés de réponse**

|Nom de la propriété| Type| Description
|-|-|-|
|id|string|Id unique de l’élément de frais marketplace hello|
|subscriptionGuid|Guid|Hello Guid de l’abonnement|
|subscriptionName|string|Nom de l’abonnement de Hello|
|meterId|string|ID de hello émis compteur|
|usageStartDate|DateTime|Heure de début de l’enregistrement de l’utilisation de hello|
|usageEndDate|DateTime|Heure de fin de l’enregistrement de l’utilisation de hello|
|offerName|string|nom de l’offre Hello|
|resourceGroup|string|ressource de Hello groupe|
|instanceId|string|ID de l’instance|
|additionalInfo|string|Chaîne JSON avec informations supplémentaires|
|tags|string|Chaîne JSON de balise|
|orderNumber|string|numéro de commande Hello|
|unitOfMeasure|string|Unité de mesure pour le compteur de hello|
|costCenter|string|Centre de coût de Hello|
|accountId|int|compte Hello Id|
|accountName|string |Nom du compte de Hello|
|accountOwnerId|string|Hello Id de propriétaire de compte|
|departmentId|int|service Hello Id|
|departmentName|string|nom du service informatique Hello|
|publisherName|string|nom de l’éditeur Hello|
|planName|string|nom du Plan Hello|
|consumedQuantity|Décimal|Quantité consommée pendant cette période|
|resourceRate|Décimal|Prix unitaire pour le compteur de hello|
|extendedCost|Décimal|Estimation des frais en fonction de la quantité consommée et du coût global|
<br/>
## <a name="see-also"></a>Voir aussi

* [API Périodes de facturation](billing-enterprise-api-billing-periods.md)

* [API Détails de l’utilisation](billing-enterprise-api-usage-detail.md) 

* [API Solde et résumé](billing-enterprise-api-balance-summary.md)

* [API Grille tarifaire](billing-enterprise-api-pricesheet.md)