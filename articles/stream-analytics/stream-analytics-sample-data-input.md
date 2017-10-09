---
title: "entrées d’échantillonnage aaa Analytique de flux de données Azure | Documents Microsoft"
description: "Identifiez les problèmes lors du dépannage des travaux Stream Analytics."
keywords: "résoudre les problèmes d’entrée, échantillonnage des entrées"
documentationcenter: 
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
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a>Échantillonnage de flux d’entrée Azure Stream Analytics

À l’aide d’Analytique de flux de données Azure, vous pouvez échantillonner des événements d’entrée qui proviennent d’un fichier et de tester les requêtes dans le portail de hello sans avoir besoin de toostart ou d’arrêter un travail.

## <a name="testing-your-query"></a>Test de votre requête

Dans le volet d’informations travail hello Analytique de flux de données, ouvrez hello **l’éditeur de requête** panneau en cliquant sur le nom de la requête hello sous **requête**. (Dans notre exemple de scénario, car aucune requête n’a encore été créé, cliquez sur hello **< >** espace réservé.)

![éditeur de requête de flux de données Analytique Hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

panneau d’éditeur enrichi Hello pour la création de votre requête s’affiche telle qu’elle était dans la version précédente de hello. Maintenant le panneau de hello a été mis à jour avec un nouveau volet gauche qui affiche hello entrées et les sorties qui sont utilisées par la requête de hello et définis pour cette tâche.

![éditeur de requête de flux de données Analytique Hello les entrées et sorties des listes](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

Sont également affichées une entrée et une sortie supplémentaires, qui ne sont pas définies. Elles proviennent de hello modèle de requête avec laquelle vous démarrez. Ils modifient ou disparaissent complètement, lorsque vous modifiez la requête de hello. Vous pouvez ignorer ces erreurs pour l’instant.

tootest avec des exemples de données d’entrée, cliquez sur un de vos entrées, puis sélectionnez **télécharger des exemples de données à partir du fichier**.

![Hello flux Analytique éditeur téléchargement exemple interroge les données de fichier (commande)](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

Une fois le téléchargement de hello est terminé, cliquez sur **Test** tootest cette requête sur hello exemples de données que vous avez fournies.

![bouton Test éditeur Hello Analytique de flux de requête](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

Si vous souhaitez que les résultats des tests toosave hello pour une utilisation ultérieure, sortie hello de votre requête s’affiche dans le navigateur hello avec un résultats du téléchargement toohello lien. Vous pouvez désormais facilement et de manière itérative modifiez votre requête et testez-le à plusieurs reprises toosee comment hello de sortie est modifiée.

![Exemple de sortie de l’éditeur de requête Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

Bonjour précédant l’image, une deuxième sortie a été ajoutée, appelée **HighAvgTempOutput**.

Lorsque vous utilisez plusieurs sorties dans une requête, vous pouvez voir les résultats de hello pour chaque sortie séparément et basculer facilement entre eux.

Une fois que vous êtes satisfait des résultats de hello, vous pouvez enregistrer votre requête, lancez votre tâche, confortablement et regardez magic hello de flux de données Analytique.

## <a name="get-help"></a>Obtenir de l’aide

Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
