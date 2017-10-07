---
title: "un retard dans les applications de la logique d’aaaAdd | Documents Microsoft"
description: "Vue d’ensemble de hello délai et le délai-jusqu'à ce que les actions et comment toouse avec une application Azure logique."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a>Prise en main hello délai et le délai-jusqu'à ce que les actions
À l’aide du délai de hello et « délai-jusqu'à ce que « actions, vous pouvez effectuer les scénarios de flux de travail.

Vous pouvez par exemple afficher :

* Attendez un toosend jour ouvrable un état de mise à jour par e-mail.
* Workflow de hello délai jusqu'à ce qu’un appel HTTP a toofinish de temps avant la reprise et de récupérer les résultats de hello.

tooget démarré à l’aide de retarder l’action hello dans une application logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-delay-actions"></a>Utiliser des actions de retard hello
Une action est une opération est effectuée par le flux de travail hello défini dans une application logique. [En savoir plus sur les actions](connectors-overview.md).

Voici un exemple de séquence de comment toouse un délai étape dans une application de logique :

1. Après l’ajout d’un déclencheur, cliquez sur **nouvelle étape** tooadd une action.
2. Recherchez **délai** toobring des actions de retard hello. Dans cet exemple, nous sélectionnons **Retarder**.
   
    ![Action Retarder](./media/connectors-native-delay/using-action-1.png)
3. Effectuez l’une de retard de hello action propriétés tooconfigure hello.
   
    ![Configuration du retard](./media/connectors-native-delay/using-action-2.png)
4. Cliquez sur **enregistrer** toopublish et activer l’application de la logique de hello.

## <a name="action-details"></a>Détails de l’action
déclencheur de périodicité Hello a hello suivant des propriétés qui peuvent être configurées.

### <a name="delay-action"></a>Action Retarder
Cette hello de retards action exécutée pour un intervalle de temps donné.
Le symbole * désigne est un champ obligatoire.

| Nom complet | Nom de la propriété | Description |
| --- | --- | --- |
| Count* |count |nombre de Hello de toodelay d’unités de temps |
| Unit* |unité |unité de Hello de temps : `Second`, `Minute`, `Hour`, ou`Day` |

<br>

### <a name="delay-until-action"></a>Action Retarder jusqu'à
Cette action retarde hello exécuter jusqu'à une date/heure spécifiée.
Le symbole * désigne est un champ obligatoire.

| Nom complet | Nom de la propriété | Description |
| --- | --- | --- |
| Year* |timestamp |Hello année toodelay jusqu'à (GMT) |
| Month* |timestamp |Hello mois toodelay jusqu'à (GMT) |
| Day* |timestamp |Hello jour toodelay jusqu'à (GMT) |

<br>

## <a name="next-steps"></a>Étapes suivantes
Maintenant, essayez de plate-forme de hello et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Vous pouvez Explorer hello tous les autres connecteurs disponibles dans les applications de la logique en consultant notre [liste des API](apis-list.md).

