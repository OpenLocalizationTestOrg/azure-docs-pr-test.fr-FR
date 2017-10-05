---
title: "Ajouter une source d’événement à votre environnement Azure Time Series Insights | Microsoft Docs"
description: "Dans ce didacticiel, vous connectez une source d’événement à votre environnement Time Series Insights"
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
ms.openlocfilehash: ffa2eaf3680e68ac14aabf49b6308caeb173fd43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="df5cf-103">Créer une source d’événement pour votre environnement Time Series Insights à l’aide du portail Ibiza</span><span class="sxs-lookup"><span data-stu-id="df5cf-103">Create an event source for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="df5cf-104">La source d’événement Time Series Insights est dérivée d’un service Broker pour les événements tel que les concentrateurs d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="df5cf-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="df5cf-105">Time Series Insights se connecte directement aux sources d’événement, en recevant le flux de données sans demander aux utilisateurs d’écrire une seule ligne de code.</span><span class="sxs-lookup"><span data-stu-id="df5cf-105">Time Series Insights connects directly to Event Sources, ingesting the data stream without requiring users to write a single line of code.</span></span> <span data-ttu-id="df5cf-106">Actuellement, Time Series Insights prend en charge les concentrateurs d’événements Azure et les IoT Hubs.</span><span class="sxs-lookup"><span data-stu-id="df5cf-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="df5cf-107">À l’avenir, plusieurs sources d’événements seront ajoutées.</span><span class="sxs-lookup"><span data-stu-id="df5cf-107">In the future, more Event Sources will be added.</span></span>

## <a name="steps-to-add-an-event-source-to-your-environment"></a><span data-ttu-id="df5cf-108">Étapes pour ajouter une source d’événement à votre environnement</span><span class="sxs-lookup"><span data-stu-id="df5cf-108">Steps to add an event source to your environment</span></span>

1.  <span data-ttu-id="df5cf-109">Connectez-vous au [portail Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="df5cf-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="df5cf-110">Cliquez sur « Toutes les ressources » dans le menu de gauche du portail Ibiza.</span><span class="sxs-lookup"><span data-stu-id="df5cf-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3.  <span data-ttu-id="df5cf-111">Sélectionnez votre environnement Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="df5cf-111">Select your Time Series Insights environment.</span></span>

  ![Créer la source d’événement Time Series Insights](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="df5cf-113">Sélectionnez « Sources d’événement », puis cliquez sur « + Ajouter ».</span><span class="sxs-lookup"><span data-stu-id="df5cf-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Créer la source d’événement Time Series Insights - Détails](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="df5cf-115">Spécifiez le nom de la source d’événement.</span><span class="sxs-lookup"><span data-stu-id="df5cf-115">Specify the name of the event source.</span></span> <span data-ttu-id="df5cf-116">Ce nom est associé à tous les événements provenant de cette source d’événement et est disponible au moment de la requête.</span><span class="sxs-lookup"><span data-stu-id="df5cf-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="df5cf-117">Sélectionnez un concentrateur d’événements à partir de la liste des ressources du concentrateur d’événements de l’abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="df5cf-117">Select an event hub from the list of Event Hub resources in the current subscription.</span></span> <span data-ttu-id="df5cf-118">Sinon, choisissez l’option d’importation « Fournir des paramètres Event Hub manuellement » pour spécifier un concentrateur d’événements d’un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="df5cf-118">Otherwise choose import option "Provide Event Hub settings manually” to specify an event hub in another subscription.</span></span> <span data-ttu-id="df5cf-119">Les événements doivent être publiés au format JSON.</span><span class="sxs-lookup"><span data-stu-id="df5cf-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="df5cf-120">Sélectionnez la stratégie disposant de l’autorisation de lecture sur le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="df5cf-120">Select policy that has read permission in the event hub.</span></span>
8.  <span data-ttu-id="df5cf-121">Spécifiez un groupe de consommateurs du concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="df5cf-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="df5cf-122">Assurez-vous que ce groupe de consommateurs n’est pas utilisé par un autre service (par exemple, la tâche Stream Analytics ou un autre environnement Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="df5cf-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="df5cf-123">Si le groupe de consommateurs est utilisé par d’autres services, l’opération de lecture est affectée pour cet environnement et les autres services.</span><span class="sxs-lookup"><span data-stu-id="df5cf-123">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="df5cf-124">Si vous utilisez le groupe de consommateurs « $Default », ceci peut entraîner une réutilisation potentielle par d’autres lecteurs.</span><span class="sxs-lookup"><span data-stu-id="df5cf-124">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

9.  <span data-ttu-id="df5cf-125">Cliquez sur « Créer ».</span><span class="sxs-lookup"><span data-stu-id="df5cf-125">Click “Create.”</span></span>

<span data-ttu-id="df5cf-126">Après la création de la source d’événement, Time Series Insights démarre automatiquement la diffusion de données dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="df5cf-126">After creation of the event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df5cf-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df5cf-127">Next steps</span></span>

* <span data-ttu-id="df5cf-128">[Envoyer des événements](time-series-insights-send-events.md) à la source d’événement</span><span class="sxs-lookup"><span data-stu-id="df5cf-128">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="df5cf-129">Afficher votre environnement dans le [Portail Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="df5cf-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
