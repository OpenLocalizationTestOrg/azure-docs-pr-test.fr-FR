---
title: "aaaUnderstanding analyse de flux de données Analytique travail | Documents Microsoft"
description: "Présentation de la surveillance des tâches Stream Analytics"
keywords: "surveillance des requêtes"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>Comprendre l’analyse de travail Analytique des flux de données et la manière dont les requêtes toomonitor

## <a name="introduction-hello-monitor-page"></a>Introduction : la page hello moniteur
Hello portail Azure, les deux mesures de performances clés qui peuvent être utilisé toomonitor et résoudre les problèmes de performances de vos requêtes et de travail de surface. toosee ces métriques, parcourir la tâche de flux de données Analytique toohello vous ne souhaitez afficher hello de vue et les métriques pour **analyse** section sur la page de vue d’ensemble de hello.  

![Lien Surveillance](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

fenêtre Hello s’affichent comme indiqué :

![Tableau de bord de surveillance des tâches](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Mesures disponibles pour Stream Analytics
| Mesure                 | Définition                               |
| ---------------------- | ---------------------------------------- |
| Utilisation de % d’unités de diffusion       | utilisation de Hello de hello ou les unités de diffusion en continu affecté tooa travail à partir de l’onglet échelle hello du travail de hello. Si cet indicateur atteint 80 % ou plus, il est fort probable que le traitement des événements soit retardé ou arrêté. |
| Événements d’entrée           | Quantité de données reçues par tâche de flux de données Analytique hello, dans le nombre d’événements. Cela peut être utilisé toovalidate que les événements sont envoyés toohello des sources d’entrée. |
| Événements de sortie          | Quantité de données envoyées par hello flux Analytique toohello sortie cible du travail, dans le nombre d’événements. |
| Événements non ordonnés    | Nombre d’événements reçus dans le désordre qui ont été supprimés ou dont un horodatage ajusté, en fonction de hello stratégie de classement des événements. Cela peut être touché par configuration hello du paramètre de la fenêtre de tolérance de panne de hello. |
| Erreurs de conversion de données | Nombre d’erreurs de conversion de données générées par une tâche Stream Analytics. |
| Erreurs d’exécution         | Nombre total de Hello d’erreurs qui se produisent pendant l’exécution d’une tâche de flux de données Analytique. |
| Événements d’entrée tardifs      | Nombre d’événements entrants au plus tard à partir de la source de hello qui soit ont été abandonnés ou leur horodatage a été ajusté, selon la configuration de stratégie de classement des événements hello du paramètre de fenêtre de tolérance d’arrivée tardive hello. |
| Requêtes de fonction      | Nombre d’appels toohello fonction Azure Machine Learning (le cas échéant). |
| Requêtes de fonction ayant échoué | Nombre d’appels à la fonction Azure Machine Learning ayant échoué (le cas échéant). |
| Événements de fonction        | Nombre d’événements envoyés fonction d’Azure Machine Learning toohello (le cas échéant). |
| Octets des événements d’entrée      | Quantité de données reçues par la tâche de flux de données Analytique hello, en octets. Cela peut être utilisé toovalidate que les événements sont envoyés toohello des sources d’entrée. |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>Personnalisation de surveillance Bonjour portail Azure
Vous pouvez ajuster le type hello du graphique, les métriques affichées et la période dans les paramètres de modifier le graphique de hello. Pour plus d’informations, consultez [comment tooCustomize analyse](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

  ![Graphique représentant le temps de surveillance des requêtes](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>Obtenir de l'aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

