---
title: "nouvelle tentative et la remise de grille d’événement aaaAzure"
description: "Décrit comment Azure Event Grid distribue des événements et gère les messages qui n’ont pas été distribués."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a>Distribution et nouvelle tentative de distribution de messages avec Azure Grid 

Cet article décrit comment Azure Event Grid gère les événements en l’absence d’accusé de réception d’une distribution.

Event Grid assure une distribution fiable. Il distribue chaque message au moins une fois pour chaque abonnement. Les événements sont immédiatement envoyés webhook toohello inscrit de chaque abonnement. Si un webhook ne confirme pas la réception d’un événement pendant 60 secondes de la remise hello première tentative, grille d’événement tentatives de remise d’événement de hello.

## <a name="message-delivery-status"></a>État de distribution du message

Grille d’événement utilise la réception de tooacknowledge de codes de réponse HTTP d’événements. 

### <a name="success-codes"></a>Codes de réussite

Hello des codes de réponse HTTP suivants indiquent qu’un événement a été remis tooyour webhook. Event Grid considère que la distribution est effectuée.

- 200 OK
- 202 Accepté

### <a name="failure-codes"></a>Codes d’échec

Hello suivant des codes de réponse HTTP indique l’échec de la tentative de remise d’un événement. Grille d’événement événements de hello toosend recommence. 

- 400 Demande incorrecte
- 401 Non autorisé
- 404 Introuvable
- 408 Délai d’expiration de la demande
- 414 URI trop long
- 500 Erreur interne du serveur
- 503 Service indisponible
- 504 Dépassement du délai de la passerelle

Tout autre code de réponse ou manque de réponse indique un échec. Event Grid effectue une nouvelle tentative de distribution. 

## <a name="retry-intervals"></a>Intervalles avant nouvelle tentative

Event Grid utilise une stratégie de nouvelle tentative d’interruption exponentielle pour la distribution des événements. Si votre webhook ne répond pas, ou retourne un code d’échec, grille d’événement tentatives de remise sur hello suivant planification :

1. 10 secondes
2. 30 secondes
3. 1 minute
4. 5 minutes
5. 10 minutes
6. 30 minutes
7. 1 heure

Grille d’événement ajoute une intervalles tooall randomisation petit.

## <a name="retry-duration"></a>Durée des nouvelles tentatives

Version d’évaluation hello grille d’événement Azure expire tous les événements qui ne sont pas remis dans les deux heures. Avant la disponibilité générale, cette heure sera accrue too24 heures. 

## <a name="next-steps"></a>Étapes suivantes

* Pour une introduction tooEvent grille, consultez [sur la grille d’événement](overview.md).
* tooquickly mise en route à l’aide de la grille d’événement, consultez [créer et itinéraire des événements personnalisés avec la grille d’événement Azure](custom-event-quickstart.md).
