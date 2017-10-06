---
title: aaaAzure de facturation des API Enterprise | Documents Microsoft
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>Vue d’ensemble des API de création de rapports pour les clients Enterprise
Hello Reporting API permettent la consommation de Azure d’entreprise clients tooprogrammatically par extraction de données et les données de facturation dans les outils d’analyse de données par défaut. 

## <a name="enabling-data-access-toohello-api"></a>L’activation des API de toohello d’accès aux données
* **Générer ou de récupérer la clé d’API de hello** API de création de rapports - journal toohello Enterprise portal et suivez hello didacticiel sous aide -. première section de Hello sous cet article d’aide explique comment la clé hello API toogenerate ou récupérer pour hello spécifiée d’inscription.
* **Passe des clés Bonjour API** -clé de hello API doit toobe passé pour chaque appel d’authentification et autorisation. la propriété suivante Hello doit toobe toohello HTTP en-têtes

|Clé d’en-tête de demande | Valeur|
|-|-|
|Autorisation| Spécifiez la valeur de hello dans ce format : **PORTEUR {API_KEY}** <br/> Exemple : porteur eyr... 09|

## <a name="consumption-apis"></a>API de consommation
Il existe un point de terminaison Swagger [ici](https://consumption.azure.com/swagger/ui/index) pour hello API décrites dessous de laquelle doit activer les introspection facile de hello API et du client de toogenerate hello capacité kits de développement logiciel à l’aide de [AutoRest](https://github.com/Azure/AutoRest) ou [ Swagger CodeGen](http://swagger.io/swagger-codegen/). À compter du 1er mai 2014, ces données sont disponibles via cette API. 

* **Solde et résumé** - hello [solde et API Résumé](billing-enterprise-api-balance-summary.md) offre un résumé de tous les mois d’informations sur les soldes, nouveaux achats, des frais de service Azure Marketplace, ajustements et frais de dépassement.

* **Détails d’utilisation** - hello [API des détails d’utilisation](billing-enterprise-api-usage-detail.md) offre une analyse quotidienne des quantités consommées et frais estimés par une inscription. résultat de Hello inclut également des informations sur les instances, les compteurs et les services. Hello API peut être interrogée par période de facturation ou par un début spécifiée et la date de fin. 

* **Les frais Marketplace magasin** - hello [API du magasin de frais Marketplace](billing-enterprise-api-marketplace-storecharge.md) retourne répartition de frais hello basée sur l’utilisation de marketplace par jour pour hello spécifié la période de facturation ou les dates de début et de fin (frais d’une seule fois ne sont pas inclus) .

* **Table de tarification** - hello [API de feuille de prix](billing-enterprise-api-pricesheet.md) fournit les taux applicable hello pour chacun des compteurs pour hello donné d’inscription et la période de facturation. 

## <a name="helper-apis"></a>API d’assistance
 **Liste des périodes de facturation** - hello [API de périodes de facturation](billing-enterprise-api-billing-periods.md) retourne une liste de facturation des périodes qui ont des données de consommation pour hello spécifié d’inscription dans l’ordre chronologique inverse. Chaque période contient une propriété pointant itinéraire d’API toohello pour hello quatre ensembles de données - BalanceSummary, UsageDetails, frais Marketplace et table de tarification.


## <a name="api-response-codes"></a>Codes de réponse HTTP  
|Code du statut de réponse|Message|Description|
|-|-|-|
|200| OK|Aucune erreur|
|401| Non autorisé| Clé API introuvable, non valide, expirée, etc.|
|404| Non disponible| Point de terminaison de rapport introuvable|
|400| Demande incorrecte| Paramètres non valides : plages de dates, nombres de Contrats Entreprise (EA), etc.|
|500| Erreur de serveur| Erreur inattendue lors du traitement de la demande| 









