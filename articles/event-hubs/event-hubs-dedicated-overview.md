---
title: "aaaOverview de la capacité de dédiée de concentrateurs d’événements Azure | Documents Microsoft"
description: "Vue d’ensemble de la capacité Azure Event Hubs Dedicated."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 79c09975e5c0a6d4729c8f836576770abaaf322e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-event-hubs-dedicated"></a>Vue d’ensemble d’Event Hubs Dedicated

*Dédié des concentrateurs d’événements* capacité offre des déploiements de locataire unique pour les clients avec hello exigences plus strictes. À l’échelle complète, Azure Event Hubs peut entrée plus de 2 millions d’événements par seconde ou too2 en Go par seconde de télémétrie avec une latence de stockage et la seconde une durabilité complète. Ce également permet aux solutions intégrées par le traitement en temps réel et le lot sur hello même système. Par l’archivage des concentrateurs d’événements inclus dans l’offre de hello, vous pouvez réduire la complexité de hello de votre solution en ayant un seul flux prend en charge les pipelines en temps réel et en fonction de traitement par lots.

Hello tableau suivant compare les niveaux de service disponible hello des concentrateurs d’événements. offre de Hello dédié des concentrateurs d’événements est un coût mensuel fixe, toousage comparé pour la plupart des fonctionnalités de Basic Standard et la tarification. couche de dédié Hello offre des fonctionnalités de hello de plan Standard de hello, mais avec une capacité de mise à l’échelle d’entreprise pour les clients avec des charges de travail exigeantes. 

| Fonctionnalité | De base | Standard | Dédié |
| --- |:---:|:---:|:---:|
| Événements d’entrée | Paiement par million d’événements | Paiement par million d’événements | Inclus |
| Unité de débit (1 Mo/s en entrée, 2 Mo/s en sortie) | Paiement par heure | Paiement par heure | Inclus |
| Taille des messages | 256 KB | 256 KB | 1 Mo |
| Stratégies d’éditeur | N/A | Oui | Oui |     
| Groupes de consommateurs | 1 - par défaut | 20 | 20 |
| Relecture des messages | Oui | Oui | Oui |
| Unités de débit maximales | 20 | 20 (too100 flexible)  | 1 unité de capacité≈200 |
| Connexions réparties | 100 inclus | 1 000 inclus | 100 K inclus |
| Connexions négociées supplémentaires | N/A | Oui | Oui |
| Rétention des messages | 1 jour inclus | 1 jour inclus | Jours d’activité too7 inclus |
| Archive (version préliminaire) | N/A   | Paiement par heure | Inclus |

## <a name="benefits-of-event-hubs-dedicated-capacity"></a>Avantages de la capacité Event Hubs Dedicated

Hello avantages suivants est disponible lorsque vous utilisez dédié des concentrateurs d’événements :

* Hébergement à locataire unique ne subissant pas le bruit d’autres locataires.
* La taille augmente too1 Mo par rapport de message Ko too256 pour Standard et de base.
* Performances reproductibles chaque fois.
* Garantie toomeet capacité que votre croissance a besoin.
* Évolutive entre 1 et les unités de capacité 8 (CU) : en fournissant des événements d’entrée millions too2 par seconde.
  * Nalisée gérer la montée en puissance hello pour l’événement concentrateurs dédié, où chaque CU peut fournir environ hello équivalent 200 unités de débit (CO).
* Aucune maintenance : nous gérons l’équilibrage de la charge, les mises à jour du système d’exploitation, les correctifs de sécurité et le partitionnement.
* Tarification mensuelle fixe.

Dédié des concentrateurs d’événements supprime également certaines des limitations de débit hello de l’offre Standard de hello. Unités de débit dans les niveaux de base et Standard vous donne droit too1000 des événements par seconde ou 1 Mo par seconde de l’entrée par co et double cette quantité de sortie. offre de mise à l’échelle dédié Hello n’impose aucune restriction en entrée et compte les événements de sortie. Ces limites sont régies uniquement par hello Hello acheté des concentrateurs d’événements de la capacité de traitement.

Ce service est destiné aux utilisateurs de télémétrie de plus grande hello et toocustomers disponibles avec un contrat entreprise.

## <a name="how-tooonboard"></a>Comment tooonboard

plateforme de Hello dédié des concentrateurs d’événements est proposée via un contrat d’entreprise avec différentes tailles de Nalisée. Chaque CU fournit environ hello équivalent 200 unités de débit. Vous pouvez faire évoluer votre capacité vers le haut ou vers le bas dans l’ensemble de hello mois toomeet vos besoins en ajoutant ou supprimant Nalisée. plan de dédié Hello est unique, vous rencontrerez une intégration plus pratique de hello concentrateurs d’événements produit équipe tooget hello déploiement flexible qui vous convient. 

## <a name="next-steps"></a>Étapes suivantes
Contactez votre responsable de compte Microsoft ou le Support technique de Microsoft tooget des détails supplémentaires sur la capacité dédié de concentrateurs d’événements. Vous pouvez également plus d’informations sur concentrateurs d’événements en visitant hello suivant liens :

Pour plus d’informations sur la tarification, visitez hello suivant liens :

- [Tarification d’Event Hubs Dedicated](https://azure.microsoft.com/pricing/details/event-hubs/). Vous pouvez également contacter votre responsable de compte Microsoft ou le Support technique de Microsoft tooget des détails supplémentaires sur la capacité de dédié des concentrateurs d’événements.
- Hello [FAQ de concentrateurs d’événements](event-hubs-faq.md) contient des informations sur la tarification et répond à certaines questions fréquemment posées sur les concentrateurs d’événements. 
