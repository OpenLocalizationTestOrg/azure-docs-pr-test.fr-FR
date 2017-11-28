---
title: Corriger les erreurs 502 Passerelle incorrecte, 503 Services indisponibles | Microsoft Docs
description: "Corriger les erreurs « 502 Passerelle incorrecte » et « 503 Service indisponible » dans votre application web hébergée dans Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: 502 Passerelle incorrecte, 503 Service indisponible, erreur 503, erreur 502
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 397a6aaf7dc27adfa0fc0e722b8a2be5cc1d75f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="4a152-104">Résoudre les erreurs HTTP de type « 502 Passerelle incorrecte » et « 503 Service indisponible » dans vos applications web Azure</span><span class="sxs-lookup"><span data-stu-id="4a152-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="4a152-105">« 502 Passerelle incorrecte » et « 503 Service indisponible » sont des erreurs courantes dans votre application web hébergée dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="4a152-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="4a152-106">Cet article vous permet de résoudre ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="4a152-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="4a152-107">Si vous avez besoin d'aide supplémentaire concernant n'importe quel point de cet article, contactez les experts Azure sur les [forums MSDN Azure et Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="4a152-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="4a152-108">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="4a152-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="4a152-109">Accédez au [site de support Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Obtenir un support**.</span><span class="sxs-lookup"><span data-stu-id="4a152-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="4a152-110">Symptôme</span><span class="sxs-lookup"><span data-stu-id="4a152-110">Symptom</span></span>
<span data-ttu-id="4a152-111">Lorsque vous accédez à l'application web, elle retourne un message d’erreur HTTP « 502 Passerelle incorrecte » ou HTTP « 503 Service non disponible ».</span><span class="sxs-lookup"><span data-stu-id="4a152-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="4a152-112">Cause :</span><span class="sxs-lookup"><span data-stu-id="4a152-112">Cause</span></span>
<span data-ttu-id="4a152-113">Ce problème est souvent dû à des problèmes au niveau de l’application, tels que :</span><span class="sxs-lookup"><span data-stu-id="4a152-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="4a152-114">demandes exigeant beaucoup de temps ;</span><span class="sxs-lookup"><span data-stu-id="4a152-114">requests taking a long time</span></span>
* <span data-ttu-id="4a152-115">un taux d’utilisation élevé de la mémoire/UC par l’application ;</span><span class="sxs-lookup"><span data-stu-id="4a152-115">application using high memory/CPU</span></span>
* <span data-ttu-id="4a152-116">un blocage de l’application en raison d’une exception.</span><span class="sxs-lookup"><span data-stu-id="4a152-116">application crashing due to an exception.</span></span>

## <a name="troubleshooting-steps-to-solve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="4a152-117">Étapes de dépannage pour résoudre les erreurs « 503 Service indisponible » et « 502 Passerelle incorrecte »</span><span class="sxs-lookup"><span data-stu-id="4a152-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="4a152-118">Le dépannage peut être divisé en trois tâches distinctes, dans un ordre séquentiel :</span><span class="sxs-lookup"><span data-stu-id="4a152-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="4a152-119">Observer et contrôler le comportement de l’application</span><span class="sxs-lookup"><span data-stu-id="4a152-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="4a152-120">Collecter les données</span><span class="sxs-lookup"><span data-stu-id="4a152-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="4a152-121">Résoudre le problème</span><span class="sxs-lookup"><span data-stu-id="4a152-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="4a152-122">[App Service Web Apps](/services/app-service/web/) vous offre différentes options à chaque étape.</span><span class="sxs-lookup"><span data-stu-id="4a152-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="4a152-123">1. Observer et contrôler le comportement de l'application</span><span class="sxs-lookup"><span data-stu-id="4a152-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="4a152-124">Suivi de l’état du service</span><span class="sxs-lookup"><span data-stu-id="4a152-124">Track Service health</span></span>
<span data-ttu-id="4a152-125">Microsoft Azure publie chaque interruption du service et chaque dégradation des performances.</span><span class="sxs-lookup"><span data-stu-id="4a152-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="4a152-126">Vous pouvez assurer le suivi de l’état du service sur le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4a152-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="4a152-127">Pour plus d’informations, consultez la rubrique [Suivi de l’état du service](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="4a152-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="4a152-128">Contrôle de votre application web</span><span class="sxs-lookup"><span data-stu-id="4a152-128">Monitor your web app</span></span>
<span data-ttu-id="4a152-129">Cette option vous permet de savoir si votre application rencontre des problèmes.</span><span class="sxs-lookup"><span data-stu-id="4a152-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="4a152-130">Dans le panneau de votre application web, cliquez sur la vignette **Demandes et erreurs** .</span><span class="sxs-lookup"><span data-stu-id="4a152-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="4a152-131">Le panneau **Mesure** affiche toutes les mesures que vous pouvez ajouter.</span><span class="sxs-lookup"><span data-stu-id="4a152-131">The **Metric** blade will show you all the metrics you can add.</span></span>

