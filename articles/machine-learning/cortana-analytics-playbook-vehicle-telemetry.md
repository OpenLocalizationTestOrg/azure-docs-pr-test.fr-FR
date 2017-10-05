---
title: "Prédire l’état des véhicules et les habitudes de conduite | Microsoft Docs"
description: "Utilisez les fonctionnalités de Cortana Intelligence pour obtenir des informations en temps réel et prédictives sur l’état des véhicules et les habitudes de conduite."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: d202d314c61416cf306f760f93e0a4a88a1ab42b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="9f12f-103">Manuel de la solution Vehicle Telemetry Analytics</span><span class="sxs-lookup"><span data-stu-id="9f12f-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="9f12f-104">Ce **menu** contient des liens vers les chapitres de ce manuel.</span><span class="sxs-lookup"><span data-stu-id="9f12f-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="9f12f-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9f12f-105">Overview</span></span>
<span data-ttu-id="9f12f-106">Nous avons transféré nos superordinateurs du laboratoire à notre garage !</span><span class="sxs-lookup"><span data-stu-id="9f12f-106">Super computers have moved out of the lab and are now parked in our garage!</span></span> <span data-ttu-id="9f12f-107">Ces automobiles de pointe contiennent une multitude de capteurs capables de suivre et de surveiller des millions d'événements chaque seconde.</span><span class="sxs-lookup"><span data-stu-id="9f12f-107">These cutting-edge automobiles contain a myriad of sensors, giving them the ability to track and monitor millions of events every second.</span></span> <span data-ttu-id="9f12f-108">Nous pensons que d’ici 2020, la plupart de ces voitures seront connectées à Internet.</span><span class="sxs-lookup"><span data-stu-id="9f12f-108">We expect that by 2020, most of these cars will have been connected to the Internet.</span></span> <span data-ttu-id="9f12f-109">Imaginez le potentiel qu’offrent toutes ces données pour améliorer la sécurité, la fiabilité et le plaisir de la conduite !</span><span class="sxs-lookup"><span data-stu-id="9f12f-109">Imagine tapping into this wealth of data to provide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="9f12f-110">Microsoft a réalisé ce rêve en développant Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="9f12f-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="9f12f-111">Cortana Intelligence de Microsoft est une suite de traitement du Big Data et d’analyse avancée entièrement gérée, qui vous permet de convertir vos données en action intelligente.</span><span class="sxs-lookup"><span data-stu-id="9f12f-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you to transform your data into intelligent action.</span></span> <span data-ttu-id="9f12f-112">Nous souhaitons vous présenter le modèle de la solution Vehicle Telemetry Analytics Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="9f12f-112">We want to introduce you to the Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="9f12f-113">Cette solution montre comment les concessions, les constructeurs automobiles et les compagnies d’assurance peuvent utiliser les fonctionnalités de Cortana Intelligence pour obtenir des informations en temps réel et prédictives sur l’état des véhicules et les habitudes de conduite.</span><span class="sxs-lookup"><span data-stu-id="9f12f-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="9f12f-114">La solution est implémentée comme un [modèle d’architecture lambda](https://en.wikipedia.org/wiki/Lambda_architecture) montrant tout le potentiel de la plateforme Cortana Intelligence pour le traitement en temps réel et par lots.</span><span class="sxs-lookup"><span data-stu-id="9f12f-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing the full potential of the Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="9f12f-115">La solution :</span><span class="sxs-lookup"><span data-stu-id="9f12f-115">The solution:</span></span> 

