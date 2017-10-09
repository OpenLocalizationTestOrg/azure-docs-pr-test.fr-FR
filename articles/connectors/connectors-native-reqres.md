---
title: "actions de demande et de réponse aaaUse | Documents Microsoft"
description: "Vue d’ensemble de déclencheur de demande et de réponse hello et d’action dans une application Azure logique"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a>Prise en main des composants de demande et de réponse hello
À hello demande et réponse des composants d’une application logique, vous pouvez répondre en temps réel tooevents.

Vous pouvez par exemple afficher :

* Répondre demande HTTP de tooan avec des données à partir d’une base de données locale via une application logique.
* déclencher une application logique à partir d’un événement webhook externe ;
* appeler une application logique avec une action de requête et de réponse depuis une autre application logique.

tooget démarré à l’aide des actions de demande et de réponse hello dans une application logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-request-trigger"></a>Utilisez hello déclencheur de la requête HTTP
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail qui est défini dans une application logique. [En savoir plus sur les déclencheurs](connectors-overview.md).

Voici un exemple de séquence de la demande de tooset un HTTP Bonjour Concepteur de logique d’application.

1. Ajouter le déclencheur de hello **demande - HTTP lors de la demande est reçue** dans votre application logique. Vous pouvez éventuellement fournir un schéma JSON (à l’aide d’un outil tel que [JSONSchema.net](http://jsonschema.net)) pour le corps de la demande hello. Cela permet des jetons de concepteur toogenerate hello pour les propriétés dans la demande HTTP de hello.
2. Ajouter une autre action afin que vous puissiez enregistrer application logique de hello.
3. Après avoir enregistré l’application logique de hello, vous pouvez obtenir des URL de demande hello HTTP à partir de la carte de demande hello.
4. Une requête HTTP POST (vous pouvez utiliser un outil tel que [Postman](https://www.getpostman.com/)) déclencheurs d’URL toohello hello application logique.

> [!NOTE]
> Si vous ne définissez pas une action de réponse, une `202 ACCEPTED` réponse est retournée immédiatement toohello appelant. Vous pouvez utiliser hello réponse action toocustomize une réponse.
> 
> 

![Déclencheur de réponse](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a>Utilisez hello action de réponse HTTP
Hello action de réponse HTTP est valide uniquement lorsque vous l’utilisez dans un workflow qui est déclenché par une requête HTTP. Si vous ne définissez pas une action de réponse, une `202 ACCEPTED` réponse est retournée immédiatement toohello appelant.  Vous pouvez ajouter une action de réponse à une étape dans le flux de travail hello. Hello logique application conserve uniquement les demande entrante hello ouvert pendant une minute pour une réponse.  Après une minute, si aucune réponse n’a été envoyé à partir de flux de travail hello (et une action de réponse existe dans la définition de hello), un `504 GATEWAY TIMEOUT` est retourné à l’appelant de toohello.

Voici comment tooadd une action de réponse HTTP :

1. Sélectionnez hello **nouvelle étape** bouton.
2. Choisissez **Ajouter une action**.
3. Dans la zone de recherche action hello, tapez **réponse** hello de toolist action de réponse.
   
    ![Sélectionnez l’action de réponse hello](./media/connectors-native-reqres/using-action-1.png)
4. Ajoutez tous les paramètres qui sont requis pour le message de réponse HTTP hello.
   
    ![Action de réponse hello terminée](./media/connectors-native-reqres/using-action-2.png)
5. Cliquez sur le coin supérieur gauche de hello de toosave de barre d’outils hello et votre logique application est à la fois enregistrer et publier (activer).

## <a name="request-trigger"></a>Déclencheur de requête
Voici les détails de hello pour déclencheur hello qui prend en charge par ce connecteur. Il existe un seul déclencheur de requête.

| Déclencheur | Description |
| --- | --- |
| Demande |Se produit quand une requête HTTP est reçue |

## <a name="response-action"></a>Action de réponse
Voici les détails de hello pour action hello qui prend en charge par ce connecteur. Il existe une action de réponse unique qui est utilisable uniquement lorsqu’elle est accompagnée d’un déclencheur de requête.

| Action | Description |
| --- | --- |
| Réponse |Retourne qu'une réponse toohello mis en corrélation de demande HTTP |

### <a name="trigger-and-action-details"></a>Détail des déclencheurs et des actions
Hello tableaux suivants décrire les champs d’entrée de hello pour hello trigger et action et hello détails de sortie correspondants.

#### <a name="request-trigger"></a>Déclencheur de requête
Hello Voici un champ d’entrée pour le déclencheur hello à partir d’une demande HTTP entrante.

| Nom complet | Nom de la propriété | Description |
| --- | --- | --- |
| JSON Schema (Schéma JSON) |schema |schéma JSON Hello hello HTTP du corps de demande |

<br>

**Détails des résultats**

Hello Voici les détails de sortie pour la demande de hello.

| Nom de la propriété | Type de données | Description |
| --- | --- | --- |
| headers |objet |En-têtes de requête |
| Corps |objet |Objet Requête |

#### <a name="response-action"></a>Action de réponse
Hello Voici les champs d’entrée de hello action de réponse HTTP. Le symbole * désigne est un champ obligatoire.

| Nom complet | Nom de la propriété | Description |
| --- | --- | --- |
| Status Code (Code d’état)* |statusCode |Hello, code d’état HTTP |
| headers |headers |Un objet JSON de n’importe quel tooinclude d’en-têtes de réponse |
| Corps |body |corps de réponse Hello |

## <a name="next-steps"></a>Étapes suivantes
Maintenant, essayez de plate-forme de hello et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Vous pouvez Explorer hello tous les autres connecteurs disponibles dans les applications de la logique en consultant notre [liste des API](apis-list.md).

