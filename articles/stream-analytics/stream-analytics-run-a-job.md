---
title: "toostart aaaHow travaux dans le flux de données Analytique de diffusion en continu | Documents Microsoft"
description: "Comment exécuter une tâche de diffusion en continu dans Azure Stream Analytics | segment du parcours d’apprentissage."
keywords: "diffusion en continu de tâches"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a>Comment toorun une diffusion en continu de la tâche dans Azure flux Analytique
Lorsqu’une tâche d’entrée, de requêtes et de sortie ont tous été spécifiés que vous pouvez démarrer la tâche de flux de données Analytique hello.

toostart votre travail :

1. Dans le portail Azure Classic hello, à partir du tableau de bord projet hello, cliquez sur **Démarrer** bas hello de page de hello.
   
   ![Bouton Démarrer la tâche](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   Bonjour portail Azure, cliquez sur **Démarrer** haut hello de votre page de travail.
   
   ![Bouton Démarrer le travail du portail Azure](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. Spécifiez un **démarrer une sortie** toodetermine valeur lors de la tâche commencera à générer une sortie. Hello paramètre par défaut pour les travaux qui n’ont pas déjà été démarré est **heure de début de tâche**, ce qui signifie que le travail hello démarre immédiatement le traitement des données. Vous pouvez également spécifier un **personnalisé** temps Bonjour passé (pour consommer des données d’historique) ou hello future (toodelay traitement jusqu'à une date future). Pour les cas où un travail a été démarré et arrêté, précédemment hello option **heure du dernier arrêt** est disponible dans la tâche de hello tooresume ordre à partir de hello dernière heure de sortie et d’éviter la perte de données.  
   
   ![Heure de démarrage de la tâche de diffusion en continu](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Heure de démarrage du travail de streaming dans le portail Azure](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. Confirmez votre sélection. état de la tâche Hello modifiera trop*départ* et déplacera peu trop*en cours d’exécution* une fois que le travail hello a démarré. Vous pouvez surveiller la progression hello Hello **Démarrer** opération Bonjour **Hub de Notification**:
   
   ![progression de la tâche de diffusion en continu](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Progression du travail de streaming dans le portail Azure](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>Obtenir de l'aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

