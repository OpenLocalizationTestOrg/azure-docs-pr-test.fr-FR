---
title: "événement aaaReal au moment du traitement de traitement des événements de flux de données Analytique | Documents Microsoft"
description: "Découvrez comment un ensemble de services Azure peut interagir pour l’analyse et le traitement des événements en temps réel."
keywords: "traitement en temps réel, traitement des événements, architecture de référence"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="85c60-104">Architecture de référence : Traitement d’événements en temps réel avec Microsoft Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="85c60-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="85c60-105">architecture de référence Hello pour les événements en temps réel avec Azure flux Analytique de traitement est prévue tooprovide un modèle générique pour le déploiement d’une plateforme en temps réel comme solution de traitement de flux de service (PaaS) avec Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="85c60-105">hello reference architecture for real-time event processing with Azure Stream Analytics is intended tooprovide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="85c60-106">Résumé</span><span class="sxs-lookup"><span data-stu-id="85c60-106">Summary</span></span>
<span data-ttu-id="85c60-107">En règle générale, les solutions analytique s’appuient sur des fonctionnalités telles que ETL (extraction, transformation, chargement) et d’entreposage de données, où les données sont stockées tooanalysis préalable.</span><span class="sxs-lookup"><span data-stu-id="85c60-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior tooanalysis.</span></span> <span data-ttu-id="85c60-108">Évolutions, y compris les données plus rapidement entrantes repoussent cette limite toohello de modèle existant.</span><span class="sxs-lookup"><span data-stu-id="85c60-108">Changing requirements, including more rapidly arriving data, are pushing this existing model toohello limit.</span></span> <span data-ttu-id="85c60-109">données de tooanalyze possibilité Hello dans Mobile toostorage préalable de flux de données sont une solution, et s’il n’est pas une nouvelle fonctionnalité, approche de hello n’a pas été largement adopté dans tous les secteurs de l’industrie.</span><span class="sxs-lookup"><span data-stu-id="85c60-109">hello ability tooanalyze data within moving streams prior toostorage is one solution, and while it is not a new capability, hello approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="85c60-110">Microsoft Azure fournit un catalogue étendu de technologies d’analyse compatibles avec de nombreuses solutions et spécifications.</span><span class="sxs-lookup"><span data-stu-id="85c60-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="85c60-111">En sélectionnant le toodeploy services Azure pour une solution de bout en bout peut être difficile étant donné la gamme hello des offres.</span><span class="sxs-lookup"><span data-stu-id="85c60-111">Selecting which Azure services toodeploy for an end-to-end solution can be a challenge given hello breadth of offerings.</span></span> <span data-ttu-id="85c60-112">Ce document est conçue toodescribe hello capacités et interopérabilité de hello divers services Azure qui prennent en charge une solution d’événements de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="85c60-112">This paper is designed toodescribe hello capabilities and interoperation of hello various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="85c60-113">Elle explique également certains des scénarios hello dans lesquels les clients peuvent tirer parti de ce type d’approche.</span><span class="sxs-lookup"><span data-stu-id="85c60-113">It also explains some of hello scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="85c60-114">Sommaire</span><span class="sxs-lookup"><span data-stu-id="85c60-114">Contents</span></span>
* <span data-ttu-id="85c60-115">Résumé</span><span class="sxs-lookup"><span data-stu-id="85c60-115">Executive Summary</span></span>
* <span data-ttu-id="85c60-116">Introduction au moment de le tooReal Analytique</span><span class="sxs-lookup"><span data-stu-id="85c60-116">Introduction tooReal-Time Analytics</span></span>
* <span data-ttu-id="85c60-117">Proposition de valeur des données en temps réel dans Azure</span><span class="sxs-lookup"><span data-stu-id="85c60-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="85c60-118">Scénarios courants d’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="85c60-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="85c60-119">Architecture et composants</span><span class="sxs-lookup"><span data-stu-id="85c60-119">Architecture and Components</span></span>
  * <span data-ttu-id="85c60-120">Sources de données</span><span class="sxs-lookup"><span data-stu-id="85c60-120">Data Sources</span></span>
  * <span data-ttu-id="85c60-121">Couche d’intégration de données</span><span class="sxs-lookup"><span data-stu-id="85c60-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="85c60-122">Couche d’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="85c60-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="85c60-123">Couche de stockage des données</span><span class="sxs-lookup"><span data-stu-id="85c60-123">Data Storage Layer</span></span>
  * <span data-ttu-id="85c60-124">Couche présentation/consommation</span><span class="sxs-lookup"><span data-stu-id="85c60-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="85c60-125">Conclusion</span><span class="sxs-lookup"><span data-stu-id="85c60-125">Conclusion</span></span>

<span data-ttu-id="85c60-126">**Auteur :** Charles Feddersen, architecte de solutions, Data Insights Center of Excellence, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="85c60-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="85c60-127">**Publié :** janvier 2015</span><span class="sxs-lookup"><span data-stu-id="85c60-127">**Published:** January 2015</span></span>

<span data-ttu-id="85c60-128">**Révision :** 1.0</span><span class="sxs-lookup"><span data-stu-id="85c60-128">**Revision:** 1.0</span></span>

<span data-ttu-id="85c60-129">**Téléchargement :**[Traitement d’événements en temps réel avec Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="85c60-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="85c60-130">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="85c60-130">Get help</span></span>
<span data-ttu-id="85c60-131">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="85c60-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="85c60-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="85c60-132">Next steps</span></span>
* [<span data-ttu-id="85c60-133">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="85c60-133">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="85c60-134">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="85c60-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="85c60-135">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="85c60-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="85c60-136">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="85c60-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="85c60-137">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="85c60-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

