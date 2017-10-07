---
title: "fonctions de fenêtre d’Analytique aaaIntroduction tooStream | Documents Microsoft"
description: "En savoir plus sur les fonctions de fenêtre trois hello dans le flux de données Analytique (bascule, récurrente, glissante)."
keywords: "fenêtre bascule, fenêtre glissante, fenêtre récurrente"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a>Fonctions de fenêtre d’Analytique tooStream introduction
En temps réel plusieurs scénarios de diffusion en continu, il est nécessaire tooperform des opérations uniquement sur les données hello contenues dans les fenêtres temporelles. Prise en charge native pour les fonctions de fenêtrage est une fonctionnalité clé de l’Analytique de flux de données Azure qui déplace l’aiguille de hello sur la productivité des développeurs dans la création de tâches de traitement des flux de données complexes. Flux Analytique permet aux développeurs toouse [ **bascule**](https://msdn.microsoft.com/library/dn835055.aspx), [ **saut** ](https://msdn.microsoft.com/library/dn835041.aspx) et [ **décalé** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporelle les opérations de diffusion en continu de données. Il est important de noter que tous les [fenêtre](https://msdn.microsoft.com/library/dn835019.aspx) opérations produit des résultats à hello **fin** de fenêtre hello. sortie Hello de fenêtre hello sera un événement unique basé sur la fonction d’agrégation hello utilisée. événement de Hello aura hello horodatage de fin hello de fenêtre hello et toutes les fonctions de fenêtre sont définies avec une longueur fixe. Enfin, il est important toonote que toutes les fonctions de fenêtre doivent être utilisées dans un [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) clause.

![Concepts des fonctions de fenêtrage de Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a>Fenêtre bascule
Fonctions de fenêtre bascule sont toosegment utilisé un flux de données en segments de temps distinctes et exécutent une fonction contre eux, comme l’exemple hello ci-dessous. les principaux atouts de Hello d’une fenêtre bascule sont qu’ils répéter, ne se chevauchent pas et un événement ne peut pas appartenir toomore à une fenêtre bascule.

![Introduction aux fonctions de fenêtre bascule de Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a>Fenêtre récurrente
Les fonctions de fenêtre récurrente font des bonds d’une durée fixe dans le temps. Il peut être facilement toothink d'entre eux en tant que fenêtres bascules qui peuvent se chevaucher, les événements peuvent appartenir toomore à un jeu de résultats de la fenêtre saut. toomake une saut de fenêtre même hello comme une fenêtre bascule un spécifiez simplement toobe de taille de saut hello même hello en tant que taille de la fenêtre hello. 

![Introduction aux fonctions de fenêtre récurrente de Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a>Fenêtre glissante
Les fonctions de fenêtre glissante, à la différence des fenêtres bascules ou récurrentes, ne génèrent une sortie **que** lorsqu’un événement se produit. Chaque fenêtre aura au moins un événement et fenêtre hello en permanence avance par un € (epsilon). Comme les fenêtres récurrentes, les événements peuvent appartenir toomore à une fenêtre glissante.

![Introduction aux fonctions de fenêtre glissante de Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a>Obtenir de l’aide sur les fonctions de fenêtrage
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

