---
title: Surveiller une application web | Microsoft Docs
description: "Découvrez comment configurer la surveillance de votre application web"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="4fe75-103">Surveiller App Service</span><span class="sxs-lookup"><span data-stu-id="4fe75-103">Monitor App Service</span></span>
<span data-ttu-id="4fe75-104">Ce didacticiel vous explique comment surveiller votre application et utiliser les outils de plateforme intégrés pour résoudre les problèmes lorsqu’ils surviennent.</span><span class="sxs-lookup"><span data-stu-id="4fe75-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="4fe75-105">Chaque section de ce document traite d’une fonctionnalité spécifique.</span><span class="sxs-lookup"><span data-stu-id="4fe75-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="4fe75-106">En utilisant conjointement les fonctionnalités, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="4fe75-106">Using the features together let you:</span></span>
- <span data-ttu-id="4fe75-107">Identifier un problème dans votre application.</span><span class="sxs-lookup"><span data-stu-id="4fe75-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="4fe75-108">Déterminer si le problème vient de votre code ou de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="4fe75-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="4fe75-109">Réduire la source du problème dans votre code.</span><span class="sxs-lookup"><span data-stu-id="4fe75-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="4fe75-110">Déboguer et résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="4fe75-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4fe75-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4fe75-111">Before you begin</span></span>
- <span data-ttu-id="4fe75-112">Vous avez besoin d’une application web à surveiller pour suivre les étapes indiquées.</span><span class="sxs-lookup"><span data-stu-id="4fe75-112">You need a Web App to monitor and follow the outlined steps.</span></span>
    - <span data-ttu-id="4fe75-113">Vous pouvez créer une application en suivant les étapes décrites dans le didacticiel [Créer une application ASP.NET dans Azure avec SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md).</span><span class="sxs-lookup"><span data-stu-id="4fe75-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="4fe75-114">Si vous souhaitez essayer de **déboguer votre application à distance**, vous devez disposer de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4fe75-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="4fe75-115">Si vous n’avez pas encore installé Visual Studio 2017, vous pouvez télécharger et utiliser la version gratuite [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4fe75-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="4fe75-116">Veillez à activer **le développement Azure** lors de l’installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4fe75-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <span data-ttu-id="4fe75-117"><a name="metrics"></a> Étape 1 : Afficher les mesures</span><span class="sxs-lookup"><span data-stu-id="4fe75-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="4fe75-118">Les **mesures** sont utiles pour comprendre les concepts suivants :</span><span class="sxs-lookup"><span data-stu-id="4fe75-118">**Metrics** are useful to understand:</span></span>
- <span data-ttu-id="4fe75-119">Intégrité d’application</span><span class="sxs-lookup"><span data-stu-id="4fe75-119">Application health</span></span>
- <span data-ttu-id="4fe75-120">Performances de l’application</span><span class="sxs-lookup"><span data-stu-id="4fe75-120">App performance</span></span>
- <span data-ttu-id="4fe75-121">Consommation des ressources</span><span class="sxs-lookup"><span data-stu-id="4fe75-121">Resource consumption</span></span>