<span data-ttu-id="4a152-132">Parmi les mesures que vous pouvez surveiller pour votre application web, se trouvent</span><span class="sxs-lookup"><span data-stu-id="4a152-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="4a152-133">Plage de travail moyenne de la mémoire</span><span class="sxs-lookup"><span data-stu-id="4a152-133">Average memory working set</span></span>
* <span data-ttu-id="4a152-134">Temps de réponse moyen</span><span class="sxs-lookup"><span data-stu-id="4a152-134">Average response time</span></span>
* <span data-ttu-id="4a152-135">Temps processeur</span><span class="sxs-lookup"><span data-stu-id="4a152-135">CPU time</span></span>
* <span data-ttu-id="4a152-136">Plage de travail de la mémoire</span><span class="sxs-lookup"><span data-stu-id="4a152-136">Memory working set</span></span>
* <span data-ttu-id="4a152-137">Demandes</span><span class="sxs-lookup"><span data-stu-id="4a152-137">Requests</span></span>

![surveiller l’application web pour résoudre les erreurs HTTP de type « 502 Passerelle incorrecte » et « 503 Service indisponible »](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="4a152-139">Pour plus d’informations, consultez :</span><span class="sxs-lookup"><span data-stu-id="4a152-139">For more information, see:</span></span>

* [<span data-ttu-id="4a152-140">Surveiller les applications web dans Microsoft Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4a152-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="4a152-141">Réception de notifications d'alerte</span><span class="sxs-lookup"><span data-stu-id="4a152-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="4a152-142">2. Collecter les données</span><span class="sxs-lookup"><span data-stu-id="4a152-142">2. Collect data</span></span>
#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="4a152-143">Utilisation du portail de support Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4a152-143">Use the Azure App Service Support Portal</span></span>
<span data-ttu-id="4a152-144">Web Apps vous offre la possibilité de résoudre les problèmes liés à votre application web grâce à des journaux HTTP, les journaux des événements, les vidages de processus et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="4a152-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="4a152-145">Vous pouvez accéder à toutes ces informations à l’aide de notre portail de support à l’adresse **http://&lt;your app name>.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="4a152-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="4a152-146">Le portail de support Azure App Service vous propose trois onglets distincts pour prendre en charge les trois étapes d’un scénario de dépannage courant :</span><span class="sxs-lookup"><span data-stu-id="4a152-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="4a152-147">Observer le comportement actuel</span><span class="sxs-lookup"><span data-stu-id="4a152-147">Observe current behavior</span></span>
2. <span data-ttu-id="4a152-148">Analyser en collectant des informations de diagnostic et en exécutant les analyseurs intégrés</span><span class="sxs-lookup"><span data-stu-id="4a152-148">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="4a152-149">Résoudre</span><span class="sxs-lookup"><span data-stu-id="4a152-149">Mitigate</span></span>

<span data-ttu-id="4a152-150">Si le problème est en cours, cliquez sur **Analyser** > **Diagnostics** > **Diagnostiquer maintenant** pour créer une session de diagnostic, qui recueillera les journaux HTTP, les journaux de l'observateur d'événements, les vidages de mémoire, les journaux d'erreurs PHP et le rapport de traitement PHP.</span><span class="sxs-lookup"><span data-stu-id="4a152-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="4a152-151">Une fois les données collectées, une analyse sera également exécutée sur les données pour vous fournir un rapport HTML.</span><span class="sxs-lookup"><span data-stu-id="4a152-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span></span>

<span data-ttu-id="4a152-152">Si vous souhaitez télécharger les données, par défaut, celles-ci sont stockées dans le dossier D:\home\data\DaaS.</span><span class="sxs-lookup"><span data-stu-id="4a152-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="4a152-153">Pour plus d'informations sur le portail de support Azure App Service, consultez [Nouvelles mises à jour à l'extension de site de support pour les sites web Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="4a152-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="4a152-154">Utilisation de la console de débogage Kudu</span><span class="sxs-lookup"><span data-stu-id="4a152-154">Use the Kudu Debug Console</span></span>
<span data-ttu-id="4a152-155">Web Apps est fourni avec une console de débogage que vous pouvez utiliser pour le débogage, l’exploration, le téléchargement de fichiers, ainsi que les points de terminaison JSON pour obtenir des informations relatives à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="4a152-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="4a152-156">Il s'agit de la *console Kudu* ou du *tableau de bord SCM* pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="4a152-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="4a152-157">Vous pouvez accéder à ce tableau de bord avec le lien **https://&lt;Your app name>.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="4a152-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="4a152-158">Kudu fournit, entre autres, les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4a152-158">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="4a152-159">paramètres d’environnement pour votre application ;</span><span class="sxs-lookup"><span data-stu-id="4a152-159">environment settings for your application</span></span>
* <span data-ttu-id="4a152-160">flux de journal ;</span><span class="sxs-lookup"><span data-stu-id="4a152-160">log stream</span></span>
* <span data-ttu-id="4a152-161">vidage de diagnostic ;</span><span class="sxs-lookup"><span data-stu-id="4a152-161">diagnostic dump</span></span>
* <span data-ttu-id="4a152-162">console de débogage dans laquelle vous pouvez exécuter les applets de commande Powershell et les commandes DOS de base.</span><span class="sxs-lookup"><span data-stu-id="4a152-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="4a152-163">Autre fonctionnalité utile de Kudu, dans le cas où votre application lève des exceptions de première chance, vous pouvez utiliser Kudu et l’outil Procdump de SysInternals pour créer des vidages de mémoire.</span><span class="sxs-lookup"><span data-stu-id="4a152-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="4a152-164">Ces vidages de mémoire sont des instantanés du processus et peuvent souvent vous aider à résoudre les problèmes plus complexes avec votre application web.</span><span class="sxs-lookup"><span data-stu-id="4a152-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="4a152-165">Pour plus d'informations sur les fonctionnalités disponibles dans Kudu, consultez [Outils en ligne de Sites Web Azure que vous devez connaître](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="4a152-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="4a152-166">3. Résoudre le problème</span><span class="sxs-lookup"><span data-stu-id="4a152-166">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="4a152-167">Mise à l’échelle de l’application web</span><span class="sxs-lookup"><span data-stu-id="4a152-167">Scale the web app</span></span>
<span data-ttu-id="4a152-168">Dans Azure App Service, pour améliorer les performances et le débit, vous pouvez ajuster l’échelle à laquelle vous exécutez votre application.</span><span class="sxs-lookup"><span data-stu-id="4a152-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="4a152-169">La mise à l’échelle d’une application web implique deux actions associées : l’évolution de votre plan App Service vers un niveau de tarification supérieur et la configuration de certains paramètres après le passage à ce niveau de tarification supérieur.</span><span class="sxs-lookup"><span data-stu-id="4a152-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="4a152-170">Pour plus d'informations sur la mise à l'échelle, consultez [Mise à l'échelle d'une application web dans Microsoft Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4a152-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="4a152-171">En outre, vous pouvez choisir d’exécuter votre application sur plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="4a152-171">Additionally, you can choose to run your application on more than one instance .</span></span> <span data-ttu-id="4a152-172">Non seulement cela vous offre plus de capacité de traitement, mais également un certain niveau de tolérance aux pannes.</span><span class="sxs-lookup"><span data-stu-id="4a152-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="4a152-173">Si le processus s’arrête sur une instance, l’autre instance continue de servir les requêtes.</span><span class="sxs-lookup"><span data-stu-id="4a152-173">If the process goes down on one instance, the other instance will still continue serving requests.</span></span>

<span data-ttu-id="4a152-174">Vous pouvez définir la mise à l’échelle pour qu’elle soit manuelle ou automatique.</span><span class="sxs-lookup"><span data-stu-id="4a152-174">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="4a152-175">Utilisation de la correction automatique (AutoHeal)</span><span class="sxs-lookup"><span data-stu-id="4a152-175">Use AutoHeal</span></span>
<span data-ttu-id="4a152-176">La correction automatique (AutoHeal) recycle le processus de travail pour votre application en fonction des paramètres que vous choisissez (comme les modifications de configuration, les requêtes, les limites de mémoire ou le temps nécessaire pour exécuter une requête).</span><span class="sxs-lookup"><span data-stu-id="4a152-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="4a152-177">La plupart du temps, le recyclage du processus est le moyen le plus rapide pour résoudre un problème.</span><span class="sxs-lookup"><span data-stu-id="4a152-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="4a152-178">Même si vous pouvez toujours redémarrer l’application web directement dans le portail Azure, la fonctionnalité de correction automatique (AutoHeal) le fera automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="4a152-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="4a152-179">Il vous suffit d’ajouter des déclencheurs dans le fichier web.config racine pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="4a152-179">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="4a152-180">Notez que ces paramètres fonctionnent de la même façon même si votre application n’est pas une application .Net.</span><span class="sxs-lookup"><span data-stu-id="4a152-180">Note that these settings would work in the same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="4a152-181">Pour plus d'informations, consultez [Correction automatique de Sites Web Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="4a152-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="4a152-182">Redémarrage de l’application web</span><span class="sxs-lookup"><span data-stu-id="4a152-182">Restart the web app</span></span>
<span data-ttu-id="4a152-183">Il s’agit souvent du moyen le plus simple de résoudre des problèmes à usage unique.</span><span class="sxs-lookup"><span data-stu-id="4a152-183">This is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="4a152-184">Dans le [portail Azure](https://portal.azure.com/), sur le panneau de votre application web, vous avez la possibilité d’arrêter ou de redémarrer votre application.</span><span class="sxs-lookup"><span data-stu-id="4a152-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![redémarrer l’application pour résoudre les erreurs HTTP de type « 502 Passerelle incorrecte » et « 503 Service indisponible »](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="4a152-186">Vous pouvez également gérer votre application web à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a152-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="4a152-187">Pour plus d'informations, consultez [Utilisation d'Azure PowerShell avec le Gestionnaire de ressources Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4a152-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

