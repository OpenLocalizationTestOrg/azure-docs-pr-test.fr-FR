---
title: "aaaAdd un environnement de Azure temps série Insights événement source tooyour | Documents Microsoft"
description: "Dans ce didacticiel, vous vous connectez à un environnement de temps série Insights tooyour événement source"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Créer une source d’événements pour votre environnement d’un aperçu en temps série à l’aide du portail de Ibiza hello

La source d’événement Time Series Insights est dérivée d’un service Broker pour les événements tel que les concentrateurs d’événements Azure. Temps série Insights se connecte directement les Sources de tooEvent, absorber les flux de données hello sans nécessiter d’utilisateurs toowrite une seule ligne de code. Actuellement, Time Series Insights prend en charge les concentrateurs d’événements Azure et les IoT Hubs. Bonjour future, plusieurs Sources d’événements est ajoutés.

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a>Étapes tooadd un environnement de tooyour événement source

1.  Connectez-vous à toohello [portail Ibiza](https://portal.azure.com).
2.  Cliquez sur « Toutes les ressources » dans le menu hello hello situé à gauche du portail de Ibiza hello.
3.  Sélectionnez votre environnement Time Series Insights.

  ![Créer source d’événement hello temps série Insights](media/add-event-source/getstarted-create-event-source-1.png)

4.  Sélectionnez « Sources d’événement », puis cliquez sur « + Ajouter ».

  ![Créer la source d’événement de temps série Insights hello - détails](media/add-event-source/getstarted-create-event-source-2.png)

5.  Spécifiez le nom hello de source d’événements hello. Ce nom est associé à tous les événements provenant de cette source d’événement et est disponible au moment de la requête.
6.  Sélectionnez un concentrateur d’événements à partir de la liste hello des ressources de concentrateur d’événements dans l’abonnement actif de hello. Sinon choisissez option d’importation « paramètres du concentrateur d’événements fournir manuellement « toospecify un concentrateur d’événements dans un autre abonnement. Les événements doivent être publiés au format JSON.
7.  Sélectionnez la stratégie de lecture dans le concentrateur d’événements hello.
8.  Spécifiez un groupe de consommateurs du concentrateur d’événements.

  > [!IMPORTANT]
  > Assurez-vous que ce groupe de consommateurs n’est pas utilisé par un autre service (par exemple, une tâche Stream Analytics ou un autre environnement Time Series Insights). Si le groupe de consommateurs est utilisé par d’autres services, lisez opération affectée pour cet environnement et hello d’autres services. Si vous utilisez « $Default » en tant que groupe de consommateurs hello, il risque de réutilisation de toopotential par les autres lecteurs.

9.  Cliquez sur « Créer ».

Après la création d’une source d’événement hello, temps série Insights démarre automatiquement en continu des données dans votre environnement.

## <a name="next-steps"></a>Étapes suivantes

* [Envoyer des événements](time-series-insights-send-events.md) toohello source d’événement
* Afficher votre environnement dans le [Portail Time Series Insights](https://insights.timeseries.azure.com)
