---
title: aaaMonitor un dynamique ASP.NET web application avec Azure Application Insights | Documents Microsoft
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
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="61f82-104">Instrumenter des applications web lors de l’exécution avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="61f82-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="61f82-105">Vous pouvez instrumenter une application web dynamique avec Azure Application Insights, sans avoir toomodify ou redéployer votre code.</span><span class="sxs-lookup"><span data-stu-id="61f82-105">You can instrument a live web app with Azure Application Insights, without having toomodify or redeploy your code.</span></span> <span data-ttu-id="61f82-106">Si vos applications sont hébergées sur un serveur IIS local, installez Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="61f82-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="61f82-107">S’ils sont des applications web Azure ou que vous exécutent dans une machine virtuelle Azure, vous pouvez basculer sur la surveillance de l’Application Insights à partir du Panneau de configuration Azure hello.</span><span class="sxs-lookup"><span data-stu-id="61f82-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from hello Azure control panel.</span></span> <span data-ttu-id="61f82-108">(Des articles distincts sont également consacrés à l’instrumentation des [applications web J2EE actives](app-insights-java-live.md) et [d’Azure Cloud Services](app-insights-cloudservices.md).) Cette opération nécessite un abonnement [Microsoft Azure](http://azure.com) .</span><span class="sxs-lookup"><span data-stu-id="61f82-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![Exemples de graphiques](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="61f82-110">Vous avez le choix entre trois itinéraires tooapply Application Insights tooyour .NET web applications :</span><span class="sxs-lookup"><span data-stu-id="61f82-110">You have a choice of three routes tooapply Application Insights tooyour .NET web applications:</span></span>

* <span data-ttu-id="61f82-111">**Heure de création :** [hello d’ajouter Application Insights SDK] [ greenbrown] code d’application web tooyour.</span><span class="sxs-lookup"><span data-stu-id="61f82-111">**Build time:** [Add hello Application Insights SDK][greenbrown] tooyour web app code.</span></span>
* <span data-ttu-id="61f82-112">**Durée d’exécution :** instrumenter votre application web sur le serveur de hello, comme décrit ci-dessous, sans régénérer et redéployer les code hello.</span><span class="sxs-lookup"><span data-stu-id="61f82-112">**Run time:** Instrument your web app on hello server, as described below, without rebuilding and redeploying hello code.</span></span>
* <span data-ttu-id="61f82-113">**Les deux :** générer hello SDK dans votre code d’application web et s’appliquent également des extensions d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="61f82-113">**Both:** Build hello SDK into your web app code, and also apply hello run-time extensions.</span></span> <span data-ttu-id="61f82-114">Obtenir hello meilleur des deux options.</span><span class="sxs-lookup"><span data-stu-id="61f82-114">Get hello best of both options.</span></span>

<span data-ttu-id="61f82-115">Voici un résumé de ce que vous apporte chaque méthode :</span><span class="sxs-lookup"><span data-stu-id="61f82-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="61f82-116">En cours de création</span><span class="sxs-lookup"><span data-stu-id="61f82-116">Build time</span></span> | <span data-ttu-id="61f82-117">En cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="61f82-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61f82-118">Requêtes et exceptions</span><span class="sxs-lookup"><span data-stu-id="61f82-118">Requests & exceptions</span></span> |<span data-ttu-id="61f82-119">Oui</span><span class="sxs-lookup"><span data-stu-id="61f82-119">Yes</span></span> |<span data-ttu-id="61f82-120">Oui</span><span class="sxs-lookup"><span data-stu-id="61f82-120">Yes</span></span> |
| [<span data-ttu-id="61f82-121">Exceptions plus détaillées</span><span class="sxs-lookup"><span data-stu-id="61f82-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="61f82-122">Oui</span><span class="sxs-lookup"><span data-stu-id="61f82-122">Yes</span></span> |
| [<span data-ttu-id="61f82-123">Diagnostics de dépendance</span><span class="sxs-lookup"><span data-stu-id="61f82-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="61f82-124">Sur .NET 4.6 +, mais moins détaillé</span><span class="sxs-lookup"><span data-stu-id="61f82-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="61f82-125">Oui, tous les détails : codes de résultat, texte de commande SQL, verbe HTTP</span><span class="sxs-lookup"><span data-stu-id="61f82-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="61f82-126">Compteurs de performances système</span><span class="sxs-lookup"><span data-stu-id="61f82-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="61f82-127">Oui</span><span class="sxs-lookup"><span data-stu-id="61f82-127">Yes</span></span> |<span data-ttu-id="61f82-128">Oui</span><span class="sxs-lookup"><span data-stu-id="61f82-128">Yes</span></span> |
| <span data-ttu-id="61f82-129">[API pour la télémétrie personnalisée][api]</span><span class="sxs-lookup"><span data-stu-id="61f82-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="61f82-130">Oui</span><span class="sxs-lookup"><span data-stu-id="61f82-130">Yes</span></span> |<span data-ttu-id="61f82-131">Non</span><span class="sxs-lookup"><span data-stu-id="61f82-131">No</span></span> |
| [<span data-ttu-id="61f82-132">Intégration des journaux de suivi</span><span class="sxs-lookup"><span data-stu-id="61f82-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="61f82-133">Oui</span><span class="sxs-lookup"><span data-stu-id="61f82-133">Yes</span></span> |<span data-ttu-id="61f82-134">Non</span><span class="sxs-lookup"><span data-stu-id="61f82-134">No</span></span> |
| [<span data-ttu-id="61f82-135">Mode Page et données utilisateur</span><span class="sxs-lookup"><span data-stu-id="61f82-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="61f82-136">Oui</span><span class="sxs-lookup"><span data-stu-id="61f82-136">Yes</span></span> |<span data-ttu-id="61f82-137">Non</span><span class="sxs-lookup"><span data-stu-id="61f82-137">No</span></span> |
| <span data-ttu-id="61f82-138">Besoin de code toorebuild</span><span class="sxs-lookup"><span data-stu-id="61f82-138">Need toorebuild code</span></span> |<span data-ttu-id="61f82-139">Oui</span><span class="sxs-lookup"><span data-stu-id="61f82-139">Yes</span></span> | <span data-ttu-id="61f82-140">Non</span><span class="sxs-lookup"><span data-stu-id="61f82-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="61f82-141">Surveiller une application web Azure active</span><span class="sxs-lookup"><span data-stu-id="61f82-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="61f82-142">Si votre application s’exécute en tant que Azure d’un service web, voici comment tooswitch sur la surveillance :</span><span class="sxs-lookup"><span data-stu-id="61f82-142">If your application is running as an Azure web service, here's how tooswitch on monitoring:</span></span>

* <span data-ttu-id="61f82-143">Sélectionnez l’Application Insights sur le panneau de configuration l’application hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="61f82-143">Select Application Insights on hello app's control panel in Azure.</span></span>

    ![Configurer Application Insights pour une application web Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="61f82-145">Lors de la page de résumé Application Insights hello s’ouvre, cliquez sur le lien de hello en hello bas tooopen hello complète ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="61f82-145">When hello Application Insights summary page opens, click hello link at hello bottom tooopen hello full Application Insights resource.</span></span>

    ![Parcourez tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="61f82-147">[Surveillance des applications de machine virtuelle et cloud](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="61f82-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="61f82-148">Activation de la surveillance côté client dans Azure</span><span class="sxs-lookup"><span data-stu-id="61f82-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="61f82-149">Si vous avez activé Application Insights dans Azure, vous pouvez ajouter la consultation de page et la télémétrie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="61f82-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="61f82-150">Cliquez sur Paramètres > Paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="61f82-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="61f82-151">Sous Paramètres de l’application, ajoutez une nouvelle paire clé/valeur :</span><span class="sxs-lookup"><span data-stu-id="61f82-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="61f82-152">Clé :`APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="61f82-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="61f82-153">Valeur: `true`</span><span class="sxs-lookup"><span data-stu-id="61f82-153">Value: `true`</span></span>
3. <span data-ttu-id="61f82-154">**Enregistrer** hello paramètres et **redémarrer** votre application.</span><span class="sxs-lookup"><span data-stu-id="61f82-154">**Save** hello settings and **Restart** your app.</span></span>

<span data-ttu-id="61f82-155">Hello SDK de JavaScript Application Insights est désormais injecté dans chaque page web.</span><span class="sxs-lookup"><span data-stu-id="61f82-155">hello Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="61f82-156">Surveiller une application web IIS active</span><span class="sxs-lookup"><span data-stu-id="61f82-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="61f82-157">Si votre application est hébergée sur un serveur IIS, activez Application Insights à l’aide de Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="61f82-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="61f82-158">Sur votre serveur web IIS, connectez-vous avec vos informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="61f82-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="61f82-159">Si l’Application Insights Status Monitor n’est pas déjà installé, téléchargez et exécutez hello [programme d’installation du moniteur d’état](http://go.microsoft.com/fwlink/?LinkId=506648) (ou exécutez [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) et recherchez Application Insights état qu’il contient Moniteur).</span><span class="sxs-lookup"><span data-stu-id="61f82-159">If Application Insights Status Monitor is not already installed, download and run hello [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="61f82-160">Dans le moniteur d’état, sélectionnez application hello installé ou site Web que vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="61f82-160">In Status Monitor, select hello installed web application or website that you want toomonitor.</span></span> <span data-ttu-id="61f82-161">Connectez-vous avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="61f82-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="61f82-162">Configurez la ressource hello où vous intéresse toosee hello portail Application Insights de hello.</span><span class="sxs-lookup"><span data-stu-id="61f82-162">Configure hello resource where you want toosee hello results in hello Application Insights portal.</span></span> <span data-ttu-id="61f82-163">(Normalement, il est meilleure toocreate une nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="61f82-163">(Normally, it's best toocreate a new resource.</span></span> <span data-ttu-id="61f82-164">Sélectionnez une ressource existante si vous avez déjà configuré des [tests web][availability] ou une [Surveillance du client][client] pour cette application.)</span><span class="sxs-lookup"><span data-stu-id="61f82-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Choisissez une application et une ressource.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="61f82-166">Redémarrez IIS.</span><span class="sxs-lookup"><span data-stu-id="61f82-166">Restart IIS.</span></span>

    ![Cliquez sur Redémarrer haut hello de boîte de dialogue hello.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="61f82-168">Votre service web sera interrompu pendant une courte période.</span><span class="sxs-lookup"><span data-stu-id="61f82-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="61f82-169">Personnaliser les options de surveillance</span><span class="sxs-lookup"><span data-stu-id="61f82-169">Customize monitoring options</span></span>

<span data-ttu-id="61f82-170">L’activation d’Application Insights ajoute des DLL et ApplicationInsights.config tooyour l’application web.</span><span class="sxs-lookup"><span data-stu-id="61f82-170">Enabling Application Insights adds DLLs and ApplicationInsights.config tooyour web app.</span></span> <span data-ttu-id="61f82-171">Vous pouvez [modifier le fichier .config de hello](app-insights-configuration-with-applicationinsights-config.md) toochange certaines des options de hello.</span><span class="sxs-lookup"><span data-stu-id="61f82-171">You can [edit hello .config file](app-insights-configuration-with-applicationinsights-config.md) toochange some of hello options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="61f82-172">Lorsque vous republiez votre application, réactivez Application Insights</span><span class="sxs-lookup"><span data-stu-id="61f82-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="61f82-173">Avant de vous republiez votre application, pensez à [Ajout de code d’Application Insights toohello dans Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="61f82-173">Before you re-publish your app, consider [adding Application Insights toohello code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="61f82-174">Vous obtenez la télémétrie plus détaillée et une télémétrie personnalisée hello capacité toowrite.</span><span class="sxs-lookup"><span data-stu-id="61f82-174">You'll get more detailed telemetry and hello ability toowrite custom telemetry.</span></span>

<span data-ttu-id="61f82-175">Si vous souhaitez que toore-publier sans ajouter Application Insights toohello code, n’oubliez pas que les processus de déploiement hello peuvent supprimer les DLL hello et ApplicationInsights.config de hello publié le site web.</span><span class="sxs-lookup"><span data-stu-id="61f82-175">If you want toore-publish without adding Application Insights toohello code, be aware that hello deployment process may delete hello DLLs and ApplicationInsights.config from hello published web site.</span></span> <span data-ttu-id="61f82-176">Par conséquent :</span><span class="sxs-lookup"><span data-stu-id="61f82-176">Therefore:</span></span>

1. <span data-ttu-id="61f82-177">Si vous avez modifié le fichier ApplicationInsights.config, copiez-le avant de republier votre application.</span><span class="sxs-lookup"><span data-stu-id="61f82-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="61f82-178">Republiez votre application.</span><span class="sxs-lookup"><span data-stu-id="61f82-178">Republish your app.</span></span>
3. <span data-ttu-id="61f82-179">Réactivez la surveillance d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="61f82-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="61f82-180">(Utilisez la méthode appropriée de hello : hello Azure web app le panneau de configuration ou de hello Status Monitor sur un ordinateur hôte IIS.)</span><span class="sxs-lookup"><span data-stu-id="61f82-180">(Use hello appropriate method: either hello Azure web app control panel, or hello Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="61f82-181">Rétablir les modifications que vous avez effectué sur le fichier .config de hello.</span><span class="sxs-lookup"><span data-stu-id="61f82-181">Reinstate any edits you performed on hello .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="61f82-182">Résolution des problèmes de configuration d’exécution d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="61f82-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="61f82-183">Vous n’arrivez pas à vous connecter ?</span><span class="sxs-lookup"><span data-stu-id="61f82-183">Can't connect?</span></span> <span data-ttu-id="61f82-184">Vous n’obtenez aucune donnée de télémétrie ?</span><span class="sxs-lookup"><span data-stu-id="61f82-184">No telemetry?</span></span>

* <span data-ttu-id="61f82-185">Ouvrez [hello ports sortants nécessaires](app-insights-ip-addresses.md#outgoing-ports) dans toowork de moniteur d’état de votre serveur pare-feu tooallow.</span><span class="sxs-lookup"><span data-stu-id="61f82-185">Open [hello necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall tooallow Status Monitor toowork.</span></span>

* <span data-ttu-id="61f82-186">Ouvrez Status Monitor et sélectionnez votre application dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="61f82-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="61f82-187">Vérifiez la présence des messages de diagnostic pour cette application Bonjour section « Configuration de notifications » :</span><span class="sxs-lookup"><span data-stu-id="61f82-187">Check if there are any diagnostics messages for this application in hello "Configuration notifications" section:</span></span>

  ![Demande de toosee panneau hello ouvrir performances, temps de réponse, dépendances et autres données](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="61f82-189">Sur le serveur de hello, si vous voyez un message sur « Autorisations insuffisantes », essayez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="61f82-189">On hello server, if you see a message about "insufficient permissions", try hello following:</span></span>
  * <span data-ttu-id="61f82-190">Dans le Gestionnaire des services Internet, sélectionnez le pool d’applications, ouvrez **paramètres avancés**et sous **modèle de processus** Notez l’identité de hello.</span><span class="sxs-lookup"><span data-stu-id="61f82-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note hello identity.</span></span>
  * <span data-ttu-id="61f82-191">Dans le panneau de configuration ordinateur gestion, ajoutez cet identité toohello groupe.</span><span class="sxs-lookup"><span data-stu-id="61f82-191">In Computer management control panel, add this identity toohello Performance Monitor Users group.</span></span>
* <span data-ttu-id="61f82-192">Si des services MMA/SCOM (Systems Center Operations Manager) sont installés sur votre serveur, certaines versions peuvent entrer en conflit.</span><span class="sxs-lookup"><span data-stu-id="61f82-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="61f82-193">Désinstallez SCOM et le moniteur d’état et réinstallez les versions les plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="61f82-193">Uninstall both SCOM and Status Monitor, and re-install hello latest versions.</span></span>
* <span data-ttu-id="61f82-194">Consultez la rubrique [Résolution des problèmes][qna].</span><span class="sxs-lookup"><span data-stu-id="61f82-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="61f82-195">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="61f82-195">System Requirements</span></span>
<span data-ttu-id="61f82-196">Prise en charge du système d’exploitation pour Application Insights Status Monitor sur le serveur :</span><span class="sxs-lookup"><span data-stu-id="61f82-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="61f82-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="61f82-197">Windows Server 2008</span></span>
* <span data-ttu-id="61f82-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="61f82-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="61f82-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="61f82-199">Windows Server 2012</span></span>
* <span data-ttu-id="61f82-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="61f82-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="61f82-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="61f82-201">Windows Server 2016</span></span>

<span data-ttu-id="61f82-202">avec le dernier Service Pack et .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="61f82-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="61f82-203">Côté client de hello : Windows 7, 8, 8.1 et 10, à l’aide de .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="61f82-203">On hello client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="61f82-204">Prise en charge d’IIS : IIS 7, 7.5, 8, 8.5 (IIS requis)</span><span class="sxs-lookup"><span data-stu-id="61f82-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="61f82-205">Automation avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="61f82-205">Automation with PowerShell</span></span>
<span data-ttu-id="61f82-206">Vous pouvez démarrer et arrêter la surveillance à l’aide de PowerShell sur votre serveur IIS.</span><span class="sxs-lookup"><span data-stu-id="61f82-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="61f82-207">Module d’Application Insights hello d’abord importer :</span><span class="sxs-lookup"><span data-stu-id="61f82-207">First import hello Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="61f82-208">Identifiez les applications qui sont surveillées :</span><span class="sxs-lookup"><span data-stu-id="61f82-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="61f82-209">`-Name`Nom hello (facultatif) d’une application web.</span><span class="sxs-lookup"><span data-stu-id="61f82-209">`-Name` (Optional) hello name of a web app.</span></span>
* <span data-ttu-id="61f82-210">Affiche hello état d’analyse pour chaque application web (ou hello nommé app) Application Insights dans ce serveur IIS.</span><span class="sxs-lookup"><span data-stu-id="61f82-210">Displays hello Application Insights monitoring status for each web app (or hello named app) in this IIS server.</span></span>
* <span data-ttu-id="61f82-211">Retourne `ApplicationInsightsApplication` pour chaque application :</span><span class="sxs-lookup"><span data-stu-id="61f82-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="61f82-212">`SdkState==EnabledAfterDeployment`: Application en cours d’analyse et a été instrumentée en cours d’exécution, soit par l’outil d’analyse de l’état de hello, soit en `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="61f82-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by hello Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="61f82-213">`SdkState==Disabled`: application hello n’est pas instrumentée pour Application Insights.</span><span class="sxs-lookup"><span data-stu-id="61f82-213">`SdkState==Disabled`: hello app is not instrumented for Application Insights.</span></span> <span data-ttu-id="61f82-214">Il a été instrumenté jamais, ou analyse de l’exécution a été désactivée avec l’outil d’analyse d’état hello ou `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="61f82-214">Either it was never instrumented, or run-time monitoring was disabled with hello Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="61f82-215">`SdkState==EnabledByCodeInstrumentation`: application hello a été instrumentée en ajoutant le code source de hello SDK toohello.</span><span class="sxs-lookup"><span data-stu-id="61f82-215">`SdkState==EnabledByCodeInstrumentation`: hello app was instrumented by adding hello SDK toohello source code.</span></span> <span data-ttu-id="61f82-216">Son Kit de développement logiciel (SDK) ne peut pas être mis à jour ou arrêté.</span><span class="sxs-lookup"><span data-stu-id="61f82-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="61f82-217">`SdkVersion`Affiche la version de hello en cours d’utilisation pour l’analyse de cette application.</span><span class="sxs-lookup"><span data-stu-id="61f82-217">`SdkVersion` shows hello version in use for monitoring this app.</span></span>
  * <span data-ttu-id="61f82-218">`LatestAvailableSdkVersion`Affiche la version hello actuellement disponible dans la galerie NuGet de hello.</span><span class="sxs-lookup"><span data-stu-id="61f82-218">`LatestAvailableSdkVersion`shows hello version currently available on hello NuGet gallery.</span></span> <span data-ttu-id="61f82-219">version de toothis application tooupgrade hello, utilisez `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="61f82-219">tooupgrade hello app toothis version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="61f82-220">`-Name`nom Hello de l’application hello dans IIS</span><span class="sxs-lookup"><span data-stu-id="61f82-220">`-Name` hello name of hello app in IIS</span></span>
* <span data-ttu-id="61f82-221">`-InstrumentationKey`Bonjour ikey Hello ressource Application Insights où vous souhaitez hello toobe de résultats affiché.</span><span class="sxs-lookup"><span data-stu-id="61f82-221">`-InstrumentationKey` hello ikey of hello Application Insights resource where you want hello results toobe displayed.</span></span>
* <span data-ttu-id="61f82-222">Cette applet de commande affecte uniquement les applications qui ne sont pas déjà instrumentées, c’est-à-dire SdkState==NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="61f82-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="61f82-223">applet de commande Hello n’affecte pas une application qui est déjà instrumentée.</span><span class="sxs-lookup"><span data-stu-id="61f82-223">hello cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="61f82-224">Il ne pas important que l’application hello a été instrumentée au moment de la génération en ajoutant le code de toohello hello SDK, ou au moment de l’exécution par l’utilisation précédente de cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="61f82-224">It does not matter whether hello app was instrumented at build time by adding hello SDK toohello code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="61f82-225">application de hello tooinstrument Hello SDK version utilisée est version hello qui a été la plus récemment téléchargé toothis server.</span><span class="sxs-lookup"><span data-stu-id="61f82-225">hello SDK version used tooinstrument hello app is hello version that was most recently downloaded toothis server.</span></span>

    <span data-ttu-id="61f82-226">version la plus récente toodownload hello, utilisez ApplicationInsightsVersion de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="61f82-226">toodownload hello latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="61f82-227">Retourne `ApplicationInsightsApplication` en cas de réussite.</span><span class="sxs-lookup"><span data-stu-id="61f82-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="61f82-228">En cas d’échec, il connecte à un toostderr de trace.</span><span class="sxs-lookup"><span data-stu-id="61f82-228">If it fails, it logs a trace toostderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="61f82-229">`-Name`nom Hello d’une application dans IIS</span><span class="sxs-lookup"><span data-stu-id="61f82-229">`-Name` hello name of an app in IIS</span></span>
* <span data-ttu-id="61f82-230">`-All` Arrête la surveillance de toutes les applications de ce serveur IIS pour lequel `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="61f82-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="61f82-231">Arrête l’analyse hello applications spécifiées et supprime l’instrumentation.</span><span class="sxs-lookup"><span data-stu-id="61f82-231">Stops monitoring hello specified apps and removes instrumentation.</span></span> <span data-ttu-id="61f82-232">Il fonctionne uniquement pour les applications qui ont été instrumentées au moment de l’exécution à l’aide hello outil de surveillance de l’état ou ApplicationInsightsApplication de début.</span><span class="sxs-lookup"><span data-stu-id="61f82-232">It only works for apps that have been instrumented at run-time using hello Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="61f82-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="61f82-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="61f82-234">Renvoie ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="61f82-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="61f82-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="61f82-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="61f82-236">`-Name`: nom hello d’une application web dans IIS.</span><span class="sxs-lookup"><span data-stu-id="61f82-236">`-Name`: hello name of a web app in IIS.</span></span>
* <span data-ttu-id="61f82-237">`-InstrumentationKey` (Facultatif.) Utilisez que cette toochange hello ressource toowhich hello de télémétrie application est envoyé.</span><span class="sxs-lookup"><span data-stu-id="61f82-237">`-InstrumentationKey` (Optional.) Use this toochange hello resource toowhich hello app's telemetry is sent.</span></span>
* <span data-ttu-id="61f82-238">Cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="61f82-238">This cmdlet:</span></span>
  * <span data-ttu-id="61f82-239">Hello mises à niveau nommé toohello version de l’application Hello SDK toothis machine téléchargée le plus récemment.</span><span class="sxs-lookup"><span data-stu-id="61f82-239">Upgrades hello named app toohello version of hello SDK most recently downloaded toothis machine.</span></span> <span data-ttu-id="61f82-240">(Ne fonctionne que si `SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="61f82-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="61f82-241">Si vous fournissez une clé d’instrumentation, hello nommé app est reconfiguré toosend télémétrie toohello ressource avec cette clé.</span><span class="sxs-lookup"><span data-stu-id="61f82-241">If you provide an instrumentation key, hello named app is reconfigured toosend telemetry toohello resource with that key.</span></span> <span data-ttu-id="61f82-242">(Fonctionne si `SdkState != Disabled`)</span><span class="sxs-lookup"><span data-stu-id="61f82-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="61f82-243">Télécharge hello dernière Application Insights toohello serveur SDK.</span><span class="sxs-lookup"><span data-stu-id="61f82-243">Downloads hello latest Application Insights SDK toohello server.</span></span>

## <span data-ttu-id="61f82-244"><a name="questions"></a>Questions sur Status Monitor</span><span class="sxs-lookup"><span data-stu-id="61f82-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="61f82-245">Qu’est-ce que Status Monitor ?</span><span class="sxs-lookup"><span data-stu-id="61f82-245">What is Status Monitor?</span></span>

<span data-ttu-id="61f82-246">Il s’agit d’une application de bureau que vous installez sur votre serveur web IIS.</span><span class="sxs-lookup"><span data-stu-id="61f82-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="61f82-247">Il vous permet d’instrumenter et de configurer des applications web.</span><span class="sxs-lookup"><span data-stu-id="61f82-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="61f82-248">Quand dois-je utiliser Status Monitor ?</span><span class="sxs-lookup"><span data-stu-id="61f82-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="61f82-249">tooinstrument un web application qui s’exécute sur votre serveur IIS - même si elle est déjà en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="61f82-249">tooinstrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="61f82-250">tooenable de télémétrie supplémentaires pour les applications web qui ont été [intègrent hello Application Insights SDK](app-insights-asp-net.md) au moment de la compilation.</span><span class="sxs-lookup"><span data-stu-id="61f82-250">tooenable additional telemetry for web apps that have been [built with hello Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="61f82-251">Puis-je le fermer il après son exécution ?</span><span class="sxs-lookup"><span data-stu-id="61f82-251">Can I close it after it runs?</span></span>

<span data-ttu-id="61f82-252">Oui.</span><span class="sxs-lookup"><span data-stu-id="61f82-252">Yes.</span></span> <span data-ttu-id="61f82-253">Une fois qu’il a instrumenté hello des sites Web que vous sélectionnez, vous pouvez le fermer.</span><span class="sxs-lookup"><span data-stu-id="61f82-253">After it has instrumented hello websites you select, you can close it.</span></span>

<span data-ttu-id="61f82-254">Il ne collecte pas la télémétrie par lui-même.</span><span class="sxs-lookup"><span data-stu-id="61f82-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="61f82-255">Simplement, il configure les applications web hello et définit certaines autorisations.</span><span class="sxs-lookup"><span data-stu-id="61f82-255">It just configures hello web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="61f82-256">Que fait Status Monitor ?</span><span class="sxs-lookup"><span data-stu-id="61f82-256">What does Status Monitor do?</span></span>

<span data-ttu-id="61f82-257">Lorsque vous sélectionnez une application web pour le moniteur d’état tooinstrument :</span><span class="sxs-lookup"><span data-stu-id="61f82-257">When you select a web app for Status Monitor tooinstrument:</span></span>

* <span data-ttu-id="61f82-258">Télécharge et place des assemblys d’Application Insights hello et le fichier .config dans le dossier des fichiers binaires de l’application hello web.</span><span class="sxs-lookup"><span data-stu-id="61f82-258">Downloads and places hello Application Insights assemblies and .config file in hello web app's binaries folder.</span></span>
* <span data-ttu-id="61f82-259">Modifie `web.config` module de suivi Application Insights HTTP tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="61f82-259">Modifies `web.config` tooadd hello Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="61f82-260">Active les appels de dépendance toocollect de profilage du CLR.</span><span class="sxs-lookup"><span data-stu-id="61f82-260">Enables CLR profiling toocollect dependency calls.</span></span>

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a><span data-ttu-id="61f82-261">Dois-je toorun moniteur d’état chaque fois que l’application hello mise à jour ?</span><span class="sxs-lookup"><span data-stu-id="61f82-261">Do I need toorun Status Monitor whenever I update hello app?</span></span>

<span data-ttu-id="61f82-262">Cela n’est pas nécessaire si vous la redéployez de façon incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="61f82-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="61f82-263">Si vous sélectionnez l’option « Supprimer les fichiers existants » de hello Bonjour processus de publication, vous devez exécuter de toore Status Monitor tooconfigure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="61f82-263">If you select hello 'delete existing files' option in hello publish process, you would need toore-run Status Monitor tooconfigure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="61f82-264">Quel type de télémétrie est collecté ?</span><span class="sxs-lookup"><span data-stu-id="61f82-264">What telemetry is collected?</span></span>

<span data-ttu-id="61f82-265">Pour les applications que vous instrumentez uniquement au moment de l’exécution à l’aide de Status Monitor :</span><span class="sxs-lookup"><span data-stu-id="61f82-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="61f82-266">Des requêtes HTTP</span><span class="sxs-lookup"><span data-stu-id="61f82-266">HTTP requests</span></span>
* <span data-ttu-id="61f82-267">Appels toodependencies</span><span class="sxs-lookup"><span data-stu-id="61f82-267">Calls toodependencies</span></span>
* <span data-ttu-id="61f82-268">Exceptions</span><span class="sxs-lookup"><span data-stu-id="61f82-268">Exceptions</span></span>
* <span data-ttu-id="61f82-269">Compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="61f82-269">Performance counters</span></span>

<span data-ttu-id="61f82-270">Pour les applications déjà instrumentées au moment de la compilation :</span><span class="sxs-lookup"><span data-stu-id="61f82-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="61f82-271">Des compteurs de processus.</span><span class="sxs-lookup"><span data-stu-id="61f82-271">Process counters.</span></span>
 * <span data-ttu-id="61f82-272">Des appels de dépendances (.NET 4.5) ; des valeurs de retour dans des appels de dépendances (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="61f82-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="61f82-273">Des valeurs d’arborescence des appels de procédure d’exception.</span><span class="sxs-lookup"><span data-stu-id="61f82-273">Exception stack trace values.</span></span>

[<span data-ttu-id="61f82-274">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="61f82-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="61f82-275">Vidéo</span><span class="sxs-lookup"><span data-stu-id="61f82-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="61f82-276"><a name="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61f82-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="61f82-277">Affichez vos données de télémétrie :</span><span class="sxs-lookup"><span data-stu-id="61f82-277">View your telemetry:</span></span>

* <span data-ttu-id="61f82-278">[Explorer les métriques](app-insights-metrics-explorer.md) toomonitor performances et utilisation</span><span class="sxs-lookup"><span data-stu-id="61f82-278">[Explore metrics](app-insights-metrics-explorer.md) toomonitor performance and usage</span></span>
* <span data-ttu-id="61f82-279">[Rechercher des événements et journaux] [ diagnostic] toodiagnose problèmes</span><span class="sxs-lookup"><span data-stu-id="61f82-279">[Search events and logs][diagnostic] toodiagnose problems</span></span>
* <span data-ttu-id="61f82-280">[Utilisez la fonctionnalité Analytics](app-insights-analytics.md) pour des requêtes plus élaborées</span><span class="sxs-lookup"><span data-stu-id="61f82-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="61f82-281">Créez des tableaux de bord</span><span class="sxs-lookup"><span data-stu-id="61f82-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="61f82-282">Ajoutez des données de télémétrie :</span><span class="sxs-lookup"><span data-stu-id="61f82-282">Add more telemetry:</span></span>

* <span data-ttu-id="61f82-283">[Créer des tests web] [ availability] toomake que votre site reste active.</span><span class="sxs-lookup"><span data-stu-id="61f82-283">[Create web tests][availability] toomake sure your site stays live.</span></span>
* <span data-ttu-id="61f82-284">[Ajouter des données de télémétrie de client web] [ usage] toosee des exceptions à partir de code de page web et toolet vous insérez trace des appels.</span><span class="sxs-lookup"><span data-stu-id="61f82-284">[Add web client telemetry][usage] toosee exceptions from web page code and toolet you insert trace calls.</span></span>
* <span data-ttu-id="61f82-285">[Ajouter le code d’Application Insights SDK tooyour] [ greenbrown] afin que vous pouvez insérer la trace et enregistrer les appels</span><span class="sxs-lookup"><span data-stu-id="61f82-285">[Add Application Insights SDK tooyour code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