<span data-ttu-id="4fe75-122">Lorsque vous examinez un problème d’application, il peut être judicieux de commencer par consulter les mesures.</span><span class="sxs-lookup"><span data-stu-id="4fe75-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="4fe75-123">Le portail Azure constitue un moyen rapide d’inspecter visuellement les mesures de votre application à l’aide d’**Azure Monitor**.</span><span class="sxs-lookup"><span data-stu-id="4fe75-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="4fe75-124">Les mesures offrent un historique de différentes agrégations clés pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4fe75-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="4fe75-125">Pour toutes les applications hébergées dans App Service, vous devez surveiller à la fois l’application web et le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="4fe75-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="4fe75-126">Un plan App Service représente la collection des ressources physiques utilisées pour héberger vos applications.</span><span class="sxs-lookup"><span data-stu-id="4fe75-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="4fe75-127">Toutes les applications affectées à un plan App Service partagent les ressources qu’il définit, ce qui vous permet de réduire les coûts lors de l’hébergement de plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="4fe75-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="4fe75-128">Les plans App Service définissent :</span><span class="sxs-lookup"><span data-stu-id="4fe75-128">App Service plans define:</span></span>
> * <span data-ttu-id="4fe75-129">Région : Europe du Nord, États-Unis de l’Est, Sud-Est asiatique, etc.</span><span class="sxs-lookup"><span data-stu-id="4fe75-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="4fe75-130">Taille d’instance : Petit, Moyen, Grand, etc.</span><span class="sxs-lookup"><span data-stu-id="4fe75-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="4fe75-131">Comptage : une, deux ou trois instances, etc.</span><span class="sxs-lookup"><span data-stu-id="4fe75-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="4fe75-132">Référence (SKU) : Gratuit, Partagé, De base, Standard, Premium, etc.</span><span class="sxs-lookup"><span data-stu-id="4fe75-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="4fe75-133">Pour consulter les mesures de votre application web, accédez au panneau **Vue d’ensemble** de l’application que vous souhaitez surveiller.</span><span class="sxs-lookup"><span data-stu-id="4fe75-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="4fe75-134">Un graphique des mesures de votre application est disponible sous forme de **vignette de surveillance**.</span><span class="sxs-lookup"><span data-stu-id="4fe75-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="4fe75-135">Cliquez sur la vignette pour modifier et configurer les mesures et la plage horaire à afficher.</span><span class="sxs-lookup"><span data-stu-id="4fe75-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span>

