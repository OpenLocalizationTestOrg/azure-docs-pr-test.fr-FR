---
title: "l’intégration avec Application Insights aaaSCOM | Documents Microsoft"
description: "Si vous êtes un utilisateur SCOM, analysez les performances et diagnostiquez les problèmes avec Application Insights. Tableaux de bord complets, alertes intelligentes, requêtes analytiques et outils de diagnostic efficaces."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="f839d-104">Analyse des performances des applications à l’aide d’Application Insights pour SCOM</span><span class="sxs-lookup"><span data-stu-id="f839d-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="f839d-105">Si vous utilisez System Center Operations Manager (SCOM) toomanage vos serveurs, vous pouvez surveiller les performances et diagnostiquer les problèmes de performances à l’aide de hello de [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="f839d-105">If you use System Center Operations Manager (SCOM) toomanage your servers, you can monitor performance and diagnose performance issues with hello help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="f839d-106">Application Insights analyse les demandes entrantes de votre application web, les appels SQL et REST sortants, les exceptions et les suivis de journal.</span><span class="sxs-lookup"><span data-stu-id="f839d-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="f839d-107">Elle fournit des tableaux de bord avec des graphiques de mesure et des alertes intelligentes, ainsi que des requêtes analytiques et des outils de recherche de diagnostic efficaces sur ces données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="f839d-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="f839d-108">Vous pouvez activer l’analyse Application Insights à l’aide d’un pack d’administration SCOM.</span><span class="sxs-lookup"><span data-stu-id="f839d-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f839d-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f839d-109">Before you start</span></span>
<span data-ttu-id="f839d-110">Nous partons de l’hypothèse suivante :</span><span class="sxs-lookup"><span data-stu-id="f839d-110">We assume:</span></span>

