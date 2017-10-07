---
title: "aaaSet des alertes pour les requêtes dans le flux de données Analytique | Documents Microsoft"
description: "Présentation des alertes Stream Analytics"
keywords: configurer des alertes
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
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>Configuration d’alertes pour des tâches Azure Stream Analytics
## <a name="introduction-monitor-page"></a>Introduction : page de surveillance
Vous pouvez définir des alertes tootrigger une alerte lorsqu’un indicateur atteint une condition que vous spécifiez. Par exemple, vous pouvez configurer une alerte pour une condition hello suivante :

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

Les règles peuvent être configurés sur des métriques via le portail de hello, ou peuvent être configurés [par programme](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) sur les données de journaux des opérations.

## <a name="set-up-alerts-in-hello-azure-portal"></a>Configurer des alertes dans hello portail Azure
1. Bonjour portail Azure, ouvrez hello flux Analytique travail toocreate une alerte pour. 

2. Bonjour **travail** panneau, cliquez sur hello **analyse** section.  

3. Bonjour **métrique** panneau, cliquez sur hello **ajouter une alerte** commande.

      ![Configuration du portail Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. Entrez un nom et une description.

5. Utilisez hello sélecteurs toodefine hello condition sous le hello alerte est envoyée.

6. Fournissent des informations sur où l’alerte de hello doit accéder.

      ![Configuration d’une alerte pour un travail Azure Stream Analytics](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

Pour plus d’informations sur la configuration des alertes dans hello portail Azure, consultez [recevoir des notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).  


## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-get-started.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

