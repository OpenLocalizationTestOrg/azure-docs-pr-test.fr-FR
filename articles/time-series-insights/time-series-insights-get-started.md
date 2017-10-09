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
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a><span data-ttu-id="72280-103">Créer un nouvel environnement de temps série Insights Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="72280-103">Create a new Time Series Insights environment in hello Azure portal</span></span>

<span data-ttu-id="72280-104">Un environnement Time Series est une ressource Azure disposant d’une capacité d’entrée et de stockage.</span><span class="sxs-lookup"><span data-stu-id="72280-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="72280-105">Clients fournir des environnements via hello portail Azure avec une capacité hello requis.</span><span class="sxs-lookup"><span data-stu-id="72280-105">Customers provision environments via hello Azure portal with hello required capacity.</span></span>

## <a name="steps-toocreate-hello-environment"></a><span data-ttu-id="72280-106">Environnement de hello toocreate étapes</span><span class="sxs-lookup"><span data-stu-id="72280-106">Steps toocreate hello environment</span></span>

<span data-ttu-id="72280-107">Suivez ces étapes toocreate votre environnement :</span><span class="sxs-lookup"><span data-stu-id="72280-107">Follow these steps toocreate your environment:</span></span>

1.  <span data-ttu-id="72280-108">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72280-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="72280-109">Cliquez sur hello plus signe (« + ») dans hello angle supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="72280-109">Click hello plus sign (“+”) in hello top left corner.</span></span>
3.  <span data-ttu-id="72280-110">Recherchez « Série un aperçu en temps » dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="72280-110">Search for “Time Series Insights” in hello search box.</span></span>

  ![Création d’environnement d’un aperçu en temps série hello](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="72280-112">Sélectionnez « Time Series Insights », puis cliquez sur « Créer ».</span><span class="sxs-lookup"><span data-stu-id="72280-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Créer groupe de ressources d’un aperçu en temps série hello](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="72280-114">Spécifiez le nom de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="72280-114">Specify environment name.</span></span> <span data-ttu-id="72280-115">Ce nom représente l’environnement hello dans [explorer de série heure](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72280-115">This name will represent hello environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="72280-116">Sélectionnez un abonnement.</span><span class="sxs-lookup"><span data-stu-id="72280-116">Select a subscription.</span></span> <span data-ttu-id="72280-117">Choisissez celui qui contient votre source d’événement.</span><span class="sxs-lookup"><span data-stu-id="72280-117">Choose one that contains your event source.</span></span> <span data-ttu-id="72280-118">Un aperçu en temps série peut détecter automatiquement Azure IoT Hub et les ressources de concentrateur d’événements existant dans hello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="72280-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in hello same subscription.</span></span>
7.  <span data-ttu-id="72280-119">Sélectionnez ou créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="72280-119">Select or create a resource group.</span></span> <span data-ttu-id="72280-120">Un groupe de ressources correspond à une collection de ressources Azure utilisées ensemble.</span><span class="sxs-lookup"><span data-stu-id="72280-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="72280-121">Sélectionnez un emplacement d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="72280-121">Select a hosting location.</span></span> <span data-ttu-id="72280-122">les centres de tooavoid déplacement des données entre les données, choisissez emplacement qui contient votre source d’événements.</span><span class="sxs-lookup"><span data-stu-id="72280-122">tooavoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="72280-123">Sélectionnez un niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="72280-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="72280-124">Sélectionnez la capacité.</span><span class="sxs-lookup"><span data-stu-id="72280-124">Select capacity.</span></span> <span data-ttu-id="72280-125">Vous pouvez modifier la capacité d’un environnement après sa création.</span><span class="sxs-lookup"><span data-stu-id="72280-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="72280-126">Créez votre environnement.</span><span class="sxs-lookup"><span data-stu-id="72280-126">Create your environment.</span></span> <span data-ttu-id="72280-127">Vous pouvez également épingler votre tableau de bord toohello environnement pour un accès aisé à chaque fois que vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="72280-127">You can also pin your environment toohello dashboard for easy access whenever you sign in.</span></span>

  ![Créer hello temps série Insights pin toodashboard](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="72280-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72280-129">Next steps</span></span>

* <span data-ttu-id="72280-130">[Définir des stratégies d’accès aux données](time-series-insights-data-access.md) tooaccess votre environnement dans [temps série Insights portail](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="72280-130">[Define data access policies](time-series-insights-data-access.md) tooaccess your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="72280-131">Créer une source d’événement</span><span class="sxs-lookup"><span data-stu-id="72280-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="72280-132">[Envoyer des événements](time-series-insights-send-events.md) toohello source d’événement</span><span class="sxs-lookup"><span data-stu-id="72280-132">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
