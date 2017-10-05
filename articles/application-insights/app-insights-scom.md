---
title: "Intégration de SCOM à Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 9c205465981fabdbb696cdc44f765532bbb992b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="26862-104">Analyse des performances des applications à l’aide d’Application Insights pour SCOM</span><span class="sxs-lookup"><span data-stu-id="26862-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="26862-105">Si vous utilisez System Center Operations Manager (SCOM) pour gérer vos serveurs, vous pouvez analyser les performances et diagnostiquer les problèmes afférents à l’aide [d’Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="26862-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="26862-106">Application Insights analyse les demandes entrantes de votre application web, les appels SQL et REST sortants, les exceptions et les suivis de journal.</span><span class="sxs-lookup"><span data-stu-id="26862-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="26862-107">Elle fournit des tableaux de bord avec des graphiques de mesure et des alertes intelligentes, ainsi que des requêtes analytiques et des outils de recherche de diagnostic efficaces sur ces données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="26862-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="26862-108">Vous pouvez activer l’analyse Application Insights à l’aide d’un pack d’administration SCOM.</span><span class="sxs-lookup"><span data-stu-id="26862-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="26862-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="26862-109">Before you start</span></span>
<span data-ttu-id="26862-110">Nous partons de l’hypothèse suivante :</span><span class="sxs-lookup"><span data-stu-id="26862-110">We assume:</span></span>

* <span data-ttu-id="26862-111">Vous maîtrisez SCOM et vous utilisez SCOM 2012 R2 ou 2016 pour gérer vos serveurs web IIS.</span><span class="sxs-lookup"><span data-stu-id="26862-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span></span>
* <span data-ttu-id="26862-112">Vous avez déjà installé sur vos serveurs une application web que vous souhaitez analyser avec Application Insights.</span><span class="sxs-lookup"><span data-stu-id="26862-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span></span>
* <span data-ttu-id="26862-113">La version de l’infrastructure de l’application est .NET 4.5 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="26862-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="26862-114">Vous avez accès à un abonnement dans [Microsoft Azure](https://azure.com) et pouvez vous connecter au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="26862-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="26862-115">Votre organisation doit posséder un abonnement et peut y ajouter votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="26862-115">Your organization may have a subscription, and can add your Microsoft account to it.</span></span>

<span data-ttu-id="26862-116">(L’équipe de développement peut créer le [kit de développement logiciel (SDK) Application Insights](app-insights-asp-net.md) dans l’application web.</span><span class="sxs-lookup"><span data-stu-id="26862-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span></span> <span data-ttu-id="26862-117">Cette instrumentation en cours de création lui donne plus de flexibilité dans l’écriture des données de télémétrie personnalisées.</span><span class="sxs-lookup"><span data-stu-id="26862-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="26862-118">Toutefois, cela n’a aucune importance : vous pouvez suivre les étapes décrites ici, avec ou sans le kit de développement logiciel (SDK) intégré.)</span><span class="sxs-lookup"><span data-stu-id="26862-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="26862-119">(Une fois) Installer le pack d’administration Application Insights</span><span class="sxs-lookup"><span data-stu-id="26862-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="26862-120">Sur l’ordinateur sur lequel vous exécutez Operations Manager :</span><span class="sxs-lookup"><span data-stu-id="26862-120">On the machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="26862-121">Désinstallez les anciennes versions du pack d’administration :</span><span class="sxs-lookup"><span data-stu-id="26862-121">Uninstall any old version of the management pack:</span></span>
   1. <span data-ttu-id="26862-122">Dans Operations Manager, ouvrez Administration, Packs d’administration.</span><span class="sxs-lookup"><span data-stu-id="26862-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="26862-123">Supprimez l’ancienne version.</span><span class="sxs-lookup"><span data-stu-id="26862-123">Delete the old version.</span></span>
2. <span data-ttu-id="26862-124">Téléchargez et installez le pack d’administration à partir du catalogue.</span><span class="sxs-lookup"><span data-stu-id="26862-124">Download and install the management pack from the catalog.</span></span>
3. <span data-ttu-id="26862-125">Redémarrez Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="26862-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="26862-126">Créer un pack d’administration</span><span class="sxs-lookup"><span data-stu-id="26862-126">Create a management pack</span></span>
1. <span data-ttu-id="26862-127">Dans Operations Manager, ouvrez **Création**, **.NET...with Application Insights** (.NET... avec Application Insights), **Assistant Ajout d’analyse**, et choisissez à nouveau **.NET...with Application Insights** (.NET... avec Application Insights).</span><span class="sxs-lookup"><span data-stu-id="26862-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="26862-128">Nommez la configuration d’après votre application.</span><span class="sxs-lookup"><span data-stu-id="26862-128">Name the configuration after your app.</span></span> <span data-ttu-id="26862-129">(Vous devez instrumenter une application à la fois.)</span><span class="sxs-lookup"><span data-stu-id="26862-129">(You have to instrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="26862-130">Sur la même page de l’Assistant, créez un pack d’administration ou sélectionnez un pack que vous avez créé précédemment pour Application Insights.</span><span class="sxs-lookup"><span data-stu-id="26862-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="26862-131">(Le [pack d’administration](https://technet.microsoft.com/library/cc974491.aspx) Application Insights est un modèle à partir duquel vous créez une instance.</span><span class="sxs-lookup"><span data-stu-id="26862-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="26862-132">Vous pouvez réutiliser la même instance ultérieurement.)</span><span class="sxs-lookup"><span data-stu-id="26862-132">You can reuse the same instance later.)</span></span>

    ![Dans l’onglet Propriétés générales, saisissez le nom de l’application.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="26862-136">Choisissez une application que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="26862-136">Choose one app that you want to monitor.</span></span> <span data-ttu-id="26862-137">La fonctionnalité de recherche effectue une recherche parmi les applications installées sur vos serveurs.</span><span class="sxs-lookup"><span data-stu-id="26862-137">The search feature searches among apps installed on your servers.</span></span>
   
    ![Dans l’onglet What to Monitor (Éléments à analyser), cliquez sur Ajouter, saisissez une partie du nom de l’application, cliquez sur Rechercher, choisissez l’application, ensuite cliquez sur Ajouter, puis sur OK.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="26862-139">Le champ de portée Analyse facultatif peut être utilisé pour spécifier un sous-ensemble de vos serveurs, si vous ne souhaitez pas analyser l’application dans tous les serveurs.</span><span class="sxs-lookup"><span data-stu-id="26862-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span></span>
2. <span data-ttu-id="26862-140">Sur la page suivante de l’Assistant, vous devez d’abord fournir vos informations d’identification pour vous connecter à Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="26862-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span></span>
   
    <span data-ttu-id="26862-141">Sur cette page, vous choisissez la ressource Application Insights dans laquelle vous souhaitez que les données de télémétrie soient analysées et affichées.</span><span class="sxs-lookup"><span data-stu-id="26862-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="26862-142">Si l’application a été configurée pour Application Insights pendant le développement, sélectionnez sa ressource existante.</span><span class="sxs-lookup"><span data-stu-id="26862-142">If the application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="26862-143">Sinon, créez une ressource nommée d’après l’application.</span><span class="sxs-lookup"><span data-stu-id="26862-143">Otherwise, create a new resource named for the app.</span></span> <span data-ttu-id="26862-144">S’il existe d’autres applications qui sont des composants du même système, placez-les dans le même groupe de ressources, pour faciliter l’accès aux données de télémétrie à gérer.</span><span class="sxs-lookup"><span data-stu-id="26862-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span></span>
     
     <span data-ttu-id="26862-145">Vous pouvez modifier ces paramètres plus tard.</span><span class="sxs-lookup"><span data-stu-id="26862-145">You can change these settings later.</span></span>
     
     ![Dans l’onglet Application Insights settings (Paramètres d’Application Insights), cliquez sur « se connecter » et indiquez vos informations d’identification de compte Microsoft pour Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="26862-148">Terminez l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="26862-148">Complete the wizard.</span></span>
   
    ![Click Create](./media/app-insights-scom/070.png)

<span data-ttu-id="26862-150">Répétez cette procédure pour chaque application que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="26862-150">Repeat this procedure for each app that you want to monitor.</span></span>

<span data-ttu-id="26862-151">Si vous devez modifier les paramètres plus tard, ouvrez à nouveau les propriétés d’analyse à partir de la fenêtre de création.</span><span class="sxs-lookup"><span data-stu-id="26862-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span></span>

![Dans la fenêtre de création, sélectionnez .NET Application Performance Monitoring with Application Insights (Analyse des performances des applications .NET avec Application Insights), choisissez votre analyse et cliquez sur Propriétés.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="26862-153">Vérifier l’analyse</span><span class="sxs-lookup"><span data-stu-id="26862-153">Verify monitoring</span></span>
<span data-ttu-id="26862-154">L’analyse que vous avez mise en place recherche votre application sur chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="26862-154">The monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="26862-155">Aux endroits où elle trouve l’application, elle configure Application Insights Status Monitor pour analyser l’application.</span><span class="sxs-lookup"><span data-stu-id="26862-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span></span> <span data-ttu-id="26862-156">Si nécessaire, elle installe d’abord Status Monitor sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="26862-156">If necessary, it first installs Status Monitor on the server.</span></span>

<span data-ttu-id="26862-157">Vous pouvez vérifier quelles sont les instances de l’application trouvées :</span><span class="sxs-lookup"><span data-stu-id="26862-157">You can verify which instances of the app it has found:</span></span>

![Dans la fenêtre d’analyse, ouvrez Application Insights.](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="26862-159">Afficher les données de télémétrie dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="26862-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="26862-160">Dans le [portail Azure](https://portal.azure.com), accédez à la ressource de votre application.</span><span class="sxs-lookup"><span data-stu-id="26862-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span></span> <span data-ttu-id="26862-161">Vous [pouvez voir les graphiques affichant les données de télémétrie](app-insights-dashboards.md) depuis votre application.</span><span class="sxs-lookup"><span data-stu-id="26862-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="26862-162">(S’ils ne sont pas encore affichés sur la page principale, cliquez sur Live Metrics Stream (Diffusion des mesures en direct).)</span><span class="sxs-lookup"><span data-stu-id="26862-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="26862-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26862-163">Next steps</span></span>
* <span data-ttu-id="26862-164">[Configurez un tableau de bord](app-insights-dashboards.md) pour rassembler les graphiques d’analyse les plus importants de cette application et d’autres applications.</span><span class="sxs-lookup"><span data-stu-id="26862-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="26862-165">En savoir plus sur les métriques</span><span class="sxs-lookup"><span data-stu-id="26862-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="26862-166">Configurer des alertes</span><span class="sxs-lookup"><span data-stu-id="26862-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="26862-167">Diagnostiquer des problèmes de performances</span><span class="sxs-lookup"><span data-stu-id="26862-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="26862-168">Requêtes Analytics efficaces</span><span class="sxs-lookup"><span data-stu-id="26862-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="26862-169">Tests web de disponibilité</span><span class="sxs-lookup"><span data-stu-id="26862-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