<span data-ttu-id="4fe75-136">Par défaut, le panneau de ressources présente un affichage pour les demandes d’application et les erreurs survenues au cours de la dernière heure.</span><span class="sxs-lookup"><span data-stu-id="4fe75-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="4fe75-137">![Application Monitor](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="4fe75-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="4fe75-138">Comme vous pouvez le voir dans l’exemple, notre application génère plusieurs **erreurs de serveur HTTP**.</span><span class="sxs-lookup"><span data-stu-id="4fe75-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="4fe75-139">Le grand nombre d’erreurs est le premier signe que nous devons examiner cette application.</span><span class="sxs-lookup"><span data-stu-id="4fe75-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="4fe75-140">Utilisez les liens suivants pour en savoir plus sur Azure Monitor :</span><span class="sxs-lookup"><span data-stu-id="4fe75-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="4fe75-141">Prise en main d’Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4fe75-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="4fe75-142">Mesures Azure</span><span class="sxs-lookup"><span data-stu-id="4fe75-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="4fe75-143">Mesures prises en charge avec Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4fe75-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="4fe75-144">Tableaux de bord Azure</span><span class="sxs-lookup"><span data-stu-id="4fe75-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="4fe75-145"><a name="alerts"></a> Étape 2 : Configurer des alertes</span><span class="sxs-lookup"><span data-stu-id="4fe75-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="4fe75-146">Les **alertes** peuvent être configurées de manière à se déclencher sur des conditions spécifiques pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4fe75-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="4fe75-147">À l’[Étape 1 : Afficher les mesures](#metrics), nous avons vu que l’application comportait un grand nombre d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="4fe75-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span>

<span data-ttu-id="4fe75-148">Nous allons configurer une alerte pour recevoir une notification automatique lorsqu’une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="4fe75-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="4fe75-149">Dans le cas présent, nous voulons que l’alerte envoie un message électronique chaque fois que le nombre d’erreurs HTTP 50X dépasse un certain seuil.</span><span class="sxs-lookup"><span data-stu-id="4fe75-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="4fe75-150">Pour créer une alerte, accédez à **Surveillance** > **Alertes** et cliquez sur **[+] Ajouter une alerte**.</span><span class="sxs-lookup"><span data-stu-id="4fe75-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alertes](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="4fe75-152">Indiquez des valeurs pour configurer l’alerte :</span><span class="sxs-lookup"><span data-stu-id="4fe75-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="4fe75-153">**Ressource :** site à surveiller avec l’alerte.</span><span class="sxs-lookup"><span data-stu-id="4fe75-153">**Resource:** The site to monitor with the alert.</span></span>
- <span data-ttu-id="4fe75-154">**Nom :** nom de votre alerte, ici : *Grand nombre d’erreurs HTTP 50X*.</span><span class="sxs-lookup"><span data-stu-id="4fe75-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="4fe75-155">**Description :** explication textuelle de ce que l’alerte doit surveiller.</span><span class="sxs-lookup"><span data-stu-id="4fe75-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="4fe75-156">**Alerte sur :** les alertes peuvent surveiller les mesures ou les événements, ici nous observons les mesures.</span><span class="sxs-lookup"><span data-stu-id="4fe75-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="4fe75-157">**Mesure :** mesure à surveiller, ici : *Erreurs de serveur HTTP*.</span><span class="sxs-lookup"><span data-stu-id="4fe75-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="4fe75-158">**Condition :** moment de l’alerte, ici nous allons sélectionner l’option *supérieur à*.</span><span class="sxs-lookup"><span data-stu-id="4fe75-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="4fe75-159">**Seuil :** valeur à surveiller, ici : *400*.</span><span class="sxs-lookup"><span data-stu-id="4fe75-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="4fe75-160">**Période :** les alertes agissent au-delà de la valeur moyenne d’une mesure.</span><span class="sxs-lookup"><span data-stu-id="4fe75-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="4fe75-161">Les périodes plus courtes génèrent des alertes plus sensibles.</span><span class="sxs-lookup"><span data-stu-id="4fe75-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="4fe75-162">Dans notre exemple, nous choisissons *5 minutes*.</span><span class="sxs-lookup"><span data-stu-id="4fe75-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="4fe75-163">**Envoyer un courrier électronique aux propriétaires et aux contributeurs :** ici : *Activé*.</span><span class="sxs-lookup"><span data-stu-id="4fe75-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="4fe75-164">Maintenant que l’alerte est créée, un courrier électronique est envoyé chaque fois que l’application dépasse le seuil configuré.</span><span class="sxs-lookup"><span data-stu-id="4fe75-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="4fe75-165">Les alertes actives peuvent également être consultées dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe75-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![Alertes déclenchées](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="4fe75-167">Utilisez les liens suivants pour en savoir plus sur les alertes Azure :</span><span class="sxs-lookup"><span data-stu-id="4fe75-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="4fe75-168">Que sont les alertes dans Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4fe75-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="4fe75-169">Effectuer une opération sur les mesures</span><span class="sxs-lookup"><span data-stu-id="4fe75-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="4fe75-170">Créer des alertes de mesures</span><span class="sxs-lookup"><span data-stu-id="4fe75-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="4fe75-171"><a name="companion"></a> Étape 3 : Compagnon App Service</span><span class="sxs-lookup"><span data-stu-id="4fe75-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="4fe75-172">Le **compagnon App Service** s’avère pratique pour surveiller votre application avec une expérience native sur votre appareil mobile (iOS ou Android).</span><span class="sxs-lookup"><span data-stu-id="4fe75-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="4fe75-173">Utilisez le compagnon App Service pour :</span><span class="sxs-lookup"><span data-stu-id="4fe75-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="4fe75-174">consulter les mesures d’application,</span><span class="sxs-lookup"><span data-stu-id="4fe75-174">Review application metrics</span></span>
- <span data-ttu-id="4fe75-175">consulter et agir sur les alertes d’application et les recommandations,</span><span class="sxs-lookup"><span data-stu-id="4fe75-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="4fe75-176">procéder à un dépannage basique (parcourir, démarrer, arrêter ou redémarrer l’application).</span><span class="sxs-lookup"><span data-stu-id="4fe75-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="4fe75-177">Obtenez des notifications push pour les événements critiques.</span><span class="sxs-lookup"><span data-stu-id="4fe75-177">Get push notifications for critical events.</span></span>

![Compagnon App Service](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="4fe75-179">[![Compagnon App Service - App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Compagnon App Service - Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="4fe75-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="4fe75-180">Vous pouvez installer le compagnon App Service à partir de l’[App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) ou de [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps).</span><span class="sxs-lookup"><span data-stu-id="4fe75-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="4fe75-181"><a name="diagnose"></a> Étape 4 : Diagnostiquer et résoudre les problèmes</span><span class="sxs-lookup"><span data-stu-id="4fe75-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="4fe75-182">**Diagnostiquer et résoudre les problèmes** permet de distinguer les problèmes d’application des problèmes de plateforme.</span><span class="sxs-lookup"><span data-stu-id="4fe75-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="4fe75-183">Cela permet également d’obtenir des options d’atténuation possibles pour rétablir l’état d’intégrité de votre application web.</span><span class="sxs-lookup"><span data-stu-id="4fe75-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>

![Diagnostiquer et résoudre les problèmes](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="4fe75-185">Toujours avec l’exemple des étapes précédentes, nous constatons que l’application rencontre des problèmes de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="4fe75-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="4fe75-186">En revanche, la disponibilité de la plateforme est restée à 100 %.</span><span class="sxs-lookup"><span data-stu-id="4fe75-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="4fe75-187">Lorsque l’application rencontre un problème et que la plateforme reste saine, cela indique clairement que le problème est lié à l’application.</span><span class="sxs-lookup"><span data-stu-id="4fe75-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="4fe75-188"><a name="logging"></a> Étape 5 - Journalisation</span><span class="sxs-lookup"><span data-stu-id="4fe75-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="4fe75-189">Maintenant que nous savons que les erreurs sont dues à un problème d’application, nous pouvons examiner les journaux d’application et de serveur pour obtenir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4fe75-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="4fe75-190">La journalisation vous permet de collecter à la fois les journaux de **diagnostic d’application** et de **diagnostic de serveur web** concernant votre application web.</span><span class="sxs-lookup"><span data-stu-id="4fe75-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="4fe75-191">Diagnostics d’application</span><span class="sxs-lookup"><span data-stu-id="4fe75-191">Application Diagnostics</span></span>
<span data-ttu-id="4fe75-192">Le diagnostic d’application vous permet de capturer des suivis générés par l’application pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="4fe75-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span>

<span data-ttu-id="4fe75-193">L’ajout d’un traçage à votre application améliore considérablement votre capacité à déboguer et à déceler les problèmes.</span><span class="sxs-lookup"><span data-stu-id="4fe75-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="4fe75-194">Dans ASP.NET, vous pouvez enregistrer les suivis d’application à l’aide de la [classe System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), afin de générer des événements qui sont capturés par l’infrastructure de journalisation.</span><span class="sxs-lookup"><span data-stu-id="4fe75-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="4fe75-195">Vous pouvez également indiquer le niveau de gravité du suivi pour un filtrage plus facile.</span><span class="sxs-lookup"><span data-stu-id="4fe75-195">You can also specify the severity of the trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="4fe75-196">Pour activer la journalisation des applications, accédez à **Surveillance** > **Journaux de diagnostic** et utilisez les touches bascules.</span><span class="sxs-lookup"><span data-stu-id="4fe75-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![Surveiller l’application](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="4fe75-198">Les journaux d’application peuvent être stockés dans le système de fichiers de votre application web ou envoyés vers le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="4fe75-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="4fe75-199">Pour les scénarios de production, il est recommandé d’utiliser le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="4fe75-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4fe75-200">L’activation de la journalisation a une incidence sur les performances de votre application et sur l’utilisation des ressources.</span><span class="sxs-lookup"><span data-stu-id="4fe75-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="4fe75-201">Pour les scénarios de production, les journaux d’erreurs sont recommandés.</span><span class="sxs-lookup"><span data-stu-id="4fe75-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="4fe75-202">Activez une journalisation plus détaillée uniquement en cas de problème.</span><span class="sxs-lookup"><span data-stu-id="4fe75-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="4fe75-203">Diagnostics de serveur web</span><span class="sxs-lookup"><span data-stu-id="4fe75-203">Web Server Diagnostics</span></span>
<span data-ttu-id="4fe75-204">Les journaux des serveurs web sont générés même si votre application n’est pas instrumentée.</span><span class="sxs-lookup"><span data-stu-id="4fe75-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="4fe75-205">App Service peut collecter trois types de journaux de serveur :</span><span class="sxs-lookup"><span data-stu-id="4fe75-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="4fe75-206">**Journalisation du serveur web**</span><span class="sxs-lookup"><span data-stu-id="4fe75-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="4fe75-207">Informations sur les transactions HTTP à l’aide du [format de fichier journal étendu W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="4fe75-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="4fe75-208">Ce rapport se révèle utile pour déterminer les métriques globales d’un site, comme le nombre de demandes traitées ou le nombre de demandes émanant d’une adresse IP spécifique.</span><span class="sxs-lookup"><span data-stu-id="4fe75-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="4fe75-209">**Messages d’erreurs détaillés**</span><span class="sxs-lookup"><span data-stu-id="4fe75-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="4fe75-210">Informations d’erreur détaillées pour les codes d’état HTTP qui indiquent un échec (code d’état 400 ou supérieur).</span><span class="sxs-lookup"><span data-stu-id="4fe75-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="4fe75-211">En savoir plus sur la journalisation d’erreurs détaillée</span><span class="sxs-lookup"><span data-stu-id="4fe75-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="4fe75-212">**Suivi des demandes ayant échoué**</span><span class="sxs-lookup"><span data-stu-id="4fe75-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="4fe75-213">Informations détaillées sur les demandes qui ont échoué, y compris une trace des composants IIS utilisés pour traiter la demande et la durée dans chaque composant.</span><span class="sxs-lookup"><span data-stu-id="4fe75-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span>
    - <span data-ttu-id="4fe75-214">Les journaux des demandes ayant échoué sont utiles lorsque vous essayez d’isoler ce qui provoque une erreur HTTP spécifique.</span><span class="sxs-lookup"><span data-stu-id="4fe75-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="4fe75-215">En savoir plus sur le suivi des demandes ayant échoué</span><span class="sxs-lookup"><span data-stu-id="4fe75-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="4fe75-216">Pour activer la journalisation de serveur :</span><span class="sxs-lookup"><span data-stu-id="4fe75-216">To enable Server logging:</span></span>
- <span data-ttu-id="4fe75-217">Accédez à **Surveillance** > **Journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="4fe75-217">go to **Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="4fe75-218">Activez les différents types de diagnostics de serveur web à l’aide des bascules.</span><span class="sxs-lookup"><span data-stu-id="4fe75-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![Surveiller l’application](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="4fe75-220">L’activation de la journalisation a une incidence sur les performances de votre application et sur l’utilisation des ressources.</span><span class="sxs-lookup"><span data-stu-id="4fe75-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="4fe75-221">Pour les scénarios de production, les journaux d’erreurs sont recommandés. Activez une journalisation plus détaillée uniquement en cas de problème.</span><span class="sxs-lookup"><span data-stu-id="4fe75-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="4fe75-222">Accès aux journaux</span><span class="sxs-lookup"><span data-stu-id="4fe75-222">Accessing Logs</span></span>
<span data-ttu-id="4fe75-223">Les journaux enregistrés dans le stockage d’objets blob sont accessibles à l’aide de l’Explorateur de stockage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe75-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="4fe75-224">Les journaux stockés dans le système de fichiers de l’application web sont accessibles via FTP aux chemins suivants :</span><span class="sxs-lookup"><span data-stu-id="4fe75-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="4fe75-225">**Journaux d’application** - `%HOME%/LogFiles/Application/`</span><span class="sxs-lookup"><span data-stu-id="4fe75-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="4fe75-226">Ce dossier contient un ou plusieurs fichiers texte contenant des informations générées dans le cadre de la journalisation des applications.</span><span class="sxs-lookup"><span data-stu-id="4fe75-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="4fe75-227">**Suivi des demandes ayant échoué** - `%HOME%/LogFiles/W3SVC#########/`</span><span class="sxs-lookup"><span data-stu-id="4fe75-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="4fe75-228">Ce dossier contient un fichier XSL et un ou plusieurs fichiers XML.</span><span class="sxs-lookup"><span data-stu-id="4fe75-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="4fe75-229">**Journaux d’erreurs détaillés** - `%HOME%/LogFiles/DetailedErrors/`</span><span class="sxs-lookup"><span data-stu-id="4fe75-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="4fe75-230">Ce dossier contient un ou plusieurs fichiers .htm incluant des informations détaillées sur les erreurs HTTP générées par votre application.</span><span class="sxs-lookup"><span data-stu-id="4fe75-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="4fe75-231">**Journaux des serveurs web** - `%HOME%/LogFiles/http/RawLogs`</span><span class="sxs-lookup"><span data-stu-id="4fe75-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="4fe75-232">Ce dossier contient un ou plusieurs fichiers texte au format de fichier journal étendu W3C.</span><span class="sxs-lookup"><span data-stu-id="4fe75-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <span data-ttu-id="4fe75-233"><a name="streaming"></a> Étape 6 - Diffusion de journaux</span><span class="sxs-lookup"><span data-stu-id="4fe75-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="4fe75-234">Lorsque vous déboguez une application, la diffusion des journaux est pratique car elle s’avère plus rapide que l’[accès aux journaux](#Accessing-Logs) via FTP.</span><span class="sxs-lookup"><span data-stu-id="4fe75-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="4fe75-235">App Service peut diffuser les **journaux d’application** et les **journaux de serveur web** lorsqu’ils sont générés.</span><span class="sxs-lookup"><span data-stu-id="4fe75-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="4fe75-236">Avant d’essayer de diffuser les journaux, assurez-vous que vous avez activé la collecte des journaux comme décrit dans la section [Journalisation](#logging).</span><span class="sxs-lookup"><span data-stu-id="4fe75-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="4fe75-237">Pour diffuser les journaux, accédez à **Surveillance**> **Flux de journaux**.</span><span class="sxs-lookup"><span data-stu-id="4fe75-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="4fe75-238">Sélectionnez **Journaux d’application** ou **Journaux des serveurs web** en fonction des informations que vous recherchez.</span><span class="sxs-lookup"><span data-stu-id="4fe75-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="4fe75-239">Ici, vous pouvez également interrompre, redémarrer et effacer la mémoire tampon.</span><span class="sxs-lookup"><span data-stu-id="4fe75-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![Journaux en continu](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="4fe75-241">Les journaux sont générés uniquement lorsqu’il existe du trafic sur l’application. Vous pouvez également augmenter le niveau de détail des journaux pour obtenir plus d’événements ou d’informations.</span><span class="sxs-lookup"><span data-stu-id="4fe75-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <span data-ttu-id="4fe75-242"><a name="remote"></a> Étape 7 - Débogage à distance</span><span class="sxs-lookup"><span data-stu-id="4fe75-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="4fe75-243">Une fois la source des problèmes d’application identifiée, utilisez le **débogage à distance** pour examiner le code.</span><span class="sxs-lookup"><span data-stu-id="4fe75-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="4fe75-244">Le débogage à distance vous permet d’attacher un débogueur à votre application web s’exécutant dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="4fe75-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="4fe75-245">Vous pouvez définir des points d’arrêt, manipuler directement la mémoire, parcourir le code en détail et même modifier le chemin d’accès du code, comme vous le feriez si l’application s’exécutait en local.</span><span class="sxs-lookup"><span data-stu-id="4fe75-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="4fe75-246">Pour attacher le débogueur à votre application s’exécutant dans le cloud :</span><span class="sxs-lookup"><span data-stu-id="4fe75-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="4fe75-247">Avec Visual Studio 2017, ouvrez la solution correspondant à l’application à déboguer.</span><span class="sxs-lookup"><span data-stu-id="4fe75-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span>
- <span data-ttu-id="4fe75-248">Définissez des points d’arrêt comme vous le feriez pour un développement en local.</span><span class="sxs-lookup"><span data-stu-id="4fe75-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="4fe75-249">Ouvrez **l’explorateur de cloud** (ctr + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="4fe75-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="4fe75-250">Connectez-vous avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe75-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="4fe75-251">Recherchez l’application à déboguer.</span><span class="sxs-lookup"><span data-stu-id="4fe75-251">Find the app you want to debug</span></span>
- <span data-ttu-id="4fe75-252">Sélectionnez le formulaire **Attacher le débogueur** dans le volet **Actions**.</span><span class="sxs-lookup"><span data-stu-id="4fe75-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![Débogage à distance](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="4fe75-254">Visual Studio configure votre application pour le débogage à distance et ouvre une fenêtre de navigateur qui accède à votre application.</span><span class="sxs-lookup"><span data-stu-id="4fe75-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="4fe75-255">Parcourez votre application pour déclencher des points d’arrêt et parcourir le code.</span><span class="sxs-lookup"><span data-stu-id="4fe75-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="4fe75-256">Nous vous déconseillons d'exécuter le mode débogage en production.</span><span class="sxs-lookup"><span data-stu-id="4fe75-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="4fe75-257">Si votre application de production n’est pas montée en charge sur plusieurs instances de serveur, la fonction de débogage empêche le serveur web de répondre aux autres demandes.</span><span class="sxs-lookup"><span data-stu-id="4fe75-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="4fe75-258">Pour résoudre les problèmes de production, la meilleure solution est de [configurer la journalisation](#logging) et [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="4fe75-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="4fe75-259"><a name="explorer"></a> Étape 8 : Process Explorer</span><span class="sxs-lookup"><span data-stu-id="4fe75-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="4fe75-260">Lorsque votre application comporte plusieurs instances, **Process Explorer** peut vous aider à identifier les problèmes propres à une instance.</span><span class="sxs-lookup"><span data-stu-id="4fe75-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="4fe75-261">Utilisez **Process Explorer** pour :</span><span class="sxs-lookup"><span data-stu-id="4fe75-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="4fe75-262">énumérer tous les processus entre différentes instances de votre plan App Service ;</span><span class="sxs-lookup"><span data-stu-id="4fe75-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="4fe75-263">extraire et afficher les descripteurs et modules associés à chaque processus ;</span><span class="sxs-lookup"><span data-stu-id="4fe75-263">Drill down and view the handles and modules associated with each process.</span></span>
- <span data-ttu-id="4fe75-264">afficher le nombre de processeurs, de plages de travail et de threads pour vous aider à identifier les boucles infinies ;</span><span class="sxs-lookup"><span data-stu-id="4fe75-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="4fe75-265">rechercher des descripteurs de fichiers ouverts, voire arrêter une instance de processus spécifique.</span><span class="sxs-lookup"><span data-stu-id="4fe75-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="4fe75-266">Process Explorer se trouve sous **Surveillance** > **Process Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4fe75-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Process Explorer](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="4fe75-268"><a name="insights"></a> Étape 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="4fe75-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="4fe75-269">**Application Insights** fournit des fonctionnalités avancées de profilage et de surveillance de votre application.</span><span class="sxs-lookup"><span data-stu-id="4fe75-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="4fe75-270">Utilisez Application Insights pour détecter et diagnostiquer les exceptions et les problèmes de performances dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="4fe75-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="4fe75-271">Vous pouvez activer Application Insights pour votre application web sous **Surveillance** > **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="4fe75-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="4fe75-272">Il se peut qu’Application Insights vous demande d’installer l’extension de site Application Insights avant de commencer à collecter des données.</span><span class="sxs-lookup"><span data-stu-id="4fe75-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="4fe75-273">L’installation de l’extension de site provoque un redémarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="4fe75-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="4fe75-275">Application Insights offre de nombreuses fonctionnalités. Pour en savoir plus, consultez les liens de la section [Étapes suivantes](#next).</span><span class="sxs-lookup"><span data-stu-id="4fe75-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <span data-ttu-id="4fe75-276"><a name="next"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4fe75-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="4fe75-277">Présentation d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="4fe75-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="4fe75-278">Surveiller les performances de l’application web Azure avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="4fe75-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="4fe75-279">Analyse de la disponibilité et de la réactivité d’un site web avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="4fe75-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
