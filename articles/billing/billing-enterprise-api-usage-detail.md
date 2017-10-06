---
title: "aaaAzure de facturation des API d’entreprise - détails d’utilisation | Documents Microsoft"
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>API de création de rapports pour les clients Enterprise - Détails d’utilisation

Hello API des détails d’utilisation offre une analyse quotidienne des quantités consommées et frais estimés par une inscription. résultat de Hello inclut également des informations sur les instances, les compteurs et les services. Hello API peut être interrogée par période de facturation ou par un début spécifiée et la date de fin. 
## <a name="consumption-apis"></a>API de consommation


##<a name="request"></a>Demande 
Propriétés d’en-tête commun nécessitant toobe ajouté sont spécifiées [ici](billing-enterprise-api.md). Si une période de facturation n’est pas spécifiée, puis les données de facturation actuel de hello période sont retournées. Les plages de temps personnalisé peuvent être spécifiés avec le début de hello et fin des paramètres de date qui se trouvent dans un format hello AAAA-MM-JJ. plage d’heure pris en charge maximale Hello est 36 mois.  

|Méthode | URI de demande|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails 
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> version d’évaluation hello toouse de l’API, remplacez v2 v1 Bonjour au-dessus des URL.
>

## <a name="response"></a>Réponse

> En raison de toohello potentiellement gros volume de données hello jeu est paginé. propriété de nextLink Hello, s’il est présent, spécifie le lien hello pour la page de données suivante hello. Si le lien de hello est vide, il indique à qui est la dernière page de hello. 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/>
**Définitions des propriétés de réponse**

|Nom de la propriété| Type| Description
|-|-|-|
|id| string| Hello Id unique de l’appel d’API de hello. |
|données| Tableau JSON| Tableau de détails d’utilisation quotidienne pour chaque instance\meter de Hello.|
|nextLink| string| Lorsqu’il y a plus de pages de données hello nextLink points toohello URL tooreturn hello page suivante de données. |
|accountId| int| Champ obsolète. Présent à des fins de compatibilité descendante. |
|productId| int| Champ obsolète. Présent à des fins de compatibilité descendante. |
|resourceLocationId| int| Champ obsolète. Présent à des fins de compatibilité descendante. |
|consumedServiceID| int| Champ obsolète. Présent à des fins de compatibilité descendante. |
|departmentId| int| Champ obsolète. Présent à des fins de compatibilité descendante. |
|accountOwnerEmail| string| Le compte de messagerie du propriétaire du compte hello. |
|accountName| string| Nom de client saisi du compte de hello. |
|serviceAdministratorId| string| Adresse e-mail de l’administrateur de service. |
|subscriptionId| int| Champ obsolète. Présent à des fins de compatibilité descendante. |
|subscriptionGuid| string| Identificateur Unique global pour l’abonnement de hello. |
|subscriptionName| string| Nom de l’abonnement de hello. |
|date| string| date de Hello sur lequel la consommation s’est produite. |
|product| string| Détails supplémentaires sur la jauge de hello. Exemple : A1(VM)Windows - Est de l’Asie-Pacifique|
|meterId| string| Identificateur Hello compteur hello qui a émis l’utilisation. |
|meterCategory| string| Hello service de plateforme Azure qui a été utilisé. |
|meterSubCategory| string| Définit le type de service Azure de hello qui peut affecter les taux de hello. Exemple : A1 VM (Non-Windows|
|meterRegion| string| Identifie l’emplacement hello de centre de données hello pour certains services dont le prix est basée sur l’emplacement du centre de données. |
|meterName| string| Nom du compteur de hello. |
|consumedQuantity| double| quantité de Hello de compteur hello qui ont été consommé. |
|resourceRate| double| taux de Hello est applicable par unité facturable. |
|coût| double| frais de Hello engagé pour le compteur de hello. |
|resourceLocation| string| Identifie hello de centre de données sur lequel le compteur de hello s’exécute. |
|consumedService| string| Hello service de plateforme Azure qui a été utilisé. |
|instanceId| string| Cet identificateur est hello nom de ressource de hello ou hello complet ID de ressource. Pour plus d’informations, consultez [API Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). |
|serviceInfo1| string| Métadonnées de service Azure interne. |
|serviceInfo2| string| Par exemple, le type d’image d’une machine virtuelle et le nom du fournisseur de services Internet pour ExpressRoute. |
|additionalInfo| string| Métadonnées relatives au service. Par exemple, le type d’image d’une machine virtuelle. |
|tags| string| Balises ajoutées par le client. Pour plus d’informations, voir [Organisation des ressources Azure à l’aide de balises](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags). |
|storeServiceIdentifier| string| Cette colonne n’est pas utilisée. Présent à des fins de compatibilité descendante. |
|departmentName| string| Nom du service de hello. |
|costCenter| string| Centre de coût Hello qui est associée à l’utilisation de hello. |
|unitOfMeasure| string| Identifie l’unité de hello service de hello est facturé en. Par exemple : Go, heures, 10 000 s. |
|resourceGroup| string| groupe de ressources Hello dans quel hello compteur déployé est en cours d’exécution dans. Pour plus d’informations, consultez [Présentation d’Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
<br/>
## <a name="see-also"></a>Voir aussi

* [API Périodes de facturation](billing-enterprise-api-billing-periods.md)

* [API Solde et résumé](billing-enterprise-api-balance-summary.md)

* [API Frais de la Place de marché](billing-enterprise-api-marketplace-storecharge.md) 

* [API Grille tarifaire](billing-enterprise-api-pricesheet.md)
