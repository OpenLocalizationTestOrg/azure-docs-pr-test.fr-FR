---
title: "aaaCreate un environnement Azure temps série Insights | Documents Microsoft"
description: "Dans ce didacticiel, vous allez apprendre comment toocreate environnement série, connectez-le tooan source d’événements et sont prêts à tooanalyze vos données d’événement en minutes."
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
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a>Créer un nouvel environnement de temps série Insights Bonjour portail Azure

Un environnement Time Series est une ressource Azure disposant d’une capacité d’entrée et de stockage. Clients fournir des environnements via hello portail Azure avec une capacité hello requis.

## <a name="steps-toocreate-hello-environment"></a>Environnement de hello toocreate étapes

Suivez ces étapes toocreate votre environnement :

1.  Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2.  Cliquez sur hello plus signe (« + ») dans hello angle supérieur gauche.
3.  Recherchez « Série un aperçu en temps » dans la zone de recherche hello.

  ![Création d’environnement d’un aperçu en temps série hello](media/get-started/getstarted-create-environment1.png)

4.  Sélectionnez « Time Series Insights », puis cliquez sur « Créer ».

  ![Créer groupe de ressources d’un aperçu en temps série hello](media/get-started/getstarted-create-environment2.png)

5.  Spécifiez le nom de l’environnement. Ce nom représente l’environnement hello dans [explorer de série heure](https://insights.timeseries.azure.com).
6.  Sélectionnez un abonnement. Choisissez celui qui contient votre source d’événement. Un aperçu en temps série peut détecter automatiquement Azure IoT Hub et les ressources de concentrateur d’événements existant dans hello même abonnement.
7.  Sélectionnez ou créez un groupe de ressources. Un groupe de ressources correspond à une collection de ressources Azure utilisées ensemble.
8.  Sélectionnez un emplacement d’hébergement. les centres de tooavoid déplacement des données entre les données, choisissez emplacement qui contient votre source d’événements.
9.  Sélectionnez un niveau tarifaire.
10. Sélectionnez la capacité. Vous pouvez modifier la capacité d’un environnement après sa création.
11. Créez votre environnement. Vous pouvez également épingler votre tableau de bord toohello environnement pour un accès aisé à chaque fois que vous vous connectez.

  ![Créer hello temps série Insights pin toodashboard](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>Étapes suivantes

* [Définir des stratégies d’accès aux données](time-series-insights-data-access.md) tooaccess votre environnement dans [temps série Insights portail](https://insights.timeseries.azure.com)
* [Créer une source d’événement](time-series-insights-add-event-source.md)
* [Envoyer des événements](time-series-insights-send-events.md) toohello source d’événement
