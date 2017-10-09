---
title: "déclencheur de périodicité aaaAdd hello dans les applications logique | Documents Microsoft"
description: "Vue d’ensemble du déclencheur de périodicité hello et comment toouse avec une application Azure logique."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a>Prise en main déclencheur de périodicité hello
À l’aide de déclencheur de périodicité hello, vous pouvez créer puissants flux de travail dans le cloud de hello.

Vous pouvez par exemple afficher :

* Planifier un toorun de flux de travail une procédure stockée SQL tous les jours.
* Envoyer par courrier électronique un résumé de tous les tweet dans hello sur une certaine #sqlhelp la semaine dernière.

tooget démarré à l’aide de déclencheur de périodicité hello dans une application logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Utilisation d’un déclencheur de périodicité
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail qui est défini dans une application logique. [En savoir plus sur les déclencheurs](connectors-overview.md).

Voici un exemple de séquence de comment déclencher des tooset d’une périodicité dans une application de logique :

1. Ajouter hello **périodicité** déclencheur en tant que première étape de hello dans une application logique.
2. Renseignez les paramètres hello hello intervalle de périodicité.

application de la logique de Hello commence désormais une exécution après chaque intervalle de temps.

![Déclencheur HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Détails du déclencheur
déclencheur de périodicité Hello a hello propriétés que vous pouvez configurer suivantes.

Il déclenche une application logique après un intervalle de temps spécifié.
A * désigne est un champ obligatoire.

| Nom complet | Nom de la propriété | Description |
| --- | --- | --- |
| Frequency (Fréquence)* |frequency |unité de Hello de temps : `Second`, `Minute`, `Hour`, `Day`, ou `Year`. |
| Interval (Intervalle)* |interval |intervalle de salutation Hello attribué à la fréquence de récurrence de hello. |
| Time Zone (Fuseau horaire) |timeZone |Si une heure de début (startTime) est spécifiée sans décalage UTC, ce fuseau horaire est utilisé. |
| Heure de début |startTime |heure de début Hello [format ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Étapes suivantes
Maintenant, essayez de plate-forme de hello et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Vous pouvez Explorer hello tous les autres connecteurs disponibles dans les applications de la logique en consultant notre [liste des API](apis-list.md).