* <span data-ttu-id="f839d-111">Serveurs web, vous êtes familiarisé avec SCOM et que vous utilisez SCOM 2012 R2 ou 2016 toomanage votre IIS.</span><span class="sxs-lookup"><span data-stu-id="f839d-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 toomanage your IIS web servers.</span></span>
* <span data-ttu-id="f839d-112">Vous avez déjà installé sur vos serveurs d’une application web que vous souhaitez toomonitor avec Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f839d-112">You have already installed on your servers a web application that you want toomonitor with Application Insights.</span></span>
* <span data-ttu-id="f839d-113">La version de l’infrastructure de l’application est .NET 4.5 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f839d-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="f839d-114">Vous avez accès tooa abonnement dans [Microsoft Azure](https://azure.com) et peuvent se connecter toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f839d-114">You have access tooa subscription in [Microsoft Azure](https://azure.com) and can sign in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f839d-115">Votre entreprise peut disposer d’un abonnement et pouvez ajouter vos tooit de compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f839d-115">Your organization may have a subscription, and can add your Microsoft account tooit.</span></span>

<span data-ttu-id="f839d-116">(équipe de développement hello peut générer hello [Application Insights SDK](app-insights-asp-net.md) dans l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="f839d-116">(hello development team might build hello [Application Insights SDK](app-insights-asp-net.md) into hello web app.</span></span> <span data-ttu-id="f839d-117">Cette instrumentation en cours de création lui donne plus de flexibilité dans l’écriture des données de télémétrie personnalisées.</span><span class="sxs-lookup"><span data-stu-id="f839d-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="f839d-118">Toutefois, il n’a aucune importance : vous pouvez suivre les étapes de hello décrites ici, avec ou sans hello SDK intégré.)</span><span class="sxs-lookup"><span data-stu-id="f839d-118">However, it doesn't matter: you can follow hello steps described here either with or without hello SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="f839d-119">(Une fois) Installer le pack d’administration Application Insights</span><span class="sxs-lookup"><span data-stu-id="f839d-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="f839d-120">Sur l’ordinateur hello sur lequel vous exécutez Operations Manager :</span><span class="sxs-lookup"><span data-stu-id="f839d-120">On hello machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="f839d-121">Désinstallez toute ancienne version du Pack d’administration de hello :</span><span class="sxs-lookup"><span data-stu-id="f839d-121">Uninstall any old version of hello management pack:</span></span>
   1. <span data-ttu-id="f839d-122">Dans Operations Manager, ouvrez Administration, Packs d’administration.</span><span class="sxs-lookup"><span data-stu-id="f839d-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="f839d-123">Supprimez l’ancienne version de hello.</span><span class="sxs-lookup"><span data-stu-id="f839d-123">Delete hello old version.</span></span>
2. <span data-ttu-id="f839d-124">Téléchargez et installez le pack d’administration hello du catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="f839d-124">Download and install hello management pack from hello catalog.</span></span>
3. <span data-ttu-id="f839d-125">Redémarrez Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="f839d-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="f839d-126">Créer un pack d’administration</span><span class="sxs-lookup"><span data-stu-id="f839d-126">Create a management pack</span></span>
1. <span data-ttu-id="f839d-127">Dans Operations Manager, ouvrez **Création**, **.NET...with Application Insights** (.NET... avec Application Insights), **Assistant Ajout d’analyse**, et choisissez à nouveau **.NET...with Application Insights** (.NET... avec Application Insights).</span><span class="sxs-lookup"><span data-stu-id="f839d-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="f839d-128">Configuration du nom hello après votre application.</span><span class="sxs-lookup"><span data-stu-id="f839d-128">Name hello configuration after your app.</span></span> <span data-ttu-id="f839d-129">(Vous avez tooinstrument une application à la fois).</span><span class="sxs-lookup"><span data-stu-id="f839d-129">(You have tooinstrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="f839d-130">Sur hello même page de l’Assistant, créez une nouvelle gestion pack, ou sélectionnez un pack que vous avez créé pour Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f839d-130">On hello same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="f839d-131">(hello Application Insights [Pack d’administration](https://technet.microsoft.com/library/cc974491.aspx) est un modèle à partir de laquelle vous créez une instance.</span><span class="sxs-lookup"><span data-stu-id="f839d-131">(hello Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="f839d-132">Vous pouvez réutiliser hello même instance ultérieurement.)</span><span class="sxs-lookup"><span data-stu-id="f839d-132">You can reuse hello same instance later.)</span></span>

    ![Dans l’onglet Propriétés générales de hello, tapez le nom de hello de l’application hello.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="f839d-136">Choisissez une application que vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="f839d-136">Choose one app that you want toomonitor.</span></span> <span data-ttu-id="f839d-137">recherche de la fonctionnalité de recherche Hello parmi les applications installées sur vos serveurs.</span><span class="sxs-lookup"><span data-stu-id="f839d-137">hello search feature searches among apps installed on your servers.</span></span>
   
    ![Sur l’onglet tooMonitor, cliquez sur Ajouter, tapez une partie du nom de l’application hello, cliquez sur Rechercher, choisissez application hello, puis ajouter, OK.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="f839d-139">champ de Hello facultatif analyse étendue peut être utilisé toospecify un sous-ensemble de vos serveurs, si vous ne souhaitez pas application hello de toomonitor dans tous les serveurs.</span><span class="sxs-lookup"><span data-stu-id="f839d-139">hello optional Monitoring scope field can be used toospecify a subset of your servers, if you don't want toomonitor hello app in all servers.</span></span>
2. <span data-ttu-id="f839d-140">Sur la page d’Assistant suivante hello, vous devez tout d’abord fournir toosign de vos informations d’identification dans tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f839d-140">On hello next wizard page, you must first provide your credentials toosign in tooMicrosoft Azure.</span></span>
   
    <span data-ttu-id="f839d-141">Dans cette page, vous choisissez de ressource d’Application Insights hello où vous souhaitez toobe de données de télémétrie hello analysé et affiché.</span><span class="sxs-lookup"><span data-stu-id="f839d-141">On this page, you choose hello Application Insights resource where you want hello telemetry data toobe analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="f839d-142">Si l’application hello a été configurée pour Application Insights au cours du développement, sélectionnez la ressource existante.</span><span class="sxs-lookup"><span data-stu-id="f839d-142">If hello application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="f839d-143">Sinon, créez une ressource nommée pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="f839d-143">Otherwise, create a new resource named for hello app.</span></span> <span data-ttu-id="f839d-144">S’il existe des autres applications qui sont des composants de hello même système, placez-les dans hello même groupe de ressources, toomanage plus facilement des données de télémétrie toohello accès toomake.</span><span class="sxs-lookup"><span data-stu-id="f839d-144">If there are other apps that are components of hello same system, put them in hello same resource group, toomake access toohello telemetry easier toomanage.</span></span>
     
     <span data-ttu-id="f839d-145">Vous pouvez modifier ces paramètres plus tard.</span><span class="sxs-lookup"><span data-stu-id="f839d-145">You can change these settings later.</span></span>
     
     ![Dans l’onglet Application Insights settings (Paramètres d’Application Insights), cliquez sur « se connecter » et indiquez vos informations d’identification de compte Microsoft pour Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="f839d-148">Assistant hello terminée.</span><span class="sxs-lookup"><span data-stu-id="f839d-148">Complete hello wizard.</span></span>
   
    ![Click Create](./media/app-insights-scom/070.png)

<span data-ttu-id="f839d-150">Répétez cette procédure pour chaque application que vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="f839d-150">Repeat this procedure for each app that you want toomonitor.</span></span>

<span data-ttu-id="f839d-151">Si vous avez besoin de paramètres de toochange ultérieurement, ouvrez à nouveau les propriétés de hello Hello surveiller à partir de la fenêtre de création de hello.</span><span class="sxs-lookup"><span data-stu-id="f839d-151">If you need toochange settings later, re-open hello properties of hello monitor from hello Authoring window.</span></span>

![Dans la fenêtre de création, sélectionnez .NET Application Performance Monitoring with Application Insights (Analyse des performances des applications .NET avec Application Insights), choisissez votre analyse et cliquez sur Propriétés.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="f839d-153">Vérifier l’analyse</span><span class="sxs-lookup"><span data-stu-id="f839d-153">Verify monitoring</span></span>
<span data-ttu-id="f839d-154">Moniteur de Hello que vous avez installé la recherche de votre application sur chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="f839d-154">hello monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="f839d-155">Dans ce cas, il trouve l’application hello, il configure Application Insights Status Monitor toomonitor hello application.</span><span class="sxs-lookup"><span data-stu-id="f839d-155">Where it finds hello app, it configures Application Insights Status Monitor toomonitor hello app.</span></span> <span data-ttu-id="f839d-156">Si nécessaire, il installe tout d’abord le moniteur d’état sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="f839d-156">If necessary, it first installs Status Monitor on hello server.</span></span>

<span data-ttu-id="f839d-157">Vous pouvez vérifier les instances de l’application hello a trouvé :</span><span class="sxs-lookup"><span data-stu-id="f839d-157">You can verify which instances of hello app it has found:</span></span>

![Dans la fenêtre d’analyse, ouvrez Application Insights.](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="f839d-159">Afficher les données de télémétrie dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="f839d-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="f839d-160">Bonjour [portail Azure](https://portal.azure.com), parcourir les ressources toohello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="f839d-160">In hello [Azure portal](https://portal.azure.com), browse toohello resource for your app.</span></span> <span data-ttu-id="f839d-161">Vous [pouvez voir les graphiques affichant les données de télémétrie](app-insights-dashboards.md) depuis votre application.</span><span class="sxs-lookup"><span data-stu-id="f839d-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="f839d-162">(Si elle n’a pas affichées sur la page principale de hello encore, cliquez sur flux Live de métriques).</span><span class="sxs-lookup"><span data-stu-id="f839d-162">(If it hasn't shown up on hello main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f839d-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f839d-163">Next steps</span></span>
* <span data-ttu-id="f839d-164">[Configurer un tableau de bord](app-insights-dashboards.md) graphiques de données plus importantes toobring hello ensemble cela et les autres applications d’analyse.</span><span class="sxs-lookup"><span data-stu-id="f839d-164">[Set up a dashboard](app-insights-dashboards.md) toobring together hello most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="f839d-165">En savoir plus sur les métriques</span><span class="sxs-lookup"><span data-stu-id="f839d-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="f839d-166">Configurer des alertes</span><span class="sxs-lookup"><span data-stu-id="f839d-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="f839d-167">Diagnostiquer des problèmes de performances</span><span class="sxs-lookup"><span data-stu-id="f839d-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="f839d-168">Requêtes Analytics efficaces</span><span class="sxs-lookup"><span data-stu-id="f839d-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="f839d-169">Tests web de disponibilité</span><span class="sxs-lookup"><span data-stu-id="f839d-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

