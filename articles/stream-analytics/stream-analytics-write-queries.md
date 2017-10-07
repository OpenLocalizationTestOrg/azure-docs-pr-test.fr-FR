---
title: "requêtes de toowrite aaaHow dans le flux de données Analytique | Documents Microsoft"
description: "Écrire des requêtes dans Stream Analytics et interroger des données | segment du parcours d’apprentissage."
keywords: "la façon dont les requêtes toowrite, interroger des données, écrivez une requête, l’écriture de requêtes"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a>Fonctionnement des requêtes dans le flux de données Analytique toowrite
L’écriture de requêtes pour le flux logique dans Azure flux Analytique de traitement est implémenté comme une « requête permanent » qui est définie avant un travail démarre et exécutés sur des données qu’il atteint le travail de hello. transformation des données Hello est exprimée dans un langage de requête de type SQL, qui est principalement un sous-ensemble T-SQL avec certaines ajouté comme des extensions de langage [fenêtrage](https://msdn.microsoft.com/library/azure/dn835019.aspx) utilisé tooexpress la sémantique temporel.

## <a name="writing-queries"></a>Écriture de requêtes :
1. Dans votre tâche Analytique de flux de données dans le portail de gestion Azure hello, cliquez sur **requête**.
   
    ![Sélection d'une requête](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    Bonjour portail Azure, cliquez sur **requête**.
   
    ![Sélection d’un aperçu de requête](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. Nouvelles tâches ont une toohelp de modèle de requête vous aideront à démarrer. requête Hello modèle effectue un « pass-through » de requête qui projette tous les champs à partir des événements d’entrée dans la sortie de hello.  
   
   * Si vous avez défini au moins une entrée et sortie pour votre travail, vous pouvez remplacer hello espace réservé « [YourOutputAlias] » et « [YourInputAlias] » champs avec des alias hello Hello d’entrée et sortie que vous souhaitez utiliser tout d’abord. En outre, vous pouvez toujours créer et tester votre requête Bonjour portail classique Azure sans définir des entrées et sorties sur le travail de hello.
   * Si vous le souhaitez tooperform davantage de traitement que direct simple, vous pouvez modifier la définition de la requête hello. tooget création de la requête, examinons certains des requêtes courantes de modèles sont capturés [ici](stream-analytics-stream-analytics-query-patterns.md).  
   
   ![Fenêtre Données de requête](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a>données de requête toovalidate fonctionne :
Vous pouvez vérifier que votre requête se comporte comme prévu en l’exécutant dans le navigateur de hello sur un ou plusieurs fichiers JSON locales contenant des données de test. Il ne sera pas démarrer le travail de hello ou avoir des conséquences de facturation.

> [!NOTE]
> Actuellement le test de la requête de dans le navigateur n’est pas pris en charge dans hello portail Azure.  
> 
> 

1. Assurez-vous qu’il n’y a aucune erreur de requête hello (sinon hello Test bouton est désactivé) puis cliquez sur le bouton de Test hello.  
   
   ![Test des données de requête](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. Vous serez fichiers toospecify demandées pour chacune des entrées hello référencées dans la requête de hello. Dans cet exemple, la requête de modèle hello est considérée comme-étant, boîte de dialogue hello demande pour une entrée nommée « yourinputalias ».  
   
   ![Tester les données de requête](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. Rechercher le fichier de test tooa. Plusieurs exemples de fichiers sont disponibles sur [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) et vous pouvez également récupérer des exemples de données à partir de vos propres entrées de flux de données via hello fonction d’exemples de données sur l’onglet d’entrées hello.  
   
   ![Entrée de requête](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. Après avoir fermé la boîte de dialogue hello, votre requête sera exécutée sur les données de test hello et vous verrez des résultats hello bas hello de page de la requête hello.  
   
   ![Résumé de la requête](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>Obtenir de l'aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

