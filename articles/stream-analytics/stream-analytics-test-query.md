---
title: "test de la requête de flux de données Analytique aaaAzure | Documents Microsoft"
description: "Comment tootest vos requêtes dans les tâches de flux de données Analytique."
keywords: "test des requêtes, dépannage des requêtes"
documentation center: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a>Tester les requêtes Azure Stream Analytique Bonjour portail Azure

Avec Azure Analytique de flux de données, vous pouvez tester les requêtes Bonjour portail Azure sans avoir besoin de toostart ou arrêter un travail.

## <a name="test-hello-input"></a>Entrée de test hello

1. tootest avec des exemples de données d’entrée, cliquez sur un de vos entrées, puis sélectionnez **télécharger des exemples de données à partir du fichier**.

    ![Test des requêtes dans l’éditeur de requête Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. Une fois le téléchargement de hello est terminé, cliquez sur **Test** tootest cette requête sur hello les exemples de données que vous avez fourni.

    ![Exemple de données de test des requêtes dans l’éditeur de requête Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

sortie de Hello de votre requête s’affiche dans le navigateur hello, avec un lien de téléchargement de résultats si vous souhaitez que sortie de test toosave hello pour une utilisation ultérieure. Vous pouvez désormais facilement et de manière itérative modifiez votre requête et testez-le à plusieurs reprises toosee comment hello de sortie est modifiée.

![Exemple de sortie de l’éditeur de requête Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

Plusieurs sorties utilisé dans une requête, vous pouvez consulter les résultats hello pour les deux sorties séparément et basculer facilement entre eux.

Une fois que vous êtes satisfait des résultats hello indiquées dans le navigateur de hello, vous pouvez enregistrer votre requête, lancez votre tâche et laisser il traite les événements sans erreur.

## <a name="get-help"></a>Obtenir de l’aide

Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes

* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
