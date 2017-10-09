---
title: "aaaUsage API liées à des questions fréquentes | Documents Microsoft"
description: "Liste des compteurs de la pile d’Azure, comparaison tooAzure l’utilisation des API, l’utilisation et signalés temps, les codes d’erreur."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: 847f18b2-49a9-4931-9c09-9374e932a071
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: alfredop
ms.openlocfilehash: 6881fc46f69b6e61a3754c44360ccfb9643a2270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-usage-api-faqs"></a>Questions fréquentes (FAQ) sur l’API d’utilisation d’Azure Stack
Cet article répond à certaines questions fréquemment posées sur hello API de l’utilisation de pile Azure.

## <a name="what-meter-ids-can-i-see"></a>Quels ID de compteur sont visibles ?
Actuellement, l’utilisation est signalée pour les fournisseurs de ressources de calcul, stockage et réseau de hello.

| **Fournisseur de ressources** | **ID du compteur** | **Nom du compteur** | **Unité** | **Informations supplémentaires** |
| --- | --- | --- | --- | --- | 
| **Réseau** |F271A8A388C44D93956A063E1D2FA80B |Static IP Address Usage |Adresses IP|Nombre d’adresses IP utilisées | 
| |9E2739BA86744796B465F64674B822BA |Dynamic IP Address Usage |Adresses IP|Nombre d’adresses IP utilisées | 
| **Stockage** |B4438D5D-453B-4EE1-B42A-DC72E377F1E4 |TableCapacity |Go\*heures |Capacité totale consommée par table |
| | B5C15376-6C94-4FDD-B655-1A69D138ACA3 |PageBlobCapacity |Go\*heures |Capacité totale consommée par objet blob de pages |
| | B03C6AE7-B080-4BFA-84A3-22C800F315C6 |QueueCapacity |Go\*heures |Capacité totale consommée par file d’attente |
| | 09F8879E-87E9-4305-A572-4B7BE209F857 |BlockBlobCapacity |Go\*heures |Capacité totale consommée par objet blob de blocs |
| | B9FF3CD0-28AA-4762-84BB-FF8FBAEA6A90 |TableTransactions |Nombre de requêtes en 10 000 s |Requêtes de service de Table (en 10 000 s) |
| | 50A1AEAF-8ECA-48A0-8973-A5B3077FEE0D |TableDataTransIn |Données en entrée, en Go |Entrée de données de service de Table, en Go |
| | 1B8C1DEC-EE42-414B-AA36-6229CF199370 |TableDataTransOut |Sortie, en Go |Sortie de données de service de Table, en Go |
| | 43DAF82B-4618-444A-B994-40C23F7CD438 |BlobTransactions |Nombre de requêtes en 10 000 s |Requêtes de service BLOB (en 10 000 s) |
| | 9764F92C-E44A-498E-8DC1-AAD66587A810 |BlobDataTransIn |Données en entrée, en Go |Entrée de données de service BLOB, en Go |
| | 3023FEF4-ECA5-4D7B-87B3-CFBC061931E8 |BlobDataTransOut |Sortie, en Go |Sortie de données de service BLOB, en Go |
| | EB43DD12-1AA6-4C4B-872C-FAF15A6785EA |QueueTransactions |Nombre de requêtes en 10 000 s |Requêtes de service de File d’attente (en 10 000 s) |
| | E518E809-E369-4A45-9274-2017B29FFF25 |QueueDataTransIn |Données en entrée, en Go |Entrée de données de service de File d’attente, en Go | 
| | DD0A10BA-A5D6-4CB6-88C0-7D585CEF9FC2 |QueueDataTransOut |Sortie, en Go |Sortie de données de service de File d’attente, en Go |
| **Calcul** |FAB6EB84-500B-4A09-A8CA-7358F8BBAEA5 |Base VM Size Hours |Minutes de mémoire à tores magnétiques virtuelle | Nombre de fois où le vcores minutes hello qu'exécution de la machine virtuelle |
| |9CD92D4C-BAFD-4492-B278-BEDC2DE8232A |Windows VM Size Hours |Minutes de mémoire à tores magnétiques virtuelle | Nombre de fois où le vcores minutes hello qu'exécution de la machine virtuelle |
| |6DAB500F-A4FD-49C4-956D-229BB9C8C793 |VM size hours |Heures de machine virtuelle |Capture à la fois la machine virtuelle de base et la machine virtuelle Windows. Ne s’ajuste pas en fonction des vcores |
| **Key Vault** | EBF13B9F-B3EA-46FE-BF54-396E93D48AB4 |Key Vault transactions | Nombre de requêtes en 10 000 s| Nombre de requêtes d’API REST reçues par le plan de données Key Vault |

