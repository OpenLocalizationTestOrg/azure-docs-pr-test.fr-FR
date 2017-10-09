---
title: "contrôle d’intégrité du véhicule aaaPredict et du pilotage habitudes - Azure | Documents Microsoft"
description: "Utiliser les fonctionnalités de hello des aperçus Cortana Intelligence toogain prédictives et en temps réel sur l’intégrité du véhicule et du pilotage habituelles."
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
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="41301-103">Manuel de la solution Vehicle Telemetry Analytics</span><span class="sxs-lookup"><span data-stu-id="41301-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="41301-104">Cela **menu** lie chapitres toohello dans ce manuel.</span><span class="sxs-lookup"><span data-stu-id="41301-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="41301-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="41301-105">Overview</span></span>
<span data-ttu-id="41301-106">Ordinateurs super ont déplacé hors de laboratoire de hello et sont désormais stationnés dans notre garage !</span><span class="sxs-lookup"><span data-stu-id="41301-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="41301-107">Ces automobiles pointe contiennent une multitude de capteurs, en leur donnant hello capacité tootrack et surveiller des millions d’événements par seconde.</span><span class="sxs-lookup"><span data-stu-id="41301-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="41301-108">Nous espérons que par 2020, la plupart de ces voitures auront déjà été connecté toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="41301-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="41301-109">Imaginez appuyé dans grâce à cette multitude de sécurité supérieure des tooprovide de données, de fiabilité et une expérience mieux conduite !</span><span class="sxs-lookup"><span data-stu-id="41301-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="41301-110">Microsoft a réalisé ce rêve en développant Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="41301-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="41301-111">Intelligence de Cortana de Microsoft est de type données big entièrement gérées et avancé analytique suite vous tootransform vos données en action intelligente.</span><span class="sxs-lookup"><span data-stu-id="41301-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="41301-112">Nous souhaitons toointroduce toohello Cortana Intelligence véhicule télémétrie Analytique Solution de modèle.</span><span class="sxs-lookup"><span data-stu-id="41301-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="41301-113">Cette solution montre comment concessions de voiture et sociétés d’assurance automobiles fabricants peuvent utiliser des fonctions de hello de toogain Cortana Intelligence en temps réel et des analyses prédictives sur l’intégrité du véhicule et du pilotage habituelles.</span><span class="sxs-lookup"><span data-stu-id="41301-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="41301-114">solution de Hello est implémentée comme un [modèle d’architecture lambda](https://en.wikipedia.org/wiki/Lambda_architecture) montrant le potentiel de plateforme d’analyse décisionnelle de Cortana hello pour hello en temps réel et le traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="41301-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="41301-115">solution de Hello :</span><span class="sxs-lookup"><span data-stu-id="41301-115">hello solution:</span></span> 

* <span data-ttu-id="41301-116">fournit un simulateur de télématique des véhicules ;</span><span class="sxs-lookup"><span data-stu-id="41301-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="41301-117">utilise Event Hubs pour la réception dans Azure de millions d’événements de télémétrie virtuels associés aux véhicules ;</span><span class="sxs-lookup"><span data-stu-id="41301-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="41301-118">utilise les informations de flux de données Analytique toogain en temps réel sur l’intégrité du véhicule</span><span class="sxs-lookup"><span data-stu-id="41301-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="41301-119">conserve les données de hello dans le stockage à long terme pour l’analytique de lot plus riche.</span><span class="sxs-lookup"><span data-stu-id="41301-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="41301-120">bénéficie de l’apprentissage pour la détection d’anomalies dans en temps réel et insights prédictive toogain de traitement du lot.</span><span class="sxs-lookup"><span data-stu-id="41301-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="41301-121">s’appuie sur des données de tootransform HDInsight à l’échelle et orchestration toohandle de fabrique de données, en planifiant, gestion des ressources et d’analyse de pipeline de traitement par lots hello</span><span class="sxs-lookup"><span data-stu-id="41301-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="41301-122">offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives à l’aide de Power BI.</span><span class="sxs-lookup"><span data-stu-id="41301-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="41301-123">Architecture</span><span class="sxs-lookup"><span data-stu-id="41301-123">Architecture</span></span>
<span data-ttu-id="41301-124">![Diagramme d’architecture de solution](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Architecture d’analyse de télémétrie de véhicule*</span><span class="sxs-lookup"><span data-stu-id="41301-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="41301-125">Cette solution inclut des éléments suivants de hello **composants Cortana Intelligence** et présente leur intégration tooend de fin :</span><span class="sxs-lookup"><span data-stu-id="41301-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="41301-126">**Event Hubs** , pour la réception dans Azure de millions d’événements de télémétrie associés aux véhicules.</span><span class="sxs-lookup"><span data-stu-id="41301-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="41301-127">**STREAM ANALYTICS** , pour une visibilité en temps réel sur l’état des véhicules et une conservation de ces données dans un stockage à long terme afin d’enrichir les analyses par lots.</span><span class="sxs-lookup"><span data-stu-id="41301-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="41301-128">**Apprentissage** pour la détection d’anomalie en temps réel et les analyses prédictives toogain de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="41301-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="41301-129">**HDInsight** est exploitée tootransform des données à grande échelle</span><span class="sxs-lookup"><span data-stu-id="41301-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="41301-130">**Fabrique de données** gère l’orchestration, la planification, la gestion des ressources et la surveillance de pipeline de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="41301-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="41301-131">**POWER BI** offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives.</span><span class="sxs-lookup"><span data-stu-id="41301-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="41301-132">Cette solution utilise deux **sources de données**différentes :</span><span class="sxs-lookup"><span data-stu-id="41301-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="41301-133">**Simulée véhicule signaux et les diagnostics**: un simulateur de télématique véhicule émet des informations de diagnostic et des signaux qui correspondent état toohello du véhicule de hello et hello gérant le modèle à un moment donné dans le temps.</span><span class="sxs-lookup"><span data-stu-id="41301-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="41301-134">**Catalogue de véhicule**: un dataset de référence contenant un mappage de toomodel VIN.</span><span class="sxs-lookup"><span data-stu-id="41301-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>

