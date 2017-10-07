---
title: "aaaRate limitée pour SMS, des messages électroniques et de webhooks | Documents Microsoft"
description: "Comprendre comment Azure limite le nombre de hello des notifications de SMS, par courrier électronique ou webhook possibles à partir d’un groupe d’actions."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a>Limitation de la fréquence des SMS, e-mails et publications Webhook
Limitation du débit est une suspension de notifications qui se produit quand trop de notifications sont envoyées tooa téléphone particulier numéro ou adresse de messagerie. Elle garantit que les alertes sont faciles à gérer et exploitables.

règles de Hello pour SMS et par courrier électronique sont hello identiques. limite de seuil de taux Hello est la suivante :

 - **SMS** : 10 messages en une heure ;
 - **E-mail** : 100 messages en une heure.

## <a name="rate-limit-rules"></a>Règles de limitation de la fréquence
- Un numéro de téléphone particulier ou un e-mail est limitée lorsqu’il reçoit plus de messages que le seuil de hello permet de taux.
- Un numéro de téléphone ou une adresse de messagerie peut faire partie de groupes d’actions sur plusieurs abonnements. La limitation de la fréquence s’applique à tous les abonnements, Il s’applique dès que hello est atteint, même si les messages sont envoyés à partir de plusieurs abonnements.  
- Quand un numéro de téléphone ou un e-mail taux limitée, une notification supplémentaire est envoyée toocommunicate hello limitation du débit. Hello États lorsque hello limitation du débit de notification d’expiration.

## <a name="rate-limit-of-webhooks"></a>Limite de fréquence des Webhooks ##
Aucune limitation de la fréquence n’est appliquée aux Webhooks.

## <a name="next-steps"></a>Étapes suivantes ##
* En savoir plus sur le [comportement des alertes SMS](monitoring-sms-alert-behavior.md).
* Obtenir un [vue d’ensemble des alertes de journal d’activité](monitoring-overview-alerts.md)et découvrez comment tooreceive alertes.  
* Découvrez comment trop[configurer des alertes lors de la validation d’une notification de contrôle d’intégrité du service](monitoring-activity-log-alerts-on-service-notifications.md).