## <a name="how-do-hello-azure-stack-usage-apis-compare-toohello-azure-usage-apihttpsmsdnmicrosoftcomlibraryazure1ea5b323-54bb-423d-916f-190de96c6a3c-currently-in-public-preview"></a>Comment hello API de l’utilisation de pile Azure comparer toohello [API de l’utilisation d’Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) (actuellement en version préliminaire publique) ?
* Hello API de locataires de l’utilisation est cohérent avec hello API Azure, à une exception près : hello *showDetails* indicateur actuellement n'est pas pris en charge dans la pile de Azure.
* Hello API d’utilisation du fournisseur s’applique uniquement tooAzure pile.
* Actuellement, hello [RateCard API](https://msdn.microsoft.com/en-us/library/azure/mt219004.aspx) qui est disponible dans Azure n’est pas disponible dans la pile de Azure.

## <a name="what-is-hello-difference-between-usage-time-and-reported-time"></a>Qu’est la différence hello entre a signalé une heure et d’utilisation ?
Les rapports de données d’utilisation comportent deux valeurs de durée principales :

* **Heure du rapport**. temps de Hello lors d’événement d’utilisation hello l'entrée système de d’utilisation de hello
* **Heure d’utilisation**. temps de Hello lorsque hello ressource de la pile d’Azure a été consommé

Vous pouvez voir une différence entre les valeurs Heure d’utilisation et Heure du rapport pour un événement d’utilisation spécifique. délai de Hello peut être aussi longue que plusieurs heures dans n’importe quel environnement.

Actuellement, vous pouvez interroger *uniquement par Heure du rapport*.

## <a name="what-do-these-usage-api-error-codes-mean"></a>Que signifient les codes d’erreur d’API d’utilisation suivants ?
| **Code d’état HTTP** | **Code d’erreur** | **Description** |
| --- | --- | --- |
| 400 - Demande incorrecte |*NoApiVersion* |Hello *api-version* paramètre de requête est manquant. |
| 400 - Demande incorrecte |*InvalidProperty* |Une propriété est manquante ou a une valeur non valide. message de type Hello dans le code d’erreur hello dans le corps de la réponse hello identifie hello propriété manquante. |
| 400 - Demande incorrecte |*RequestEndTimeIsInFuture* |Hello valeur pour *ReportedEndTime* est Bonjour futures. Valeurs Bonjour futures ne sont pas autorisées pour cet argument. |
| 400 - Demande incorrecte |*SubscriberIdIsNotDirectTenant* |Un appel d’API du fournisseur utilisé un ID d’abonnement qui n’est pas un client valid de l’appelant de hello. |
| 400 - Demande incorrecte |*SubscriptionIdMissingInRequest* |ID d’abonnement Hello de l’appelant de hello est manquant. |
| 400 - Demande incorrecte |*InvalidAggregationGranularity* |Une granularité d’agrégation non valide a été demandée. Les valeurs valides sont « quotidienne » et « horaire ». |
| 503 |*ServiceUnavailable* |Une erreur renouvelable s’est produite, car le service de hello est occupé ou appel de hello est limitée. |

## <a name="next-steps"></a>Étapes suivantes
[Facturation des clients et rétrofacturation dans Azure Stack](azure-stack-billing-and-chargeback.md)

[API d’utilisation des ressources de fournisseur](azure-stack-provider-resource-api.md)

[API d’utilisation des ressources de locataire](azure-stack-tenant-resource-usage-api.md)

