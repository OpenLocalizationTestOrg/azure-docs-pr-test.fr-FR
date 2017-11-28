---
title: "Créer un environnement Azure Time Series Insights | Microsoft Docs"
description: "Dans ce didacticiel, vous allez découvrir comment créer un environnement Time Series, le connecter à une source d’événement et le préparer à analyser vos données d’événement en quelques minutes."
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
ms.openlocfilehash: eb710795916a2d7beea75a6408a0982fb4dc8750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-time-series-insights-environment-in-the-azure-portal"></a><span data-ttu-id="5947a-103">Créer un nouvel environnement de Time Series Insights dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5947a-103">Create a new Time Series Insights environment in the Azure portal</span></span>

<span data-ttu-id="5947a-104">Un environnement Time Series est une ressource Azure disposant d’une capacité d’entrée et de stockage.</span><span class="sxs-lookup"><span data-stu-id="5947a-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="5947a-105">Les clients approvisionne des environnements via le portail Azure avec la capacité requise.</span><span class="sxs-lookup"><span data-stu-id="5947a-105">Customers provision environments via the Azure portal with the required capacity.</span></span>

## <a name="steps-to-create-the-environment"></a><span data-ttu-id="5947a-106">Étapes pour créer l’environnement</span><span class="sxs-lookup"><span data-stu-id="5947a-106">Steps to create the environment</span></span>

<span data-ttu-id="5947a-107">Procédez comme suit pour créer votre environnement :</span><span class="sxs-lookup"><span data-stu-id="5947a-107">Follow these steps to create your environment:</span></span>

1.  <span data-ttu-id="5947a-108">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5947a-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="5947a-109">Cliquez sur le signe plus (« + ») dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="5947a-109">Click the plus sign (“+”) in the top left corner.</span></span>
3.  <span data-ttu-id="5947a-110">Recherchez « Time Series Insights » dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="5947a-110">Search for “Time Series Insights” in the search box.</span></span>

  ![Créer l’environnement Time Series Insights](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="5947a-112">Sélectionnez « Time Series Insights », puis cliquez sur « Créer ».</span><span class="sxs-lookup"><span data-stu-id="5947a-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Créer le groupe de ressources Time Series Insights](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="5947a-114">Spécifiez le nom de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="5947a-114">Specify environment name.</span></span> <span data-ttu-id="5947a-115">Ce nom représente l’environnement dans l’[explorateur time series](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5947a-115">This name will represent the environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="5947a-116">Sélectionnez un abonnement.</span><span class="sxs-lookup"><span data-stu-id="5947a-116">Select a subscription.</span></span> <span data-ttu-id="5947a-117">Choisissez celui qui contient votre source d’événement.</span><span class="sxs-lookup"><span data-stu-id="5947a-117">Choose one that contains your event source.</span></span> <span data-ttu-id="5947a-118">Time Series Insights peut détecter automatiquement les ressources Azure IoT Hub et Concentrateur d’événements existant dans le même abonnement.</span><span class="sxs-lookup"><span data-stu-id="5947a-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in the same subscription.</span></span>
7.  <span data-ttu-id="5947a-119">Sélectionnez ou créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5947a-119">Select or create a resource group.</span></span> <span data-ttu-id="5947a-120">Un groupe de ressources correspond à une collection de ressources Azure utilisées ensemble.</span><span class="sxs-lookup"><span data-stu-id="5947a-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="5947a-121">Sélectionnez un emplacement d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="5947a-121">Select a hosting location.</span></span> <span data-ttu-id="5947a-122">Pour éviter de déplacer des données entre des centres de données, choisissez l’emplacement qui contient votre source d’événement.</span><span class="sxs-lookup"><span data-stu-id="5947a-122">To avoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="5947a-123">Sélectionnez un niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="5947a-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="5947a-124">Sélectionnez la capacité.</span><span class="sxs-lookup"><span data-stu-id="5947a-124">Select capacity.</span></span> <span data-ttu-id="5947a-125">Vous pouvez modifier la capacité d’un environnement après sa création.</span><span class="sxs-lookup"><span data-stu-id="5947a-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="5947a-126">Créez votre environnement.</span><span class="sxs-lookup"><span data-stu-id="5947a-126">Create your environment.</span></span> <span data-ttu-id="5947a-127">Vous pouvez également épingler votre environnement au tableau de bord pour y accéder facilement à chaque fois que vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="5947a-127">You can also pin your environment to the dashboard for easy access whenever you sign in.</span></span>

  ![Créer l’épingle Time Series Insights sur le tableau de bord](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="5947a-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5947a-129">Next steps</span></span>

* <span data-ttu-id="5947a-130">[Définir des stratégies d’accès aux données](time-series-insights-data-access.md) pour accéder à votre environnement dans le [Portail Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="5947a-130">[Define data access policies](time-series-insights-data-access.md) to access your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="5947a-131">Créer une source d’événement</span><span class="sxs-lookup"><span data-stu-id="5947a-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="5947a-132">[Envoyer des événements](time-series-insights-send-events.md) à la source d’événement</span><span class="sxs-lookup"><span data-stu-id="5947a-132">[Send events](time-series-insights-send-events.md) to the event source</span></span>
