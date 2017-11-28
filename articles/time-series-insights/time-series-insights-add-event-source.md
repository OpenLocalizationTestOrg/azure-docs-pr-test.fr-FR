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
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="0d98b-103">Créer une source d’événements pour votre environnement d’un aperçu en temps série à l’aide du portail de Ibiza hello</span><span class="sxs-lookup"><span data-stu-id="0d98b-103">Create an event source for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="0d98b-104">La source d’événement Time Series Insights est dérivée d’un service Broker pour les événements tel que les concentrateurs d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="0d98b-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="0d98b-105">Temps série Insights se connecte directement les Sources de tooEvent, absorber les flux de données hello sans nécessiter d’utilisateurs toowrite une seule ligne de code.</span><span class="sxs-lookup"><span data-stu-id="0d98b-105">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without requiring users toowrite a single line of code.</span></span> <span data-ttu-id="0d98b-106">Actuellement, Time Series Insights prend en charge les concentrateurs d’événements Azure et les IoT Hubs.</span><span class="sxs-lookup"><span data-stu-id="0d98b-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="0d98b-107">Bonjour future, plusieurs Sources d’événements est ajoutés.</span><span class="sxs-lookup"><span data-stu-id="0d98b-107">In hello future, more Event Sources will be added.</span></span>

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a><span data-ttu-id="0d98b-108">Étapes tooadd un environnement de tooyour événement source</span><span class="sxs-lookup"><span data-stu-id="0d98b-108">Steps tooadd an event source tooyour environment</span></span>

1.  <span data-ttu-id="0d98b-109">Connectez-vous à toohello [portail Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d98b-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="0d98b-110">Cliquez sur « Toutes les ressources » dans le menu hello hello situé à gauche du portail de Ibiza hello.</span><span class="sxs-lookup"><span data-stu-id="0d98b-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3.  <span data-ttu-id="0d98b-111">Sélectionnez votre environnement Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="0d98b-111">Select your Time Series Insights environment.</span></span>

  ![Créer source d’événement hello temps série Insights](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="0d98b-113">Sélectionnez « Sources d’événement », puis cliquez sur « + Ajouter ».</span><span class="sxs-lookup"><span data-stu-id="0d98b-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Créer la source d’événement de temps série Insights hello - détails](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="0d98b-115">Spécifiez le nom hello de source d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="0d98b-115">Specify hello name of hello event source.</span></span> <span data-ttu-id="0d98b-116">Ce nom est associé à tous les événements provenant de cette source d’événement et est disponible au moment de la requête.</span><span class="sxs-lookup"><span data-stu-id="0d98b-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="0d98b-117">Sélectionnez un concentrateur d’événements à partir de la liste hello des ressources de concentrateur d’événements dans l’abonnement actif de hello.</span><span class="sxs-lookup"><span data-stu-id="0d98b-117">Select an event hub from hello list of Event Hub resources in hello current subscription.</span></span> <span data-ttu-id="0d98b-118">Sinon choisissez option d’importation « paramètres du concentrateur d’événements fournir manuellement « toospecify un concentrateur d’événements dans un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0d98b-118">Otherwise choose import option "Provide Event Hub settings manually” toospecify an event hub in another subscription.</span></span> <span data-ttu-id="0d98b-119">Les événements doivent être publiés au format JSON.</span><span class="sxs-lookup"><span data-stu-id="0d98b-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="0d98b-120">Sélectionnez la stratégie de lecture dans le concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="0d98b-120">Select policy that has read permission in hello event hub.</span></span>
8.  <span data-ttu-id="0d98b-121">Spécifiez un groupe de consommateurs du concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0d98b-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0d98b-122">Assurez-vous que ce groupe de consommateurs n’est pas utilisé par un autre service (par exemple, une tâche Stream Analytics ou un autre environnement Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="0d98b-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="0d98b-123">Si le groupe de consommateurs est utilisé par d’autres services, lisez opération affectée pour cet environnement et hello d’autres services.</span><span class="sxs-lookup"><span data-stu-id="0d98b-123">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="0d98b-124">Si vous utilisez « $Default » en tant que groupe de consommateurs hello, il risque de réutilisation de toopotential par les autres lecteurs.</span><span class="sxs-lookup"><span data-stu-id="0d98b-124">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

9.  <span data-ttu-id="0d98b-125">Cliquez sur « Créer ».</span><span class="sxs-lookup"><span data-stu-id="0d98b-125">Click “Create.”</span></span>

<span data-ttu-id="0d98b-126">Après la création d’une source d’événement hello, temps série Insights démarre automatiquement en continu des données dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="0d98b-126">After creation of hello event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d98b-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d98b-127">Next steps</span></span>

* <span data-ttu-id="0d98b-128">[Envoyer des événements](time-series-insights-send-events.md) toohello source d’événement</span><span class="sxs-lookup"><span data-stu-id="0d98b-128">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="0d98b-129">Afficher votre environnement dans le [Portail Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="0d98b-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
