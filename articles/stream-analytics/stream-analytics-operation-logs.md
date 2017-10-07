---
title: "aaaDebug à l’aide des journaux d’opération et de service dans le flux de données Analytique | Documents Microsoft"
description: "Flux de façon-toouse journaux Analytique"
keywords: journaux de service
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a>Débogage des travaux Stream Analytics à l’aide des journaux des opérations et de service
Tous les détails de toorecord toousers messages journalisation opérationnel de fourniture des services Azure liées toomanagement operations. Dans Azure Analytique de flux de données, ces informations peuvent être utilisées pour le débogage, telles que l’affichage État du travail, progression du travail et la défaillance messages tootrack hello progression d’une tâche au fil du temps, à partir du début tooprocessing toooutput.

## <a name="find-operation-logs-in-hello-azure-management-portal"></a>Rechercher les journaux des opérations dans le portail de gestion Azure hello
Les journaux des opérations sont accessibles de deux manières :  

* Tableau de bord de la tâche de flux de données Analytique hello  
* Services de gestion dans le portail Azure Classic de hello  

## <a name="dashboard-of-hello-stream-analytics-job"></a>Tableau de bord de la tâche de flux de données Analytique hello
Un toohello lien correspondant des journaux d’une tâche de flux de données Analytique est affiché sur l’onglet tableau de bord de la tâche hello. Si vous cliquez sur ce lien, elle définit les filtres hello de manière qu’elle affiche les derniers journaux pour cette tâche.

  ![Sélection des journaux des services de gestion](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a>Services de gestion
toomanually accédez toohello journaux d’opérations de flux de données Analytique et d’autres services dans le portail Azure Classic de hello :

1. Cliquez sur **des Services de gestion** Bonjour [portail Azure Classic](https://manage.windowsazure.com).
2. Sélectionnez **flux Analytique** pour **Type** et le nom hello hello du travail de pour **nom du Service**.  
   
   ![Sélection de Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a>Rechercher des journaux d’audit dans hello portail Azure
journaux des opérations toofind pour votre tâche de flux de données Analytique Bonjour portail Azure, cliquez sur **Parcourir** , puis sélectionnez **journaux d’Audit**.

  ![Sélection de Stream Analytics dans le portail Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

Un panneau d’affichage des 7 derniers jours pour toutes les ressources d’événements à partir de hello dans votre abonnement s’ouvre.  Vous pouvez filtrer les événements de toosee de spécifier le type ou de l’intervalle de temps en cliquant sur hello **filtre** commande.

  ![Sélection de Stream Analytics dans le portail Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a>Obtenir les détails d’un journal
Vous pouvez filtrer par plage de temps et les journaux de statut tooview hello pour votre travail.

Dans le portail de gestion Azure hello, cliquez sur hello **détails** bouton bas hello hello fenêtre tooview plus de détails sur un événement sélectionné. 

  ![Sélection des détails](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

Bonjour portail Azure, cliquez sur un toosee d’entrée de journal hello événements détaillés qu’il contient.

  ![Sélection des détails dans le portail Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

À partir de là, vous pouvez ouvrir hello **détail** panneau en cliquant sur les événements hello.

  ![Sélection des détails dans le portail Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a>Débogage d’une tâche ayant échoué
Dans le portail de gestion Azure hello, cliquez sur l’icône de recherche hello et tapez « échec ». Vous obtenez comme résultat tous les journaux avec des erreurs. 

  ![Débogage d'une tâche ayant échoué](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

Bonjour portail Azure, vous pouvez filtrer par niveau de message tooview **critique** événements.

  ![Débogage du portail Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

Vous pouvez sélectionner l’un des échecs de hello et cliquez sur hello **détails** pour plus d’informations sur l’erreur de hello.  Certains messages d’erreur fournissent des informations sur la façon dont toomitigate hello problème. 

  ![Détails de l'opération](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

En cas de besoin toocontact [prise en charge](https://azure.microsoft.com/support/options/) ou fournissez l’équipe de toohello informations via hello [forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), notez les détails de l’opération hello, spécifiquement hello **ID de corrélation**. 

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

