---
title: "une application Web d’aaaMonitor | Documents Microsoft"
description: "Découvrez comment tooset d’analyse sur votre application Web"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="4e3d2-103">Surveiller App Service</span><span class="sxs-lookup"><span data-stu-id="4e3d2-103">Monitor App Service</span></span>
<span data-ttu-id="4e3d2-104">Ce didacticiel vous guide et à surveiller votre application à l’aide de hello plateforme intégrées outils toosolve des problèmes lorsqu’ils se produisent.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-104">This tutorial walks you through monitoring your app and using hello built-in platform tools toosolve problems when they occur.</span></span>

<span data-ttu-id="4e3d2-105">Chaque section de ce document traite d’une fonctionnalité spécifique.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="4e3d2-106">L’utilisation conjointe de fonctionnalités de hello vous permettre de :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-106">Using hello features together let you:</span></span>
- <span data-ttu-id="4e3d2-107">Identifier un problème dans votre application.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="4e3d2-108">Détermination de lorsque le problème de hello est provoquée par la plateforme de votre code ou hello.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-108">Determining when hello issue is caused by your code or hello platform.</span></span>
- <span data-ttu-id="4e3d2-109">Limiter les source hello problème de hello dans votre code.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-109">Narrow down hello source of hello problem in your code.</span></span>
- <span data-ttu-id="4e3d2-110">Déboguer et résoudre les problème de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-110">Debugging and fixing hello issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4e3d2-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4e3d2-111">Before you begin</span></span>
- <span data-ttu-id="4e3d2-112">Vous avez besoin d’un toomonitor d’application Web et que vous suivez hello décrites comme suit.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-112">You need a Web App toomonitor and follow hello outlined steps.</span></span>
    - <span data-ttu-id="4e3d2-113">Vous pouvez créer une application hello comme suit décrit dans hello [créer une application ASP.NET dans Azure avec la base de données SQL](app-service-web-tutorial-dotnet-sqldatabase.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-113">You can create an application following hello steps described in hello [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="4e3d2-114">Si vous souhaitez tootry out **débogage distant** de votre application, vous avez besoin de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-114">If you want tootry out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="4e3d2-115">Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello libre [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-115">If you don’t already have Visual Studio 2017 installed, you can download and use hello free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="4e3d2-116">Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-116">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

## <span data-ttu-id="4e3d2-117"><a name="metrics"></a> Étape 1 : Afficher les mesures</span><span class="sxs-lookup"><span data-stu-id="4e3d2-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="4e3d2-118">**Mesures** sont toounderstand utile :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-118">**Metrics** are useful toounderstand:</span></span>
- <span data-ttu-id="4e3d2-119">Intégrité d’application</span><span class="sxs-lookup"><span data-stu-id="4e3d2-119">Application health</span></span>
- <span data-ttu-id="4e3d2-120">Performances de l’application</span><span class="sxs-lookup"><span data-stu-id="4e3d2-120">App performance</span></span>
- <span data-ttu-id="4e3d2-121">Consommation des ressources</span><span class="sxs-lookup"><span data-stu-id="4e3d2-121">Resource consumption</span></span>

<span data-ttu-id="4e3d2-122">Lorsque vous recherchez un problème d’application, examen des métriques est un bon point toostart.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-122">When investigating an application issue, reviewing metrics is a good place toostart.</span></span> <span data-ttu-id="4e3d2-123">Portail Azure a un moyen rapide de toovisually inspecter les métriques de votre application à l’aide de hello **Azure analyse**.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-123">Azure portal has a quick way toovisually inspect hello metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="4e3d2-124">Les mesures offrent un historique de différentes agrégations clés pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="4e3d2-125">Pour n’importe quelle application hébergée dans le service d’applications, vous devez surveiller hello Web App et hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-125">For any app hosted in app service, you should monitor both hello Web App and hello App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="4e3d2-126">Un plan App Service représente collection hello de ressources physiques utilisées toohost vos applications.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-126">An App Service plan represents hello collection of physical resources used toohost your apps.</span></span> <span data-ttu-id="4e3d2-127">Toutes les applications tooan du Service d’applications plan partage hello les ressources affectées qu’elle vous permettant de coût de toosave lorsque plusieurs applications d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-127">All applications assigned tooan App Service plan share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="4e3d2-128">Les plans App Service définissent :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-128">App Service plans define:</span></span>
> * <span data-ttu-id="4e3d2-129">Région : Europe du Nord, États-Unis de l’Est, Sud-Est asiatique, etc.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="4e3d2-130">Taille d’instance : Petit, Moyen, Grand, etc.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="4e3d2-131">Comptage : une, deux ou trois instances, etc.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="4e3d2-132">Référence (SKU) : Gratuit, Partagé, De base, Standard, Premium, etc.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="4e3d2-133">métriques de tooreview pour votre application Web, accédez toohello **vue d’ensemble** Panneau de l’application hello souhaité toomonitor.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-133">tooreview metrics for your Web App, go toohello **Overview** blade of hello app you want toomonitor.</span></span> <span data-ttu-id="4e3d2-134">Un graphique des mesures de votre application est disponible sous forme de **vignette de surveillance**.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="4e3d2-135">Cliquez sur hello vignette tooedit et configurer le métriques tooview et hello toodisplay de plage de temps.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-135">Click hello tile tooedit and configure what metrics tooview and hello time range toodisplay.</span></span>

<span data-ttu-id="4e3d2-136">Par le panneau des ressources par défaut hello fournit une vue pour hello les demandes d’Application et les erreurs pour hello dernière heure.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-136">By default hello resource blade provides a view for hello Application Requests and errors for hello last hour.</span></span>
<span data-ttu-id="4e3d2-137">![Application Monitor](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="4e3d2-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="4e3d2-138">Comme vous pouvez le voir dans l’exemple de hello, nous disposons d’une application qui génère plusieurs **erreurs du serveur HTTP**.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-138">As you can see in hello example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="4e3d2-139">volume élevé de Hello d’erreurs est hello première indication nous devons tooinvestigate cette application.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-139">hello high volume of errors is hello first indication we need tooinvestigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="4e3d2-140">Plus d’informations sur Azure moniteur avec hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-140">Learn more about Azure Monitor with hello following links:</span></span>
> - [<span data-ttu-id="4e3d2-141">Prise en main d’Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4e3d2-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="4e3d2-142">Mesures Azure</span><span class="sxs-lookup"><span data-stu-id="4e3d2-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="4e3d2-143">Mesures prises en charge avec Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4e3d2-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="4e3d2-144">Tableaux de bord Azure</span><span class="sxs-lookup"><span data-stu-id="4e3d2-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="4e3d2-145"><a name="alerts"></a> Étape 2 : Configurer des alertes</span><span class="sxs-lookup"><span data-stu-id="4e3d2-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="4e3d2-146">**Alertes** peut être configuré tootrigger sur des conditions spécifiques de votre application.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-146">**Alerts** can be configured tootrigger on specific conditions for your app.</span></span>

<span data-ttu-id="4e3d2-147">Dans [étape 1 - des métriques de vue](#metrics), nous avons vu qu’application hello avait un grand nombre d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-147">In [Step 1 - View metrics](#metrics), we saw that hello application had a high number of errors.</span></span>

<span data-ttu-id="4e3d2-148">Permet de configurer une alerte tooautomatically soyez averti en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-148">Lets configure an alert tooautomatically get notified when errors occur.</span></span> <span data-ttu-id="4e3d2-149">Dans ce cas, nous souhaitez toosend d’alerte hello et envoyer par courrier électronique chaque fois que quantité, hello pour les erreurs HTTP 50 X dépasse un certain seuil.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-149">In this case, we want hello alert toosend and e-mail every time hello number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="4e3d2-150">toocreate une alerte, accédez trop**analyse** > **alertes** et cliquez sur **[+] ajouter une alerte**.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-150">toocreate an alert, navigate too**Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alertes](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="4e3d2-152">Fournir des valeurs pour la configuration d’alerte hello :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-152">Provide values for hello Alert configuration:</span></span>
- <span data-ttu-id="4e3d2-153">**Ressource :** hello toomonitor de site avec l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-153">**Resource:** hello site toomonitor with hello alert.</span></span>
- <span data-ttu-id="4e3d2-154">**Nom :** nom de votre alerte, ici : *Grand nombre d’erreurs HTTP 50X*.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="4e3d2-155">**Description :** explication textuelle de ce que l’alerte doit surveiller.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="4e3d2-156">**Alerte sur :** les alertes peuvent surveiller les mesures ou les événements, ici nous observons les mesures.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="4e3d2-157">**Métrique :** le métrique toomonitor, dans ce cas : *erreurs du serveur HTTP*.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-157">**Metric:** What metric toomonitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="4e3d2-158">**Condition :** lorsque tooalert, dans ce cas, sélectionnez hello *supérieur* option.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-158">**Condition:** When tooalert, in this case select hello *greater than* option.</span></span>
- <span data-ttu-id="4e3d2-159">**Seuil :** What toolook de valeur, dans ce cas : *400*.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-159">**Threshold:** What is value toolook for, in this case: *400*.</span></span>
- <span data-ttu-id="4e3d2-160">**Période :** alertes s’exécutent sur la valeur moyenne de hello d’une métrique.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-160">**Period:** Alerts operate over hello average value of a metric.</span></span> <span data-ttu-id="4e3d2-161">Les périodes plus courtes génèrent des alertes plus sensibles.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="4e3d2-162">Dans notre exemple, nous choisissons *5 minutes*.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="4e3d2-163">**Envoyer un courrier électronique aux propriétaires et aux contributeurs :** ici : *Activé*.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="4e3d2-164">Maintenant que hello alerte est créée un message électronique est envoyée chaque fois que hello application dépasse le seuil de hello configuré.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-164">Now that hello alert is created an email is sent every time hello app goes over hello configured threshold.</span></span> <span data-ttu-id="4e3d2-165">Alertes actives peuvent être consultées dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-165">Active alerts can also be reviewed in hello Azure portal.</span></span>

![Alertes déclenchées](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="4e3d2-167">Plus d’informations sur les alertes Azure avec hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-167">Learn more about Azure Alerts with hello following links:</span></span>
> - [<span data-ttu-id="4e3d2-168">Que sont les alertes dans Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4e3d2-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="4e3d2-169">Effectuer une opération sur les mesures</span><span class="sxs-lookup"><span data-stu-id="4e3d2-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="4e3d2-170">Créer des alertes de mesures</span><span class="sxs-lookup"><span data-stu-id="4e3d2-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="4e3d2-171"><a name="companion"></a> Étape 3 : Compagnon App Service</span><span class="sxs-lookup"><span data-stu-id="4e3d2-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="4e3d2-172">**Le Guide du Service d’applications** offre un moyen pratique de toomonitor votre application avec une expérience native sur votre appareil mobile (iOS ou Android).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-172">**App Service companion** offers a convenient way toomonitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="4e3d2-173">Utilisez le compagnon App Service pour :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="4e3d2-174">consulter les mesures d’application,</span><span class="sxs-lookup"><span data-stu-id="4e3d2-174">Review application metrics</span></span>
- <span data-ttu-id="4e3d2-175">consulter et agir sur les alertes d’application et les recommandations,</span><span class="sxs-lookup"><span data-stu-id="4e3d2-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="4e3d2-176">Effectuer le dépannage de base (Parcourir, Démarrer, arrêter, redémarrer hello application)</span><span class="sxs-lookup"><span data-stu-id="4e3d2-176">Perform basic troubleshooting (browse, start, stop, restart hello app)</span></span>
- <span data-ttu-id="4e3d2-177">Obtenez des notifications push pour les événements critiques.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-177">Get push notifications for critical events.</span></span>

![Compagnon App Service](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="4e3d2-179">[![Compagnon App Service - App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Compagnon App Service - Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="4e3d2-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="4e3d2-180">Vous pouvez installer le Guide du Service d’applications à partir de hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) ou [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="4e3d2-180">You can install App Service companion from hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="4e3d2-181"><a name="diagnose"></a> Étape 4 : Diagnostiquer et résoudre les problèmes</span><span class="sxs-lookup"><span data-stu-id="4e3d2-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="4e3d2-182">**Diagnostiquer et résoudre les problèmes** permet de distinguer les problèmes d’application des problèmes de plateforme.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="4e3d2-183">Il peut également suggérer des tooget de limiter les risques votre toohealthy précédent de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-183">It can also suggest possible mitigations tooget your Web App back toohealthy.</span></span>

![Diagnostiquer et résoudre les problèmes](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="4e3d2-185">Continuer avec les étapes précédentes du formulaire exemple hello, nous pouvons voir qu’application hello a été difficultés marquée.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-185">Continuing with hello example form previous steps, we can see that hello application has been having availably issues.</span></span> <span data-ttu-id="4e3d2-186">En revanche, la disponibilité de plateforme hello n’a pas déplacé de 100 %.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-186">In contrast, hello platform availability has not moved from 100%.</span></span>

<span data-ttu-id="4e3d2-187">Lorsque application hello pose problème et hello reste plateforme haut, il est montre clairement que nous avons affaire à un problème d’application.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-187">When hello app is having issue and hello platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="4e3d2-188"><a name="logging"></a> Étape 5 - Journalisation</span><span class="sxs-lookup"><span data-stu-id="4e3d2-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="4e3d2-189">Maintenant que nous avons cerner le problème d’application hello échecs tooan, nous pouvons examiner tooget de journaux des applications et le serveur hello plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-189">Now that we have narrowed down hello failures tooan application issue, we can look at hello application and server logs tooget more information.</span></span>

<span data-ttu-id="4e3d2-190">Journalisation permet de toocollect les deux **Application Diagnostics** et **Diagnostics du serveur Web** journaux pour votre application Web.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-190">Logging allows you toocollect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="4e3d2-191">Diagnostics d’application</span><span class="sxs-lookup"><span data-stu-id="4e3d2-191">Application Diagnostics</span></span>
<span data-ttu-id="4e3d2-192">Application diagnostics permet de traces toocapture vous produites par l’application hello lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-192">Application diagnostics allows you toocapture traces produced by hello application at runtime.</span></span>

<span data-ttu-id="4e3d2-193">Ajout de traçage tooyour application améliore considérablement votre capacité toodebug et les problèmes liés au point de code confidentiel.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-193">Adding tracing tooyour application greatly improves your ability toodebug and pin-point issues.</span></span>

<span data-ttu-id="4e3d2-194">Dans ASP.NET, vous pouvez vous connecter à l’aide de traces d’application [classe System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate les événements capturés par l’infrastructure de journal hello.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate events that are captured by hello log infrastructure.</span></span> <span data-ttu-id="4e3d2-195">Vous pouvez également spécifier la gravité hello de trace hello pour le filtrage plus facile.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-195">You can also specify hello severity of hello trace for easier filtering.</span></span>

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
<span data-ttu-id="4e3d2-196">journal des applications tooenable accédez trop**analyse** > **journaux de Diagnostic** et activer l’Application enregistre à l’aide de hello bascule.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-196">tooenable Application logging Go too**Monitoring** > **Diagnostic Logs** and Enable Application Logging using hello toggles.</span></span>

![Surveiller l’application](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="4e3d2-198">Journaux des applications peuvent être de système de fichiers de l’application Web de tooyour stockée ou poussé tooblob stockage.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-198">Application logs can be stored tooyour Web App's file system or pushed out tooblob storage.</span></span> <span data-ttu-id="4e3d2-199">Pour les scénarios de production, il est recommandé toouse stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-199">For production scenarios, it's recommended toouse blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e3d2-200">L’activation de la journalisation a une incidence sur les performances de votre application et sur l’utilisation des ressources.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="4e3d2-201">Pour les scénarios de production, les journaux d’erreurs sont recommandés.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="4e3d2-202">Activez une journalisation plus détaillée uniquement en cas de problème.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="4e3d2-203">Diagnostics de serveur web</span><span class="sxs-lookup"><span data-stu-id="4e3d2-203">Web Server Diagnostics</span></span>
<span data-ttu-id="4e3d2-204">Les journaux des serveurs web sont générés même si votre application n’est pas instrumentée.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="4e3d2-205">App Service peut collecter trois types de journaux de serveur :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="4e3d2-206">**Journalisation du serveur web**</span><span class="sxs-lookup"><span data-stu-id="4e3d2-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="4e3d2-207">Informations sur les transactions HTTP à l’aide de hello [format de fichier journal étendu W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-207">Information about HTTP transactions using hello [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="4e3d2-208">Utile lors de la détermination des métriques d’un site global comme nombre hello de demandes traitées ou le nombre de requêtes qui proviennent d’une adresse IP spécifique.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-208">Useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="4e3d2-209">**Messages d’erreurs détaillés**</span><span class="sxs-lookup"><span data-stu-id="4e3d2-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="4e3d2-210">Informations d’erreur détaillées pour les codes d’état HTTP qui indiquent un échec (code d’état 400 ou supérieur).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="4e3d2-211">En savoir plus sur la journalisation d’erreurs détaillée</span><span class="sxs-lookup"><span data-stu-id="4e3d2-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="4e3d2-212">**Suivi des demandes ayant échoué**</span><span class="sxs-lookup"><span data-stu-id="4e3d2-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="4e3d2-213">Des informations détaillées sur les demandes ayant échoué, y compris une trace des composants d’IIS hello utilisé tooprocess hello demande et hello temps dans chaque composant.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-213">Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span>
    - <span data-ttu-id="4e3d2-214">Les journaux de demandes ayant échoué sont utiles lors de la tentative de tooisolate ce qui provoque une erreur HTTP spécifique.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-214">Failed request logs are useful when trying tooisolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="4e3d2-215">En savoir plus sur le suivi des demandes ayant échoué</span><span class="sxs-lookup"><span data-stu-id="4e3d2-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="4e3d2-216">journalisation du serveur tooenable :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-216">tooenable Server logging:</span></span>
- <span data-ttu-id="4e3d2-217">Accédez trop**analyse** > **journaux de Diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-217">go too**Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="4e3d2-218">Activer hello différents types de Diagnostics du serveur Web à l’aide de hello bascule.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-218">Enable hello different types of Web Server Diagnostics using hello toggles.</span></span>

![Surveiller l’application](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="4e3d2-220">L’activation de la journalisation a une incidence sur les performances de votre application et sur l’utilisation des ressources.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="4e3d2-221">Pour les scénarios de production, les journaux d’erreurs sont recommandés. Activez une journalisation plus détaillée uniquement en cas de problème.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="4e3d2-222">Accès aux journaux</span><span class="sxs-lookup"><span data-stu-id="4e3d2-222">Accessing Logs</span></span>
<span data-ttu-id="4e3d2-223">Les journaux enregistrés dans le stockage d’objets blob sont accessibles à l’aide de l’Explorateur de stockage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="4e3d2-224">Journaux stockés dans le système de fichiers de l’application hello Web sont accessibles via FTP sous hello suivant des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-224">Logs stored in hello Web App's filesystem are accessed through FTP under hello following paths:</span></span>

- <span data-ttu-id="4e3d2-225">**Journaux d’application** - `%HOME%/LogFiles/Application/`</span><span class="sxs-lookup"><span data-stu-id="4e3d2-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="4e3d2-226">Ce dossier contient un ou plusieurs fichiers texte contenant des informations générées dans le cadre de la journalisation des applications.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="4e3d2-227">**Suivi des demandes ayant échoué** - `%HOME%/LogFiles/W3SVC#########/`</span><span class="sxs-lookup"><span data-stu-id="4e3d2-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="4e3d2-228">Ce dossier contient un fichier XSL et un ou plusieurs fichiers XML.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="4e3d2-229">**Journaux d’erreurs détaillés** - `%HOME%/LogFiles/DetailedErrors/`</span><span class="sxs-lookup"><span data-stu-id="4e3d2-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="4e3d2-230">Ce dossier contient un ou plusieurs fichiers .htm incluant des informations détaillées sur les erreurs HTTP générées par votre application.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="4e3d2-231">**Journaux des serveurs web** - `%HOME%/LogFiles/http/RawLogs`</span><span class="sxs-lookup"><span data-stu-id="4e3d2-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="4e3d2-232">Ce dossier contient un ou plusieurs fichiers de texte formatés à l’aide du format de fichier journal étendu hello W3C.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-232">This folder contains one or more text files formatted using hello W3C extended log file format.</span></span>

## <span data-ttu-id="4e3d2-233"><a name="streaming"></a> Étape 6 - Diffusion de journaux</span><span class="sxs-lookup"><span data-stu-id="4e3d2-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="4e3d2-234">Journaux de diffusion en continu sont pratiques lorsque vous déboguez une application, car elle enregistre le temps par rapport trop[l’accès aux journaux de hello](#Accessing-Logs) via FTP.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-234">Streaming logs are convenient when debugging an application since it saves time compared too[accessing hello logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="4e3d2-235">App Service peut diffuser les **journaux d’application** et les **journaux de serveur web** lorsqu’ils sont générés.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="4e3d2-236">Avant d’essayer de journaux de toostream, assurez-vous que vous avez activé la collecte des journaux comme décrit dans hello [journalisation](#logging) section.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-236">Before trying toostream logs, make sure you have enabled collecting logs as described in hello [Logging](#logging) section.</span></span>

<span data-ttu-id="4e3d2-237">journaux de toostream, accédez trop**analyse**> **flux du journal**.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-237">toostream logs, go too**Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="4e3d2-238">Sélectionnez **Journaux d’application** ou **Journaux des serveurs web** en fonction des informations que vous recherchez.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="4e3d2-239">À ce stade, vous pouvez aussi suspendre, redémarrer et vider le tampon de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-239">From here, you can also pause, restart, and clear hello buffer.</span></span>

![Journaux en continu](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="4e3d2-241">Les journaux sont générés uniquement lorsque l’application hello est le trafic, vous pouvez également augmenter détail hello de tooget de journaux des événements ou des informations plus.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-241">Logs are only generated when there is traffic on hello app, you can also increase hello verbosity of logs tooget more events or information.</span></span>

## <span data-ttu-id="4e3d2-242"><a name="remote"></a> Étape 7 - Débogage à distance</span><span class="sxs-lookup"><span data-stu-id="4e3d2-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="4e3d2-243">Une fois que vous avez source hello de branches de code confidentiel des problèmes d’applications hello, utilisez **débogage distant** toowalk via le code de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-243">Once you have pin-pointed hello source of hello applications problems, use **Remote Debugging** toowalk through hello code.</span></span>

<span data-ttu-id="4e3d2-244">Permet de débogage distant vous attacher un débogueur de tooyour application Web en cours d’exécution dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-244">Remote debugging lets you attach a debugger tooyour Web App running in hello cloud.</span></span> <span data-ttu-id="4e3d2-245">Vous pouvez définir des points d’arrêt, manipuler directement de mémoire, parcourir le code et même modifier le chemin d’accès du code hello exactement comme vous le feriez pour une application en cours d’exécution localement.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-245">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path just like you do for an app running locally.</span></span>

<span data-ttu-id="4e3d2-246">tooattach hello débogueur tooyour l’application en cours d’exécution dans le cloud de hello :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-246">tooattach hello debugger tooyour app running in hello cloud:</span></span>

- <span data-ttu-id="4e3d2-247">À l’aide de Visual Studio 2017, solution hello ouvert pour l’application hello souhaité toodebug</span><span class="sxs-lookup"><span data-stu-id="4e3d2-247">Using Visual Studio 2017, open hello solution for hello app you want toodebug</span></span>
- <span data-ttu-id="4e3d2-248">Définissez des points d’arrêt comme vous le feriez pour un développement en local.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="4e3d2-249">Ouvrez **l’explorateur de cloud** (ctr + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="4e3d2-250">Connectez-vous avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="4e3d2-251">Rechercher hello application toodebug</span><span class="sxs-lookup"><span data-stu-id="4e3d2-251">Find hello app you want toodebug</span></span>
- <span data-ttu-id="4e3d2-252">Sélectionnez **attacher le débogueur** hello du formulaire **Actions** volet.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-252">Select **Attach Debugger** form hello **Actions** pane.</span></span>

![Débogage à distance](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="4e3d2-254">Visual Studio configure votre application pour le débogage distant et lance une fenêtre de navigateur qui navigue tooyour application.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates tooyour app.</span></span> <span data-ttu-id="4e3d2-255">Parcourir votre application tootrigger des points d’arrêt et de parcourir le code de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-255">Browse through your app tootrigger break points and step through hello code.</span></span>

> [!WARNING]
> <span data-ttu-id="4e3d2-256">Nous vous déconseillons d'exécuter le mode débogage en production.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="4e3d2-257">Si votre application de production n’est pas mis à l’échelle des instances de serveur toomultiple, débogage empêcher serveur hello web répond tooother demandes.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-257">If your production app is not scaled out toomultiple server instances, debugging prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="4e3d2-258">Pour résoudre des problèmes de production, votre meilleure ressource est trop[configurer la journalisation](#logging) et [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-258">For troubleshooting production problems, your best resource is too[configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="4e3d2-259"><a name="explorer"></a> Étape 8 : Process Explorer</span><span class="sxs-lookup"><span data-stu-id="4e3d2-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="4e3d2-260">Lorsque votre application est remontée toomore plusieurs instances, **Explorateur de processus** peut vous aider à identifier des problèmes spécifiques d’instance.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-260">When your application is scaled out toomore than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="4e3d2-261">Utilisez **Process Explorer** pour :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="4e3d2-262">Énumérer tous les processus hello entre différentes instances de votre plan App Service.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-262">Enumerate all hello processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="4e3d2-263">Extraire et afficher les poignées de hello et modules associés à chaque processus.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-263">Drill down and view hello handles and modules associated with each process.</span></span>
- <span data-ttu-id="4e3d2-264">Nombre d’UC de la vue, le jeu de travail et le Thread à hello traiter au niveau toohelp vous identifier les processus d’échappement</span><span class="sxs-lookup"><span data-stu-id="4e3d2-264">View CPU, Working Set, and Thread count at hello process level toohelp you identify runaway processes</span></span>
- <span data-ttu-id="4e3d2-265">rechercher des descripteurs de fichiers ouverts, voire arrêter une instance de processus spécifique.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="4e3d2-266">Process Explorer se trouve sous **Surveillance** > **Process Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Process Explorer](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="4e3d2-268"><a name="insights"></a> Étape 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e3d2-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="4e3d2-269">**Application Insights** fournit des fonctionnalités avancées de profilage et de surveillance de votre application.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="4e3d2-270">Utilisez Application Insights toodetect et diagnostiquer les problèmes de performances dans votre application Web et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-270">Use Application Insights toodetect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="4e3d2-271">Vous pouvez activer Application Insights pour votre application web sous **Surveillance** > **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="4e3d2-272">Application Insights peuvent vous inviter tooinstall hello Application Insights site extension toostart collecte de données.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-272">Application Insights might prompt you tooinstall hello Application Insights site extension toostart collecting data.</span></span> <span data-ttu-id="4e3d2-273">Installation de l’extension de site hello entraîne un redémarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-273">Installing hello site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="4e3d2-275">Application Insights a un grand nombre de fonctionnalités défini, toolearn, suivez les liens de hello inclus dans hello [étapes](#next) section.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-275">Application Insights has a rich feature set, toolearn more, follow hello links included in hello [Next Steps](#next) section.</span></span>

## <span data-ttu-id="4e3d2-276"><a name="next"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e3d2-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="4e3d2-277">Présentation d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e3d2-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="4e3d2-278">Surveiller les performances de l’application web Azure avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e3d2-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="4e3d2-279">Analyse de la disponibilité et de la réactivité d’un site web avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e3d2-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
