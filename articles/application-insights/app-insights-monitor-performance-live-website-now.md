---
title: "Surveiller une application web ASP.NET active avec Azure Application Insights | Microsoft Docs"
description: "Analysez les performances d'un site web sans le redéployer. Fonctionne avec les applications web ASP.NET hébergées localement, dans des machines virtuelles ou sur Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d07a0c81f89100c378456bbea8dca1c009cc8d77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="151d9-104">Instrumenter des applications web lors de l’exécution avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="151d9-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="151d9-105">Vous pouvez instrumenter une application web dynamique avec Azure Application Insights, sans avoir à modifier ou à redéployer votre code.</span><span class="sxs-lookup"><span data-stu-id="151d9-105">You can instrument a live web app with Azure Application Insights, without having to modify or redeploy your code.</span></span> <span data-ttu-id="151d9-106">Si vos applications sont hébergées sur un serveur IIS local, installez Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="151d9-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="151d9-107">S’il s’agit d’applications web Azure ou d’applications qui s’exécutent dans une machine virtuelle Azure, vous pouvez activer l’analyse Application Insights à partir du panneau de configuration Azure.</span><span class="sxs-lookup"><span data-stu-id="151d9-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from the Azure control panel.</span></span> <span data-ttu-id="151d9-108">(Des articles distincts sont également consacrés à l’instrumentation des [applications web J2EE actives](app-insights-java-live.md) et [d’Azure Cloud Services](app-insights-cloudservices.md).) Cette opération nécessite un abonnement [Microsoft Azure](http://azure.com) .</span><span class="sxs-lookup"><span data-stu-id="151d9-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![Exemples de graphiques](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="151d9-110">Vous avez le choix entre trois façons d’appliquer Application Insights à vos applications web .NET :</span><span class="sxs-lookup"><span data-stu-id="151d9-110">You have a choice of three routes to apply Application Insights to your .NET web applications:</span></span>

* <span data-ttu-id="151d9-111">**En cours de création :** [ajoutez le Kit de développement logiciel (SDK) Application Insights][greenbrown] au code de votre application web.</span><span class="sxs-lookup"><span data-stu-id="151d9-111">**Build time:** [Add the Application Insights SDK][greenbrown] to your web app code.</span></span>
* <span data-ttu-id="151d9-112">**En cours d’exécution :** instrumentez votre application web sur le serveur, comme décrit ci-dessous, sans régénérer ni redéployer le code.</span><span class="sxs-lookup"><span data-stu-id="151d9-112">**Run time:** Instrument your web app on the server, as described below, without rebuilding and redeploying the code.</span></span>
* <span data-ttu-id="151d9-113">**Les deux :** intégrez le Kit de développement logiciel (SDK) à votre code d’application web et appliquez également les extensions à l’exécution.</span><span class="sxs-lookup"><span data-stu-id="151d9-113">**Both:** Build the SDK into your web app code, and also apply the run-time extensions.</span></span> <span data-ttu-id="151d9-114">Profitez des avantages des deux options.</span><span class="sxs-lookup"><span data-stu-id="151d9-114">Get the best of both options.</span></span>

<span data-ttu-id="151d9-115">Voici un résumé de ce que vous apporte chaque méthode :</span><span class="sxs-lookup"><span data-stu-id="151d9-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="151d9-116">En cours de création</span><span class="sxs-lookup"><span data-stu-id="151d9-116">Build time</span></span> | <span data-ttu-id="151d9-117">En cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="151d9-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="151d9-118">Requêtes et exceptions</span><span class="sxs-lookup"><span data-stu-id="151d9-118">Requests & exceptions</span></span> |<span data-ttu-id="151d9-119">Oui</span><span class="sxs-lookup"><span data-stu-id="151d9-119">Yes</span></span> |<span data-ttu-id="151d9-120">Oui</span><span class="sxs-lookup"><span data-stu-id="151d9-120">Yes</span></span> |
| [<span data-ttu-id="151d9-121">Exceptions plus détaillées</span><span class="sxs-lookup"><span data-stu-id="151d9-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="151d9-122">Oui</span><span class="sxs-lookup"><span data-stu-id="151d9-122">Yes</span></span> |
| [<span data-ttu-id="151d9-123">Diagnostics de dépendance</span><span class="sxs-lookup"><span data-stu-id="151d9-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="151d9-124">Sur .NET 4.6 +, mais moins détaillé</span><span class="sxs-lookup"><span data-stu-id="151d9-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="151d9-125">Oui, tous les détails : codes de résultat, texte de commande SQL, verbe HTTP</span><span class="sxs-lookup"><span data-stu-id="151d9-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="151d9-126">Compteurs de performances système</span><span class="sxs-lookup"><span data-stu-id="151d9-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="151d9-127">Oui</span><span class="sxs-lookup"><span data-stu-id="151d9-127">Yes</span></span> |<span data-ttu-id="151d9-128">Oui</span><span class="sxs-lookup"><span data-stu-id="151d9-128">Yes</span></span> |
| <span data-ttu-id="151d9-129">[API pour la télémétrie personnalisée][api]</span><span class="sxs-lookup"><span data-stu-id="151d9-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="151d9-130">Oui</span><span class="sxs-lookup"><span data-stu-id="151d9-130">Yes</span></span> |<span data-ttu-id="151d9-131">Non</span><span class="sxs-lookup"><span data-stu-id="151d9-131">No</span></span> |
| [<span data-ttu-id="151d9-132">Intégration des journaux de suivi</span><span class="sxs-lookup"><span data-stu-id="151d9-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="151d9-133">Oui</span><span class="sxs-lookup"><span data-stu-id="151d9-133">Yes</span></span> |<span data-ttu-id="151d9-134">Non</span><span class="sxs-lookup"><span data-stu-id="151d9-134">No</span></span> |
| [<span data-ttu-id="151d9-135">Mode Page et données utilisateur</span><span class="sxs-lookup"><span data-stu-id="151d9-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="151d9-136">Oui</span><span class="sxs-lookup"><span data-stu-id="151d9-136">Yes</span></span> |<span data-ttu-id="151d9-137">Non</span><span class="sxs-lookup"><span data-stu-id="151d9-137">No</span></span> |
| <span data-ttu-id="151d9-138">Nécessité de régénérer le code</span><span class="sxs-lookup"><span data-stu-id="151d9-138">Need to rebuild code</span></span> |<span data-ttu-id="151d9-139">Oui</span><span class="sxs-lookup"><span data-stu-id="151d9-139">Yes</span></span> | <span data-ttu-id="151d9-140">Non</span><span class="sxs-lookup"><span data-stu-id="151d9-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="151d9-141">Surveiller une application web Azure active</span><span class="sxs-lookup"><span data-stu-id="151d9-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="151d9-142">Si votre application s’exécute en tant que service web Azure, voici comment activer la surveillance :</span><span class="sxs-lookup"><span data-stu-id="151d9-142">If your application is running as an Azure web service, here's how to switch on monitoring:</span></span>

* <span data-ttu-id="151d9-143">Sélectionnez Application Insights sur le panneau de configuration de l’application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="151d9-143">Select Application Insights on the app's control panel in Azure.</span></span>

    ![Configurer Application Insights pour une application web Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="151d9-145">Lorsque la page de résumé d’Application Insights s’ouvre, cliquez sur le lien en bas pour ouvrir la ressource Application Insights complète.</span><span class="sxs-lookup"><span data-stu-id="151d9-145">When the Application Insights summary page opens, click the link at the bottom to open the full Application Insights resource.</span></span>

    ![Cliquer pour accéder à Application Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="151d9-147">[Surveillance des applications de machine virtuelle et cloud](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="151d9-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="151d9-148">Activation de la surveillance côté client dans Azure</span><span class="sxs-lookup"><span data-stu-id="151d9-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="151d9-149">Si vous avez activé Application Insights dans Azure, vous pouvez ajouter la consultation de page et la télémétrie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="151d9-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="151d9-150">Cliquez sur Paramètres > Paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="151d9-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="151d9-151">Sous Paramètres de l’application, ajoutez une nouvelle paire clé/valeur :</span><span class="sxs-lookup"><span data-stu-id="151d9-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="151d9-152">Clé :`APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="151d9-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="151d9-153">Valeur: `true`</span><span class="sxs-lookup"><span data-stu-id="151d9-153">Value: `true`</span></span>
3. <span data-ttu-id="151d9-154">**Enregistrez** les paramètres et **Redémarrez** votre application.</span><span class="sxs-lookup"><span data-stu-id="151d9-154">**Save** the settings and **Restart** your app.</span></span>

<span data-ttu-id="151d9-155">Le Kit de développement logiciel (SDK) JavaScript Application Insights est maintenant injecté dans chaque page web.</span><span class="sxs-lookup"><span data-stu-id="151d9-155">The Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="151d9-156">Surveiller une application web IIS active</span><span class="sxs-lookup"><span data-stu-id="151d9-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="151d9-157">Si votre application est hébergée sur un serveur IIS, activez Application Insights à l’aide de Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="151d9-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="151d9-158">Sur votre serveur web IIS, connectez-vous avec vos informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="151d9-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="151d9-159">Si Application Insights Status Monitor n’est pas encore installé, téléchargez et exécutez le [programme d’installation Status Monitor](http://go.microsoft.com/fwlink/?LinkId=506648) (ou exécutez [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) et recherchez-y Application Insights Status Monitor).</span><span class="sxs-lookup"><span data-stu-id="151d9-159">If Application Insights Status Monitor is not already installed, download and run the [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="151d9-160">Dans Status Monitor, sélectionnez l’application web installée ou le site Web à surveiller.</span><span class="sxs-lookup"><span data-stu-id="151d9-160">In Status Monitor, select the installed web application or website that you want to monitor.</span></span> <span data-ttu-id="151d9-161">Connectez-vous avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="151d9-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="151d9-162">Configurez la ressource où vous souhaitez afficher les résultats dans le portail Application Insights.</span><span class="sxs-lookup"><span data-stu-id="151d9-162">Configure the resource where you want to see the results in the Application Insights portal.</span></span> <span data-ttu-id="151d9-163">(En règle générale, il est préférable de créer une ressource.</span><span class="sxs-lookup"><span data-stu-id="151d9-163">(Normally, it's best to create a new resource.</span></span> <span data-ttu-id="151d9-164">Sélectionnez une ressource existante si vous avez déjà configuré des [tests web][availability] ou une [Surveillance du client][client] pour cette application.)</span><span class="sxs-lookup"><span data-stu-id="151d9-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Choisissez une application et une ressource.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="151d9-166">Redémarrez IIS.</span><span class="sxs-lookup"><span data-stu-id="151d9-166">Restart IIS.</span></span>

    ![Cliquez sur Redémarrer en haut de la boîte de dialogue.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="151d9-168">Votre service web sera interrompu pendant une courte période.</span><span class="sxs-lookup"><span data-stu-id="151d9-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="151d9-169">Personnaliser les options de surveillance</span><span class="sxs-lookup"><span data-stu-id="151d9-169">Customize monitoring options</span></span>

<span data-ttu-id="151d9-170">L’activation d’Application Insights ajoute des DLL et ApplicationInsights.config à votre application web.</span><span class="sxs-lookup"><span data-stu-id="151d9-170">Enabling Application Insights adds DLLs and ApplicationInsights.config to your web app.</span></span> <span data-ttu-id="151d9-171">Vous pouvez [modifier le fichier .config](app-insights-configuration-with-applicationinsights-config.md) pour changer certaines options.</span><span class="sxs-lookup"><span data-stu-id="151d9-171">You can [edit the .config file](app-insights-configuration-with-applicationinsights-config.md) to change some of the options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="151d9-172">Lorsque vous republiez votre application, réactivez Application Insights</span><span class="sxs-lookup"><span data-stu-id="151d9-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="151d9-173">Avant de republier votre application, vous pouvez [ajouter Application Insights au code dans Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="151d9-173">Before you re-publish your app, consider [adding Application Insights to the code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="151d9-174">Vous obtiendrez des données de télémétrie plus détaillées et aurez la possibilité de personnaliser la télémétrie à l’aide de code.</span><span class="sxs-lookup"><span data-stu-id="151d9-174">You'll get more detailed telemetry and the ability to write custom telemetry.</span></span>

<span data-ttu-id="151d9-175">Si vous souhaitez procéder à la republication sans ajouter Application Insights au code, sachez que le processus de déploiement peut supprimer les DLL et ApplicationInsights.config du site web publié.</span><span class="sxs-lookup"><span data-stu-id="151d9-175">If you want to re-publish without adding Application Insights to the code, be aware that the deployment process may delete the DLLs and ApplicationInsights.config from the published web site.</span></span> <span data-ttu-id="151d9-176">Par conséquent :</span><span class="sxs-lookup"><span data-stu-id="151d9-176">Therefore:</span></span>

1. <span data-ttu-id="151d9-177">Si vous avez modifié le fichier ApplicationInsights.config, copiez-le avant de republier votre application.</span><span class="sxs-lookup"><span data-stu-id="151d9-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="151d9-178">Republiez votre application.</span><span class="sxs-lookup"><span data-stu-id="151d9-178">Republish your app.</span></span>
3. <span data-ttu-id="151d9-179">Réactivez la surveillance d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="151d9-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="151d9-180">(Utilisez la méthode appropriée : le panneau de configuration de l’application web Azure ou Status Monitor sur un hôte IIS.)</span><span class="sxs-lookup"><span data-stu-id="151d9-180">(Use the appropriate method: either the Azure web app control panel, or the Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="151d9-181">Rétablissez les éventuelles modifications que vous avez effectuées dans le fichier .config.</span><span class="sxs-lookup"><span data-stu-id="151d9-181">Reinstate any edits you performed on the .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="151d9-182">Résolution des problèmes de configuration d’exécution d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="151d9-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="151d9-183">Vous n’arrivez pas à vous connecter ?</span><span class="sxs-lookup"><span data-stu-id="151d9-183">Can't connect?</span></span> <span data-ttu-id="151d9-184">Vous n’obtenez aucune donnée de télémétrie ?</span><span class="sxs-lookup"><span data-stu-id="151d9-184">No telemetry?</span></span>

* <span data-ttu-id="151d9-185">Ouvrez [les ports sortants requis](app-insights-ip-addresses.md#outgoing-ports) dans le pare-feu de votre serveur pour permettre à Status Monitor de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="151d9-185">Open [the necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall to allow Status Monitor to work.</span></span>

* <span data-ttu-id="151d9-186">Ouvrez Status Monitor et sélectionnez votre application dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="151d9-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="151d9-187">Vérifiez la présence de messages de diagnostic pour cette application dans la section « Notifications de configuration » :</span><span class="sxs-lookup"><span data-stu-id="151d9-187">Check if there are any diagnostics messages for this application in the "Configuration notifications" section:</span></span>

  ![Ouvrez le panneau des performances pour afficher la demande, le temps de réponse, la dépendance et d’autres données.](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="151d9-189">Si un message relatif à des « autorisations insuffisantes » s’affiche sur le serveur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="151d9-189">On the server, if you see a message about "insufficient permissions", try the following:</span></span>
  * <span data-ttu-id="151d9-190">Dans le Gestionnaire des services Internet, sélectionnez votre pool d’applications, ouvrez **Paramètres avancés** puis, sous **Modèle de processus**, notez l’identité.</span><span class="sxs-lookup"><span data-stu-id="151d9-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note the identity.</span></span>
  * <span data-ttu-id="151d9-191">Dans le panneau de configuration relatif à la gestion de l’ordinateur, ajoutez cette identité au groupe Utilisateurs de l’Analyseur de performances.</span><span class="sxs-lookup"><span data-stu-id="151d9-191">In Computer management control panel, add this identity to the Performance Monitor Users group.</span></span>
* <span data-ttu-id="151d9-192">Si des services MMA/SCOM (Systems Center Operations Manager) sont installés sur votre serveur, certaines versions peuvent entrer en conflit.</span><span class="sxs-lookup"><span data-stu-id="151d9-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="151d9-193">Désinstallez à la fois SCOM et Moniteur d’état, puis réinstallez des versions les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="151d9-193">Uninstall both SCOM and Status Monitor, and re-install the latest versions.</span></span>
* <span data-ttu-id="151d9-194">Consultez la rubrique [Résolution des problèmes][qna].</span><span class="sxs-lookup"><span data-stu-id="151d9-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="151d9-195">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="151d9-195">System Requirements</span></span>
<span data-ttu-id="151d9-196">Prise en charge du système d’exploitation pour Application Insights Status Monitor sur le serveur :</span><span class="sxs-lookup"><span data-stu-id="151d9-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="151d9-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="151d9-197">Windows Server 2008</span></span>
* <span data-ttu-id="151d9-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="151d9-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="151d9-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="151d9-199">Windows Server 2012</span></span>
* <span data-ttu-id="151d9-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="151d9-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="151d9-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="151d9-201">Windows Server 2016</span></span>

<span data-ttu-id="151d9-202">avec le dernier Service Pack et .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="151d9-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="151d9-203">Windows 7, 8, 8.1 et 10 côté client, avec également .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="151d9-203">On the client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="151d9-204">Prise en charge d’IIS : IIS 7, 7.5, 8, 8.5 (IIS requis)</span><span class="sxs-lookup"><span data-stu-id="151d9-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="151d9-205">Automation avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="151d9-205">Automation with PowerShell</span></span>
<span data-ttu-id="151d9-206">Vous pouvez démarrer et arrêter la surveillance à l’aide de PowerShell sur votre serveur IIS.</span><span class="sxs-lookup"><span data-stu-id="151d9-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="151d9-207">Tout d’abord, importez le module Application Insights :</span><span class="sxs-lookup"><span data-stu-id="151d9-207">First import the Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="151d9-208">Identifiez les applications qui sont surveillées :</span><span class="sxs-lookup"><span data-stu-id="151d9-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="151d9-209">`-Name` (Facultatif) Nom d’une application web.</span><span class="sxs-lookup"><span data-stu-id="151d9-209">`-Name` (Optional) The name of a web app.</span></span>
* <span data-ttu-id="151d9-210">Affiche l’état de la surveillance Application Insights pour chaque application web (ou l’application nommée) dans ce serveur IIS.</span><span class="sxs-lookup"><span data-stu-id="151d9-210">Displays the Application Insights monitoring status for each web app (or the named app) in this IIS server.</span></span>
* <span data-ttu-id="151d9-211">Retourne `ApplicationInsightsApplication` pour chaque application :</span><span class="sxs-lookup"><span data-stu-id="151d9-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="151d9-212">`SdkState==EnabledAfterDeployment` : l’application est surveillée et a été instrumentée lors de l’exécution par l’outil Status Monitor ou par `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="151d9-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by the Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="151d9-213">`SdkState==Disabled`: l’application n’est pas instrumentée pour Application Insights.</span><span class="sxs-lookup"><span data-stu-id="151d9-213">`SdkState==Disabled`: The app is not instrumented for Application Insights.</span></span> <span data-ttu-id="151d9-214">Soit elle n’a jamais été instrumentée, soit la surveillance lors de l’exécution a été désactivée avec l’outil Status Monitor ou avec `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="151d9-214">Either it was never instrumented, or run-time monitoring was disabled with the Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="151d9-215">`SdkState==EnabledByCodeInstrumentation`: l’application a été instrumentée en ajoutant le Kit de développement logiciel (SDK) au code source.</span><span class="sxs-lookup"><span data-stu-id="151d9-215">`SdkState==EnabledByCodeInstrumentation`: The app was instrumented by adding the SDK to the source code.</span></span> <span data-ttu-id="151d9-216">Son Kit de développement logiciel (SDK) ne peut pas être mis à jour ou arrêté.</span><span class="sxs-lookup"><span data-stu-id="151d9-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="151d9-217">`SdkVersion` affiche la version utilisée pour surveiller cette application.</span><span class="sxs-lookup"><span data-stu-id="151d9-217">`SdkVersion` shows the version in use for monitoring this app.</span></span>
  * <span data-ttu-id="151d9-218">`LatestAvailableSdkVersion`affiche la version actuellement disponible dans la galerie NuGet.</span><span class="sxs-lookup"><span data-stu-id="151d9-218">`LatestAvailableSdkVersion`shows the version currently available on the NuGet gallery.</span></span> <span data-ttu-id="151d9-219">Pour mettre à niveau l’application vers cette version, utilisez `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="151d9-219">To upgrade the app to this version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="151d9-220">`-Name` Nom de l’application dans IIS</span><span class="sxs-lookup"><span data-stu-id="151d9-220">`-Name` The name of the app in IIS</span></span>
* <span data-ttu-id="151d9-221">`-InstrumentationKey` Ikey de la ressource Application Insights où vous souhaitez afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="151d9-221">`-InstrumentationKey` The ikey of the Application Insights resource where you want the results to be displayed.</span></span>
* <span data-ttu-id="151d9-222">Cette applet de commande affecte uniquement les applications qui ne sont pas déjà instrumentées, c’est-à-dire SdkState==NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="151d9-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="151d9-223">L’applet de commande n’affecte pas une application qui est déjà instrumentée,</span><span class="sxs-lookup"><span data-stu-id="151d9-223">The cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="151d9-224">que ce soit au moment de la création en ajoutant le Kit de développement logiciel (SDK) au code ou au moment de l’exécution via une utilisation préalable de cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="151d9-224">It does not matter whether the app was instrumented at build time by adding the SDK to the code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="151d9-225">La version du Kit de développement logiciel (SDK) utilisée pour instrumenter l’application est la version la plus récente téléchargée sur ce serveur.</span><span class="sxs-lookup"><span data-stu-id="151d9-225">The SDK version used to instrument the app is the version that was most recently downloaded to this server.</span></span>

    <span data-ttu-id="151d9-226">Pour télécharger la version la plus récente, utilisez Update-ApplicationInsightsVersion.</span><span class="sxs-lookup"><span data-stu-id="151d9-226">To download the latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="151d9-227">Retourne `ApplicationInsightsApplication` en cas de réussite.</span><span class="sxs-lookup"><span data-stu-id="151d9-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="151d9-228">En cas d’échec, il consigne un suivi sur stderr.</span><span class="sxs-lookup"><span data-stu-id="151d9-228">If it fails, it logs a trace to stderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="151d9-229">`-Name` Nom d’une application dans IIS</span><span class="sxs-lookup"><span data-stu-id="151d9-229">`-Name` The name of an app in IIS</span></span>
* <span data-ttu-id="151d9-230">`-All` Arrête la surveillance de toutes les applications de ce serveur IIS pour lequel `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="151d9-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="151d9-231">Arrête la surveillance des applications spécifiées et supprime l’instrumentation.</span><span class="sxs-lookup"><span data-stu-id="151d9-231">Stops monitoring the specified apps and removes instrumentation.</span></span> <span data-ttu-id="151d9-232">Cela ne fonctionne que pour les applications qui ont été instrumentées lors de l’exécution avec l’outil Status Monitor ou avec Start-ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="151d9-232">It only works for apps that have been instrumented at run-time using the Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="151d9-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="151d9-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="151d9-234">Renvoie ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="151d9-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="151d9-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="151d9-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="151d9-236">`-Name` : nom d’une application web dans IIS.</span><span class="sxs-lookup"><span data-stu-id="151d9-236">`-Name`: The name of a web app in IIS.</span></span>
* <span data-ttu-id="151d9-237">`-InstrumentationKey` (Facultatif.) Permet de modifier la ressource à laquelle la télémétrie de l’application est envoyée.</span><span class="sxs-lookup"><span data-stu-id="151d9-237">`-InstrumentationKey` (Optional.) Use this to change the resource to which the app's telemetry is sent.</span></span>
* <span data-ttu-id="151d9-238">Cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="151d9-238">This cmdlet:</span></span>
  * <span data-ttu-id="151d9-239">Met à niveau l’application nommée vers la version la plus récente du Kit de développement logiciel (SDK) téléchargée sur cette machine.</span><span class="sxs-lookup"><span data-stu-id="151d9-239">Upgrades the named app to the version of the SDK most recently downloaded to this machine.</span></span> <span data-ttu-id="151d9-240">(Ne fonctionne que si `SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="151d9-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="151d9-241">Si vous fournissez une clé d’instrumentation, l’application nommée est reconfigurée pour envoyer la télémétrie à la ressource avec cette clé.</span><span class="sxs-lookup"><span data-stu-id="151d9-241">If you provide an instrumentation key, the named app is reconfigured to send telemetry to the resource with that key.</span></span> <span data-ttu-id="151d9-242">(Fonctionne si `SdkState != Disabled`)</span><span class="sxs-lookup"><span data-stu-id="151d9-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="151d9-243">Télécharge la version la plus récente du Kit de développement logiciel (SDK) Application Insights sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="151d9-243">Downloads the latest Application Insights SDK to the server.</span></span>

## <span data-ttu-id="151d9-244"><a name="questions"></a>Questions sur Status Monitor</span><span class="sxs-lookup"><span data-stu-id="151d9-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="151d9-245">Qu’est-ce que Status Monitor ?</span><span class="sxs-lookup"><span data-stu-id="151d9-245">What is Status Monitor?</span></span>

<span data-ttu-id="151d9-246">Il s’agit d’une application de bureau que vous installez sur votre serveur web IIS.</span><span class="sxs-lookup"><span data-stu-id="151d9-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="151d9-247">Il vous permet d’instrumenter et de configurer des applications web.</span><span class="sxs-lookup"><span data-stu-id="151d9-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="151d9-248">Quand dois-je utiliser Status Monitor ?</span><span class="sxs-lookup"><span data-stu-id="151d9-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="151d9-249">Vous pouvez l’utiliser pour instrumenter une application web qui s’exécute sur votre serveur IIS, même si elle est déjà en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="151d9-249">To instrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="151d9-250">Vous pouvez également vous en servir pour activer la télémétrie supplémentaire pour les applications web qui ont été [générées avec le Kit de développement logiciel (SDK) Application Insights](app-insights-asp-net.md) au moment de la compilation.</span><span class="sxs-lookup"><span data-stu-id="151d9-250">To enable additional telemetry for web apps that have been [built with the Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="151d9-251">Puis-je le fermer il après son exécution ?</span><span class="sxs-lookup"><span data-stu-id="151d9-251">Can I close it after it runs?</span></span>

<span data-ttu-id="151d9-252">Oui.</span><span class="sxs-lookup"><span data-stu-id="151d9-252">Yes.</span></span> <span data-ttu-id="151d9-253">Une fois qu’il a instrumenté les sites web que vous avez sélectionnés, vous pouvez le fermer.</span><span class="sxs-lookup"><span data-stu-id="151d9-253">After it has instrumented the websites you select, you can close it.</span></span>

<span data-ttu-id="151d9-254">Il ne collecte pas la télémétrie par lui-même.</span><span class="sxs-lookup"><span data-stu-id="151d9-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="151d9-255">Il configure simplement les applications web et définit certaines autorisations.</span><span class="sxs-lookup"><span data-stu-id="151d9-255">It just configures the web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="151d9-256">Que fait Status Monitor ?</span><span class="sxs-lookup"><span data-stu-id="151d9-256">What does Status Monitor do?</span></span>

<span data-ttu-id="151d9-257">Lorsque vous sélectionnez une application web que Status Monitor doit instrumenter :</span><span class="sxs-lookup"><span data-stu-id="151d9-257">When you select a web app for Status Monitor to instrument:</span></span>

* <span data-ttu-id="151d9-258">Celui-ci télécharge et place les assemblys Application Insights et le fichier .config dans le dossier de fichiers binaires de l’application web.</span><span class="sxs-lookup"><span data-stu-id="151d9-258">Downloads and places the Application Insights assemblies and .config file in the web app's binaries folder.</span></span>
* <span data-ttu-id="151d9-259">Il modifie `web.config` pour ajouter le module de suivi HTTP Application Insights.</span><span class="sxs-lookup"><span data-stu-id="151d9-259">Modifies `web.config` to add the Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="151d9-260">Il active le profilage CLR pour collecter les appels de dépendance.</span><span class="sxs-lookup"><span data-stu-id="151d9-260">Enables CLR profiling to collect dependency calls.</span></span>

### <a name="do-i-need-to-run-status-monitor-whenever-i-update-the-app"></a><span data-ttu-id="151d9-261">Dois-je exécuter Status Monitor à chaque mise à jour d’une application ?</span><span class="sxs-lookup"><span data-stu-id="151d9-261">Do I need to run Status Monitor whenever I update the app?</span></span>

<span data-ttu-id="151d9-262">Cela n’est pas nécessaire si vous la redéployez de façon incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="151d9-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="151d9-263">Si vous sélectionnez l’option « Supprimer les fichiers existants » dans le processus de publication, vous devrez à nouveau exécuter Status Monitor pour configurer Application Insights.</span><span class="sxs-lookup"><span data-stu-id="151d9-263">If you select the 'delete existing files' option in the publish process, you would need to re-run Status Monitor to configure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="151d9-264">Quel type de télémétrie est collecté ?</span><span class="sxs-lookup"><span data-stu-id="151d9-264">What telemetry is collected?</span></span>

<span data-ttu-id="151d9-265">Pour les applications que vous instrumentez uniquement au moment de l’exécution à l’aide de Status Monitor :</span><span class="sxs-lookup"><span data-stu-id="151d9-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="151d9-266">Des requêtes HTTP</span><span class="sxs-lookup"><span data-stu-id="151d9-266">HTTP requests</span></span>
* <span data-ttu-id="151d9-267">Des appels de dépendances</span><span class="sxs-lookup"><span data-stu-id="151d9-267">Calls to dependencies</span></span>
* <span data-ttu-id="151d9-268">Exceptions</span><span class="sxs-lookup"><span data-stu-id="151d9-268">Exceptions</span></span>
* <span data-ttu-id="151d9-269">Compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="151d9-269">Performance counters</span></span>

<span data-ttu-id="151d9-270">Pour les applications déjà instrumentées au moment de la compilation :</span><span class="sxs-lookup"><span data-stu-id="151d9-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="151d9-271">Des compteurs de processus.</span><span class="sxs-lookup"><span data-stu-id="151d9-271">Process counters.</span></span>
 * <span data-ttu-id="151d9-272">Des appels de dépendances (.NET 4.5) ; des valeurs de retour dans des appels de dépendances (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="151d9-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="151d9-273">Des valeurs d’arborescence des appels de procédure d’exception.</span><span class="sxs-lookup"><span data-stu-id="151d9-273">Exception stack trace values.</span></span>

[<span data-ttu-id="151d9-274">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="151d9-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="151d9-275">Vidéo</span><span class="sxs-lookup"><span data-stu-id="151d9-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="151d9-276"><a name="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="151d9-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="151d9-277">Affichez vos données de télémétrie :</span><span class="sxs-lookup"><span data-stu-id="151d9-277">View your telemetry:</span></span>

* <span data-ttu-id="151d9-278">[Explorez les mesures](app-insights-metrics-explorer.md) pour surveiller les performances et l’utilisation</span><span class="sxs-lookup"><span data-stu-id="151d9-278">[Explore metrics](app-insights-metrics-explorer.md) to monitor performance and usage</span></span>
* <span data-ttu-id="151d9-279">[Effectuez des recherches dans les événements et les journaux][diagnostic] pour diagnostiquer les problèmes</span><span class="sxs-lookup"><span data-stu-id="151d9-279">[Search events and logs][diagnostic] to diagnose problems</span></span>
* <span data-ttu-id="151d9-280">[Utilisez la fonctionnalité Analytics](app-insights-analytics.md) pour des requêtes plus élaborées</span><span class="sxs-lookup"><span data-stu-id="151d9-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="151d9-281">Créez des tableaux de bord</span><span class="sxs-lookup"><span data-stu-id="151d9-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="151d9-282">Ajoutez des données de télémétrie :</span><span class="sxs-lookup"><span data-stu-id="151d9-282">Add more telemetry:</span></span>

* <span data-ttu-id="151d9-283">[Créez des tests web][availability] pour vous assurer que votre site reste actif.</span><span class="sxs-lookup"><span data-stu-id="151d9-283">[Create web tests][availability] to make sure your site stays live.</span></span>
* <span data-ttu-id="151d9-284">[Ajoutez la télémétrie de client web][usage] pour afficher les exceptions à partir du code de la page web et vous permettre d’insérer un suivi des appels.</span><span class="sxs-lookup"><span data-stu-id="151d9-284">[Add web client telemetry][usage] to see exceptions from web page code and to let you insert trace calls.</span></span>
* <span data-ttu-id="151d9-285">[Ajoutez le Kit de développement logiciel (SDK) Application Insights à votre code][greenbrown] afin de pouvoir insérer un suivi et des appels de journaux</span><span class="sxs-lookup"><span data-stu-id="151d9-285">[Add Application Insights SDK to your code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
