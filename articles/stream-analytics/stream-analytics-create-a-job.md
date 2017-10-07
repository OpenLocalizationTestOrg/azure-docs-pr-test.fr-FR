---
title: "aaaHow toocreate un travail de traitement de données analytique pour les flux de données Analytique | Documents Microsoft"
description: "Créer une tâche de traitement d’analyse de données pour Stream Analytics | segment du parcours d’apprentissage."
keywords: "traitement d’analyse de données"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a>Comment toocreate un traitement analytique des données de la tâche de flux de données Analytique
ressources de niveau supérieur Hello dans Analytique de flux de données Azure est une tâche Analytique de flux de données.  Il se compose d’une ou plusieurs d’entrée à des sources de données, une requête exprimant la transformation de données hello et une ou plusieurs cibles de sortie qui sont écrits dans. Ensemble, ces activer analytique de données hello utilisateur tooperform scénarios de traitement des données de diffusion en continu.

toostart à l’aide de flux de données Analytique, commencez par créer une nouvelle tâche de flux de données Analytique.  Notez que cette action n’a aucune incidence facturation jusqu'à ce que la tâche hello est démarrée.

1. Connectez-vous à hello en ligne [portail Azure classic](http://manage.windowsazure.com) ou hello [portail Azure](https://portal.azure.com/).
2. Dans le portail de hello : **cliquez sur Nouveau**, puis cliquez sur **Data Services** ou **données Analytique** en fonction de votre portail et le puis cliquez sur **Analytique de flux de données Azure** ou **flux Analytique** , puis **création rapide**.
   
   ![Assistant Tâche de traitement d’analyse de données](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Créer une tâche de traitement d’analyse de données](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. Spécifiez la configuration souhaitée de hello de la tâche de flux de données Analytique de hello.
   
   * Bonjour **nom de la tâche** , entrez un nom tooidentify hello Analytique de flux du travail. Hello lorsque **nom de la tâche** est validé, une coche verte s’affiche dans la zone de nom de la tâche hello. Hello **nom de la tâche** peuvent uniquement contenir des caractères alphanumériques et hello '-' caractère et doit être comprise entre 3 et 63 caractères.
   * Utilisez **région** Bonjour portail Azure ou **emplacement** Bonjour Azure toospecify portail hello emplacement géographique où vous souhaitez que le travail de hello de toorun.
   * Si à l’aide de hello le portail Azure, sélectionnez ou créez un toouse de compte de stockage comme hello **compte de stockage de surveillance régionale**. Ce compte de stockage est utilisé toostore données d’analyse de toutes les tâches de flux de données Analytique en cours d’exécution dans cette région.
   * Si à l’aide de hello le portail Azure, spécifiez un nouveau ou existant **groupe de ressources** toohold liés des ressources pour votre application.
4. Une fois les nouvelles options de tâche de flux Analytique hello sont configurées, cliquez sur **créer une tâche de flux de données Analytique**. Il peut prendre quelques minutes pour hello flux Analytique travail toobe est créé. état de hello toocheck, vous pouvez surveiller la progression de hello dans hub de Notifications hello.
   
   ![Hub de notification des tâches de traitement d’analyse de données](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Créer une tâche de traitement d’analyse de données dans le portail Azure](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. nouvelle tâche de Hello présentent l’état de **créé**. Notez que hello **Démarrer** bouton est désactivé. Configurer hello travail entrée, de requête et de sortie avant de démarrer le travail de hello.
   
   ![Statut de la tâche de traitement d’analyse de données](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Statut de la tâche de traitement d’analyse de données dans le portail Azure](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

