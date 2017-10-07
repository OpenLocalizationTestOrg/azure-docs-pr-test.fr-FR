---
title: "action de requête aaaAdd hello dans les applications logique | Documents Microsoft"
description: "Vue d’ensemble de l’action de requête hello pour effectuer des actions comme tableau de filtre."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a>Prise en main avec l’action de requête hello
En utilisant l’action de requête de hello, vous pouvez utiliser des flux de travail de lots et de tableaux tooaccomplish à :

* Créer une tâche pour tous les enregistrements à priorité élevée à partir d’une base de données.
* Enregistrer toutes les pièces jointes PDF pour les messages électroniques dans l’objet blob Azure.

tooget démarré à l’aide d’action de requête hello dans une application logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-query-action"></a>Utilisez l’action de requête hello
Une action est une opération est effectuée par le flux de travail hello défini dans une application logique. [En savoir plus sur les actions](connectors-overview.md).  

action de requête Hello a actuellement une opération appelée tableau de filtre hello, qui est exposé dans le Concepteur de hello. Cela vous permet de tooquery un tableau et retourner un jeu de résultats filtrés.

Voici comment vous pouvez l’ajouter dans une application logique :

1. Sélectionnez hello **nouvelle étape** bouton.
2. Choisissez **Ajouter une action**.
3. Dans la zone de recherche action hello, tapez **filtre** hello de toolist **tableau de filtre** action.
   
    ![Sélectionnez l’action de requête hello](./media/connectors-native-query/using-action-1.png)
4. Sélectionnez un tableau toofilter. (hello capture d’écran suivante montre hello tableau de résultats de la recherche Twitter.)
5. Créer une condition tooevaluate sur chaque élément. (hello suivant capture d’écran de filtres tweet d’utilisateurs disposant de plus de 100 barreaux.)
   
    ![Action de requête hello terminée](./media/connectors-native-query/using-action-2.png)
   
    action de Hello produira un nouveau tableau qui contient uniquement les résultats répondant aux exigences de filtre hello.
6. Cliquez sur le coin supérieur gauche de hello de toosave de barre d’outils hello et votre logique application est à la fois enregistrer et publier (activer).

## <a name="query-action"></a>Action de requête
Voici les détails de hello pour action hello qui prend en charge par ce connecteur. connecteur de Hello possède une seule action possible.

| Action | Description |
| --- | --- |
| Filtrer le tableau |Évalue une condition pour chaque élément dans un tableau et retourne les résultats de hello |

## <a name="action-details"></a>Détails de l’action
action de requête Hello est fourni avec une seule action possible. Hello tableaux suivants décrivent hello requis et les champs d’entrée facultatifs pour action de hello et détails sortie correspondants hello qui sont associés à l’aide d’action de hello.

### <a name="filter-array"></a>Filtrer le tableau
Hello Voici les champs d’entrée pour l’action hello, qui effectue une requête de sortie HTTP.
Le symbole * désigne est un champ obligatoire.

| Nom complet | Nom de la propriété | Description |
| --- | --- | --- |
| De* |from |Hello tableau toofilter |
| Condition* |où |Hello tooevaluate condition pour chaque élément. |

<br>

### <a name="output-details"></a>Détails des résultats
Hello Voici les détails de sortie de réponse HTTP de hello.

| Nom de la propriété | Type de données | Description |
| --- | --- | --- |
| Tableau filtré |array |Tableau contenant un objet pour chaque résultat filtré |

## <a name="next-steps"></a>Étapes suivantes
Maintenant, essayez de plate-forme de hello et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Vous pouvez Explorer hello tous les autres connecteurs disponibles dans les applications de la logique en consultant notre [liste des API](apis-list.md).

