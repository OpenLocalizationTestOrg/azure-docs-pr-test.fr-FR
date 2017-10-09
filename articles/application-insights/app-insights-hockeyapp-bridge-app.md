---
title: "aaaExploring HockeyApp des données dans une Application Azure Insights | Documents Microsoft"
description: "Analysez l’utilisation et les performances de votre application Azure avec Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="c19e1-103">Exploration des données HockeyApp dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="c19e1-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="c19e1-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello est recommandé de plateforme pour l’analyse des applications de bureau et mobiles dynamiques.</span><span class="sxs-lookup"><span data-stu-id="c19e1-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is hello recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="c19e1-105">À partir de HockeyApp, vous pouvez envoyer personnalisé et l’utilisation de télémétrie toomonitor de trace et faciliter le diagnostic (dans les données de panne plus toogetting).</span><span class="sxs-lookup"><span data-stu-id="c19e1-105">From HockeyApp, you can send custom and trace telemetry toomonitor usage and assist in diagnosis (in addition toogetting crash data).</span></span> <span data-ttu-id="c19e1-106">Ce flux de données de télémétrie peut être interrogé à l’aide de hello puissant [Analytique](app-insights-analytics.md) fonctionnalité de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c19e1-106">This stream of telemetry can be queried using hello powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="c19e1-107">En outre, vous pouvez [exporter hello personnalisée et la télémétrie des traces](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="c19e1-107">In addition, you can [export hello custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="c19e1-108">tooenable ces fonctionnalités, vous avez configuré un pont qui transfère les données personnalisées de HockeyApp tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="c19e1-108">tooenable these features, you set up a bridge that relays HockeyApp custom data tooApplication Insights.</span></span>

## <a name="hello-hockeyapp-bridge-app"></a><span data-ttu-id="c19e1-109">application de HockeyApp pont Hello</span><span class="sxs-lookup"><span data-stu-id="c19e1-109">hello HockeyApp Bridge app</span></span>
<span data-ttu-id="c19e1-110">Hello HockeyApp pont App est fonction principale hello qui vous permet de tooaccess votre HockeyApp personnalisée et la télémétrie des traces dans Application Insights via hello Analytique et les fonctionnalités de l’exportation continue.</span><span class="sxs-lookup"><span data-stu-id="c19e1-110">hello HockeyApp Bridge App is hello core feature that enables you tooaccess your HockeyApp custom and trace telemetry in Application Insights through hello Analytics and Continuous Export features.</span></span> <span data-ttu-id="c19e1-111">Événements personnalisé et trace collectées par HockeyApp après la création de hello Hello HockeyApp pont application seront accessibles à partir de ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="c19e1-111">Custom and trace events collected by HockeyApp after hello creation of hello HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="c19e1-112">Nous allons voir comment tooset une de ces applications de pont.</span><span class="sxs-lookup"><span data-stu-id="c19e1-112">Let’s see how tooset up one of these Bridge Apps.</span></span>