* <span data-ttu-id="9f12f-116">fournit un simulateur de télématique des véhicules ;</span><span class="sxs-lookup"><span data-stu-id="9f12f-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="9f12f-117">utilise Event Hubs pour la réception dans Azure de millions d’événements de télémétrie virtuels associés aux véhicules ;</span><span class="sxs-lookup"><span data-stu-id="9f12f-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="9f12f-118">utilise Stream Analytics pour obtenir un aperçu en temps réel de l’intégrité du véhicule ;</span><span class="sxs-lookup"><span data-stu-id="9f12f-118">uses Stream Analytics to gain real-time insights on vehicle health</span></span>
* <span data-ttu-id="9f12f-119">conserve les données dans un stockage à long terme pour une analyse par lot plus riche ;</span><span class="sxs-lookup"><span data-stu-id="9f12f-119">persists the data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="9f12f-120">s’appuie sur Machine Learning pour la détection d’anomalies en temps réel et le traitement par lots afin d’obtenir des informations prédictives ;</span><span class="sxs-lookup"><span data-stu-id="9f12f-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="9f12f-121">utilise HDInsight pour transformer les données à l’échelle et Data Factory pour gérer l’orchestration, la planification, la gestion des ressources et la surveillance du pipeline de traitement par lots ;</span><span class="sxs-lookup"><span data-stu-id="9f12f-121">leverages HDInsight to transform data at scale and Data Factory to handle orchestration, scheduling, resource management, and monitoring of the batch processing pipeline</span></span> 
* <span data-ttu-id="9f12f-122">offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives à l’aide de Power BI.</span><span class="sxs-lookup"><span data-stu-id="9f12f-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="9f12f-123">Architecture</span><span class="sxs-lookup"><span data-stu-id="9f12f-123">Architecture</span></span>
<span data-ttu-id="9f12f-124">![Diagramme d’architecture de solution](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Architecture d’analyse de télémétrie de véhicule*</span><span class="sxs-lookup"><span data-stu-id="9f12f-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="9f12f-125">Cette solution inclut les **composants Cortana Intelligence** suivants et présente leur intégration de bout en bout :</span><span class="sxs-lookup"><span data-stu-id="9f12f-125">This solution includes the following **Cortana Intelligence components** and showcases their end to end integration:</span></span>

* <span data-ttu-id="9f12f-126">**Event Hubs** , pour la réception dans Azure de millions d’événements de télémétrie associés aux véhicules.</span><span class="sxs-lookup"><span data-stu-id="9f12f-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="9f12f-127">**STREAM ANALYTICS** , pour une visibilité en temps réel sur l’état des véhicules et une conservation de ces données dans un stockage à long terme afin d’enrichir les analyses par lots.</span><span class="sxs-lookup"><span data-stu-id="9f12f-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="9f12f-128">**MACHINE LEARNING** , pour la détection d’anomalies en temps réel et le traitement par lots afin d’obtenir des informations prédictives.</span><span class="sxs-lookup"><span data-stu-id="9f12f-128">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="9f12f-129">**HDInsight** est utilisé pour transformer les données à grande échelle</span><span class="sxs-lookup"><span data-stu-id="9f12f-129">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="9f12f-130">**Data Factory** gère l’orchestration, la planification, la gestion des ressources et la surveillance du pipeline de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="9f12f-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>
* <span data-ttu-id="9f12f-131">**POWER BI** offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives.</span><span class="sxs-lookup"><span data-stu-id="9f12f-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="9f12f-132">Cette solution utilise deux **sources de données**différentes :</span><span class="sxs-lookup"><span data-stu-id="9f12f-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="9f12f-133">**SIMULATION DES SIGNAUX ET DIAGNOSTICS D’UN VÉHICULE**: un simulateur télématique de véhicule émet des informations de diagnostic et des signaux correspondant à l’état du véhicule et au schéma de conduite à un moment donné dans le temps.</span><span class="sxs-lookup"><span data-stu-id="9f12f-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="9f12f-134">**CATALOGUE DE VÉHICULES**: un jeu de données de référence associé à un mappage VIN/modèle.</span><span class="sxs-lookup"><span data-stu-id="9f12f-134">**Vehicle catalog**: A reference dataset containing a VIN to model mapping.</span></span>

