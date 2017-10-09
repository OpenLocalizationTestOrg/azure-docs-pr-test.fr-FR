---
title: "les requêtes à l’aide de SELECT INTO aaaDebug Analytique de flux de données Azure | Documents Microsoft"
description: "Exemple de requête intermédiaire des données utilisant des instructions SELECT INTO dans Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>Déboguer des requêtes à l’aide des instructions SELECT INTO

Dans le traitement des données en temps réel, savoir quelles données hello il semble que la requête peut être utile dans le milieu de hello de hello. Étant donné que les entrées ou les étapes d’un travail Azure Stream Analytics peuvent être lues plusieurs fois, vous pouvez écrire des instructions SELECT INTO supplémentaires. Cela génère des données intermédiaires dans le stockage et vous permet d’inspecter l’exactitude hello de données de hello, tout comme *variables espionnes* feriez lorsque vous déboguez un programme.

## <a name="use-select-into-toocheck-hello-data-stream"></a>Utilisez SELECT INTO le flux de données hello toocheck

Hello exemple de requête suivant dans une tâche Analytique de flux de données Azure a un flux de données entrée, deux entrées de données de référence et une sortie de tooAzure le stockage de Table. Hello jointure de données à partir de concentrateur d’événements hello et deux objets BLOB tooget hello nom et la catégorie des informations de référence :

![Exemple de requête SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

Notez que les travaux hello sont en cours d’exécution, mais aucun événement n’est produites dans la sortie de hello. Sur hello **analyse** vignette, indiqué ici, vous pouvez voir que hello entrée qui produisent des données, mais vous ne savez pas quelle étape Hello **joindre** dû tous hello toobe événements supprimé.

![vignette de surveillance Hello](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
Dans ce cas, vous pouvez ajouter quelques supplémentaire les instructions SELECT INTO trop « ouvrir une session « résultats de la jointure intermédiaires hello et données hello qui sont lu à partir de l’entrée de hello.

Dans cet exemple, nous avons ajouté deux nouvelles « sorties temporaires ». Il peut s’agir du récepteur que vous voulez. Ici, nous utilisons Stockage Azure comme exemple :

![Ajout d’instructions SELECT INTO supplémentaires](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

Vous pouvez ensuite réécrire requête hello comme suit :

![Requête SELECT INTO réécrite](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

Maintenant redémarrer les travaux hello et laisser s’exécuter pendant quelques minutes. Requête puis temp1 et temp2 avec hello tooproduce de Visual Studio Cloud Explorer les tableaux suivants :

**table temp1**
![table temp1 SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**table temp2**
![table temp2 SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

Comme vous pouvez le voir, temp1 et temp2 disposent de données et colonne de nom hello est rempli correctement dans temporaire-2. Toutefois, étant donné qu’il n’y a toujours aucune donnée dans la sortie, quelque chose ne va pas :

![Table output1 SELECT INTO sans aucune donnée](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

En échantillonnant les données de salutation, vous pouvez être pratiquement certain que le problème de hello a avec hello seconde jointure. Vous pouvez télécharger des données de référence hello à partir de l’objet blob de hello et jeter un coup de œil :

![Table de référence SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

Comme vous pouvez le voir, format de hello Hello GUID dans ces données de référence est différent de format hello Hello [from] colonne temporaire-2. C’est pourquoi les données de salutation n’est pas arrivé dans output1 comme prévu.

Vous pouvez corriger le format de données hello, téléchargez-le tooreference blob et réessayez :

![Table temp SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

Cette fois-ci, données hello dans la sortie de hello sont mis en forme et remplies comme prévu.

![Table finale SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>Obtenir de l'aide

Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes

* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