<span data-ttu-id="c19e1-113">Dans HockeyApp, ouvrez Paramètres de compte, [Jetons d’API](https://rink.hockeyapp.net/manage/auth_tokens).</span><span class="sxs-lookup"><span data-stu-id="c19e1-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="c19e1-114">Créez un nouveau jeton ou réutilisez un jeton existant.</span><span class="sxs-lookup"><span data-stu-id="c19e1-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="c19e1-115">les droits minimaux Hello requis sont « lecture seule ».</span><span class="sxs-lookup"><span data-stu-id="c19e1-115">hello minimum rights required are "read only".</span></span> <span data-ttu-id="c19e1-116">Création d’une copie de hello API jeton.</span><span class="sxs-lookup"><span data-stu-id="c19e1-116">Take a copy of hello API token.</span></span>

![Obtenir un jeton d’API HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="c19e1-118">Portail de Microsoft Azure hello ouvert et [créer une ressource Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c19e1-118">Open hello Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="c19e1-119">Définir le Type d’Application trop « Application de pont HockeyApp » :</span><span class="sxs-lookup"><span data-stu-id="c19e1-119">Set Application Type too“HockeyApp bridge application”:</span></span>

![Nouvelle ressource Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="c19e1-121">Vous n’avez pas besoin tooset un nom, il sera automatiquement configuré à partir du nom de HockeyApp hello.</span><span class="sxs-lookup"><span data-stu-id="c19e1-121">You don't need tooset a name - this will automatically be set from hello HockeyApp name.</span></span>

<span data-ttu-id="c19e1-122">champs de pont HockeyApp Hello s’affichent.</span><span class="sxs-lookup"><span data-stu-id="c19e1-122">hello HockeyApp bridge fields appear.</span></span> 

![Renseignez les champs de pont](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="c19e1-124">Entrez un jeton de HockeyApp hello notées précédemment.</span><span class="sxs-lookup"><span data-stu-id="c19e1-124">Enter hello HockeyApp token you noted earlier.</span></span> <span data-ttu-id="c19e1-125">Cette action remplit le menu de liste déroulante « Application HockeyApp » hello avec toutes vos applications HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="c19e1-125">This action populates hello “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="c19e1-126">Sélectionnez hello une vous voulez toouse et reste hello complète des champs de hello.</span><span class="sxs-lookup"><span data-stu-id="c19e1-126">Select hello one you want toouse, and complete hello remainder of hello fields.</span></span> 

<span data-ttu-id="c19e1-127">Ouvrez la nouvelle ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="c19e1-127">Open hello new resource.</span></span> 

<span data-ttu-id="c19e1-128">Notez que les données de salutation prennent un certain temps toostart flux.</span><span class="sxs-lookup"><span data-stu-id="c19e1-128">Note that hello data takes a while toostart flowing.</span></span>

![Ressource Application Insights en attente de données](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="c19e1-130">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="c19e1-130">That’s it!</span></span> <span data-ttu-id="c19e1-131">Personnalisé et la trace les données collectées dans votre application instrumentée HockeyApp à partir de ce point sont désormais également disponible tooyou Bonjour Analytique et l’exportation continue des fonctionnalités d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c19e1-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available tooyou in hello Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="c19e1-132">Nous allons brièvement chacun de ces tooyou désormais disponible de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="c19e1-132">Let’s briefly review each of these features now available tooyou.</span></span>

## <a name="analytics"></a><span data-ttu-id="c19e1-133">Analyse</span><span class="sxs-lookup"><span data-stu-id="c19e1-133">Analytics</span></span>
<span data-ttu-id="c19e1-134">Analytique est un outil puissant pour l’interrogation de vos données, ce qui vous toodiagnose ad hoc et analyse vos données de télémétrie et rapidement découverte les causes et les modèles.</span><span class="sxs-lookup"><span data-stu-id="c19e1-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you toodiagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Analyse](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="c19e1-136">En savoir plus sur Analyse</span><span class="sxs-lookup"><span data-stu-id="c19e1-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="c19e1-137">Exportation continue</span><span class="sxs-lookup"><span data-stu-id="c19e1-137">Continuous export</span></span>
<span data-ttu-id="c19e1-138">Exportation continue vous permet de tooexport vos données dans un conteneur de stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="c19e1-138">Continuous Export allows you tooexport your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="c19e1-139">Cela est très utile si vous avez besoin tookeep vos données plus longtemps que la période de rétention hello actuellement proposée par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c19e1-139">This is very useful if you need tookeep your data for longer than hello retention period currently offered by Application Insights.</span></span> <span data-ttu-id="c19e1-140">Vous pouvez conserver les données de salutation dans le stockage blob, le traiter dans une base de données SQL ou de votre solution d’entrepôt de données par défaut.</span><span class="sxs-lookup"><span data-stu-id="c19e1-140">You can keep hello data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="c19e1-141">En savoir plus sur l’exportation continue</span><span class="sxs-lookup"><span data-stu-id="c19e1-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="c19e1-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c19e1-142">Next steps</span></span>
* [<span data-ttu-id="c19e1-143">Appliquer des données tooyour Analytique</span><span class="sxs-lookup"><span data-stu-id="c19e1-143">Apply Analytics tooyour data</span></span>](app-insights-analytics-tour.md)

