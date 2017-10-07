---
title: "génère des données de tooconfigure aaaHow pour les tâches de flux de données Analytique | Documents Microsoft"
description: "Configurer les sorties pour les tâches Stream Analytics | segment du parcours d’apprentissage."
keywords: "sortie de données, déplacement des données"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>Comment les données tooconfigure génère des tâches de flux de données Analytique

Les travaux de flux de données Analytique Azure peuvent être tooone connecté ou des sorties de données supplémentaires, qui définissent un récepteur de données connexion tooan existant. Lorsque votre tâche de flux de données Analytique traite et transforme les données entrantes, un flux de données d’événements de sortie est écrite la sortie de la tâche tooyour.

Sorties de flux de données Analytique peuvent être utilisé toosource de tableaux de bord en temps réel ou alertes, déclencheur les workflows de déplacement des données ou simplement les données d’archive pour la suite de traitement par lot. Stream Analytics bénéficie d'une intégration de première classe avec plusieurs services Azure, qui sont expliqués en détail ici.

tooadd une tâche de flux de données Analytique tooyour sortie :

1. Bonjour [portail Azure](https://portal.azure.com), ouvrez votre projet, cliquez sur **sorties** puis cliquez sur **ajouter** dans le panneau de sorties hello qui s’affiche.
   
    ![Ajout de sorties](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. Fournissez un nom convivial pour cette sortie Bonjour **Alias de sortie** boîte. Ce nom peut être utilisé dans la requête de votre travail plus tard sur toorefer toohello sortie.  
   
    Renseignez les autres hello hello requis connexion propriétés tooconnect tooyour sortie.  Ces champs varient selon le type de sortie et sont définis en détail ici.  
   
    ![Choisir le type de déplacement des données](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. Selon le type de sortie hello, vous devrez peut-être toospecify comment les données de salutation sont sérialisées ou mis en forme. paramètres de sérialisation spécifique Hello pour chaque type de sortie sont décrits ici.
   
    Renseignez les autres hello hello connexion requise propriétés tooconnect tooyour de source de données. Ces champs varient selon le type d’entrée et source de type et sont définies en détail dans hello [article de créer une tâche](stream-analytics-create-a-job.md).  

> [!Note]
>
> Une tâche d’ajouté toohello élément de sortie, doivent exister avant la tâche hello est démarrée et événements démarrer le flux. Par exemple, si vous utilisez le stockage d’objets Blob comme sortie, le travail de hello ne crée pas un compte de stockage automatiquement. Il doit toobe créé par l’utilisateur de hello avant le démarrage du travail ASA hello.
> 
 

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

