---
title: "passerelle incorrecte d’aaaFix 502, 503 service non disponibles erreurs | Documents Microsoft"
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
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="db12f-104">Résoudre les erreurs HTTP de type « 502 Passerelle incorrecte » et « 503 Service indisponible » dans vos applications web Azure</span><span class="sxs-lookup"><span data-stu-id="db12f-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="db12f-105">« 502 Passerelle incorrecte » et « 503 Service indisponible » sont des erreurs courantes dans votre application web hébergée dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="db12f-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="db12f-106">Cet article vous permet de résoudre ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="db12f-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="db12f-107">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello MSDN Azure et hello forums de débordement de pile](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="db12f-107">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="db12f-108">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="db12f-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="db12f-109">Accédez toohello [site de Support technique Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="db12f-109">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="db12f-110">Symptôme</span><span class="sxs-lookup"><span data-stu-id="db12f-110">Symptom</span></span>
<span data-ttu-id="db12f-111">Lorsque vous accédez à l’application web toohello, elle retourne un HTTP Erreur de « 502 Passerelle incorrecte » ou un HTTP erreur « 503 Service non disponible ».</span><span class="sxs-lookup"><span data-stu-id="db12f-111">When you browse toohello web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="db12f-112">Cause :</span><span class="sxs-lookup"><span data-stu-id="db12f-112">Cause</span></span>
<span data-ttu-id="db12f-113">Ce problème est souvent dû à des problèmes au niveau de l’application, tels que :</span><span class="sxs-lookup"><span data-stu-id="db12f-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="db12f-114">demandes exigeant beaucoup de temps ;</span><span class="sxs-lookup"><span data-stu-id="db12f-114">requests taking a long time</span></span>
* <span data-ttu-id="db12f-115">un taux d’utilisation élevé de la mémoire/UC par l’application ;</span><span class="sxs-lookup"><span data-stu-id="db12f-115">application using high memory/CPU</span></span>
* <span data-ttu-id="db12f-116">panne en raison de l’exception de tooan d’application.</span><span class="sxs-lookup"><span data-stu-id="db12f-116">application crashing due tooan exception.</span></span>

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="db12f-117">Dépannage des étapes toosolve « 502 Passerelle incorrecte » et les erreurs « 503 service non disponible »</span><span class="sxs-lookup"><span data-stu-id="db12f-117">Troubleshooting steps toosolve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="db12f-118">Le dépannage peut être divisé en trois tâches distinctes, dans un ordre séquentiel :</span><span class="sxs-lookup"><span data-stu-id="db12f-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="db12f-119">Observer et contrôler le comportement de l’application</span><span class="sxs-lookup"><span data-stu-id="db12f-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="db12f-120">Collecter les données</span><span class="sxs-lookup"><span data-stu-id="db12f-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="db12f-121">Limiter le problème de hello</span><span class="sxs-lookup"><span data-stu-id="db12f-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="db12f-122">[App Service Web Apps](/services/app-service/web/) vous offre différentes options à chaque étape.</span><span class="sxs-lookup"><span data-stu-id="db12f-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="db12f-123">1. Observer et contrôler le comportement de l'application</span><span class="sxs-lookup"><span data-stu-id="db12f-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="db12f-124">Suivi de l’état du service</span><span class="sxs-lookup"><span data-stu-id="db12f-124">Track Service health</span></span>
<span data-ttu-id="db12f-125">Microsoft Azure publie chaque interruption du service et chaque dégradation des performances.</span><span class="sxs-lookup"><span data-stu-id="db12f-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="db12f-126">Vous pouvez suivre la santé hello du service de hello sur hello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="db12f-126">You can track hello health of hello service on hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="db12f-127">Pour plus d’informations, consultez la rubrique [Suivi de l’état du service](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="db12f-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="db12f-128">Contrôle de votre application web</span><span class="sxs-lookup"><span data-stu-id="db12f-128">Monitor your web app</span></span>
<span data-ttu-id="db12f-129">Cette option permet de vous toofind out si votre application rencontre des problèmes.</span><span class="sxs-lookup"><span data-stu-id="db12f-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="db12f-130">Dans le panneau de votre application web, cliquez sur hello **demandes et les erreurs** vignette.</span><span class="sxs-lookup"><span data-stu-id="db12f-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="db12f-131">Hello **métrique** panneau affiche toutes les métriques hello que vous pouvez ajouter.</span><span class="sxs-lookup"><span data-stu-id="db12f-131">hello **Metric** blade will show you all hello metrics you can add.</span></span>

<span data-ttu-id="db12f-132">Parmi les métriques hello que vous pouvez vouloir toomonitor pour votre application web</span><span class="sxs-lookup"><span data-stu-id="db12f-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="db12f-133">Plage de travail moyenne de la mémoire</span><span class="sxs-lookup"><span data-stu-id="db12f-133">Average memory working set</span></span>
* <span data-ttu-id="db12f-134">Temps de réponse moyen</span><span class="sxs-lookup"><span data-stu-id="db12f-134">Average response time</span></span>
* <span data-ttu-id="db12f-135">Temps processeur</span><span class="sxs-lookup"><span data-stu-id="db12f-135">CPU time</span></span>
* <span data-ttu-id="db12f-136">Plage de travail de la mémoire</span><span class="sxs-lookup"><span data-stu-id="db12f-136">Memory working set</span></span>
* <span data-ttu-id="db12f-137">Demandes</span><span class="sxs-lookup"><span data-stu-id="db12f-137">Requests</span></span>

![surveiller l’application web pour résoudre les erreurs HTTP de type « 502 Passerelle incorrecte » et « 503 Service indisponible »](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="db12f-139">Pour plus d’informations, consultez :</span><span class="sxs-lookup"><span data-stu-id="db12f-139">For more information, see:</span></span>

* [<span data-ttu-id="db12f-140">Surveiller les applications web dans Microsoft Azure App Service</span><span class="sxs-lookup"><span data-stu-id="db12f-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="db12f-141">Réception de notifications d'alerte</span><span class="sxs-lookup"><span data-stu-id="db12f-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="db12f-142">2. Collecter les données</span><span class="sxs-lookup"><span data-stu-id="db12f-142">2. Collect data</span></span>
#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="db12f-143">Utilisez hello portail de Support Azure App Service</span><span class="sxs-lookup"><span data-stu-id="db12f-143">Use hello Azure App Service Support Portal</span></span>
<span data-ttu-id="db12f-144">Web Apps fournit hello capacité tootroubleshoot problèmes connexes tooyour web application en examinant HTTP journaux, les journaux des événements, les vidages de processus et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="db12f-144">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="db12f-145">Vous pouvez accéder à toutes ces informations à l’aide de notre portail de support à l’adresse **http://&lt;your app name>.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="db12f-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="db12f-146">portail de Support technique Azure App Service Hello fournit trois onglets distincts toosupport hello trois étapes d’un scénario de dépannage courantes :</span><span class="sxs-lookup"><span data-stu-id="db12f-146">hello Azure App Service Support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="db12f-147">Observer le comportement actuel</span><span class="sxs-lookup"><span data-stu-id="db12f-147">Observe current behavior</span></span>
2. <span data-ttu-id="db12f-148">Analyser à la collecte des informations de diagnostic et en cours d’exécution hello analyseurs intégrés</span><span class="sxs-lookup"><span data-stu-id="db12f-148">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="db12f-149">Résoudre</span><span class="sxs-lookup"><span data-stu-id="db12f-149">Mitigate</span></span>

<span data-ttu-id="db12f-150">Si le problème de hello se produit dès maintenant, cliquez sur **analyser** > **Diagnostics** > **diagnostiquer maintenant** toocreate une session de diagnostic pour vous, qui collectera HTTP connecte, Observateur d’événements, mémoire dumps, les journaux d’erreurs PHP et PHP traitent le rapport.</span><span class="sxs-lookup"><span data-stu-id="db12f-150">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="db12f-151">Une fois la collecte des données de hello, il sera également exécuter une analyse sur les données de salutation et vous fournir un rapport HTML.</span><span class="sxs-lookup"><span data-stu-id="db12f-151">Once hello data is collected, it will also run an analysis on hello data and provide you with an HTML report.</span></span>

<span data-ttu-id="db12f-152">Dans le cas des données toodownload hello, par défaut, il est stocké dans le dossier de D:\home\data\DaaS hello.</span><span class="sxs-lookup"><span data-stu-id="db12f-152">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="db12f-153">Pour plus d’informations sur le portail de Support technique Azure App Service hello, consultez [tooSupport de nouvelles mises à jour Extension de Site des sites Web Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="db12f-153">For more information on hello Azure App Service Support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="db12f-154">Utilisez hello Kudu la Console de débogage</span><span class="sxs-lookup"><span data-stu-id="db12f-154">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="db12f-155">Web Apps est fourni avec une console de débogage que vous pouvez utiliser pour le débogage, l’exploration, le téléchargement de fichiers, ainsi que les points de terminaison JSON pour obtenir des informations relatives à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="db12f-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="db12f-156">Il s’agit de hello *Kudu Console* ou hello *tableau de bord SCM* pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="db12f-156">This is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="db12f-157">Vous pouvez accéder à ce tableau de bord en accédant le lien toohello **https://&lt;votre nom de l’application >.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="db12f-157">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="db12f-158">Certains des éléments de hello Kudu offre sont :</span><span class="sxs-lookup"><span data-stu-id="db12f-158">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="db12f-159">paramètres d’environnement pour votre application ;</span><span class="sxs-lookup"><span data-stu-id="db12f-159">environment settings for your application</span></span>
* <span data-ttu-id="db12f-160">flux de journal ;</span><span class="sxs-lookup"><span data-stu-id="db12f-160">log stream</span></span>
* <span data-ttu-id="db12f-161">vidage de diagnostic ;</span><span class="sxs-lookup"><span data-stu-id="db12f-161">diagnostic dump</span></span>
* <span data-ttu-id="db12f-162">console de débogage dans laquelle vous pouvez exécuter les applets de commande Powershell et les commandes DOS de base.</span><span class="sxs-lookup"><span data-stu-id="db12f-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="db12f-163">Une autre fonctionnalité utile de Kudu est que, dans le cas où votre application lève des exceptions de première chance, vous pouvez utiliser Kudu et images hello SysInternals outil Procdump toocreate mémoire.</span><span class="sxs-lookup"><span data-stu-id="db12f-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="db12f-164">Ces images mémoire sont des instantanés des processus de hello et peuvent vous aider à résoudre les problèmes plus complexes avec votre application web.</span><span class="sxs-lookup"><span data-stu-id="db12f-164">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="db12f-165">Pour plus d'informations sur les fonctionnalités disponibles dans Kudu, consultez [Outils en ligne de Sites Web Azure que vous devez connaître](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="db12f-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="db12f-166">3. Limiter le problème de hello</span><span class="sxs-lookup"><span data-stu-id="db12f-166">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="db12f-167">Échelle hello web app</span><span class="sxs-lookup"><span data-stu-id="db12f-167">Scale hello web app</span></span>
<span data-ttu-id="db12f-168">Dans Azure App Service, pour améliorer les performances et le débit, vous pouvez ajuster échelle hello à partir duquel vous exécutez votre application.</span><span class="sxs-lookup"><span data-stu-id="db12f-168">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="db12f-169">Mise à l’échelle d’une application web implique deux actions connexes : la modification de votre tooa de plan App Service supérieur tarification et configurer certains paramètres après avoir basculé toohello niveau de tarification supérieur.</span><span class="sxs-lookup"><span data-stu-id="db12f-169">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="db12f-170">Pour plus d'informations sur la mise à l'échelle, consultez [Mise à l'échelle d'une application web dans Microsoft Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="db12f-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="db12f-171">En outre, vous pouvez choisir toorun votre application sur plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="db12f-171">Additionally, you can choose toorun your application on more than one instance .</span></span> <span data-ttu-id="db12f-172">Non seulement cela vous offre plus de capacité de traitement, mais également un certain niveau de tolérance aux pannes.</span><span class="sxs-lookup"><span data-stu-id="db12f-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="db12f-173">Si hello processus tombe en panne sur une instance, hello autre instance toujours continue à servir les demandes.</span><span class="sxs-lookup"><span data-stu-id="db12f-173">If hello process goes down on one instance, hello other instance will still continue serving requests.</span></span>

<span data-ttu-id="db12f-174">Vous pouvez définir hello mise à l’échelle toobe manuel ou automatique.</span><span class="sxs-lookup"><span data-stu-id="db12f-174">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="db12f-175">Utilisation de la correction automatique (AutoHeal)</span><span class="sxs-lookup"><span data-stu-id="db12f-175">Use AutoHeal</span></span>
<span data-ttu-id="db12f-176">AutoHeal recycle le processus de travail hello pour votre application en fonction des paramètres que vous choisissez (par exemple, les modifications de configuration, les demandes, les limites de mémoire ou une durée de hello nécessaire tooexecute une demande).</span><span class="sxs-lookup"><span data-stu-id="db12f-176">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="db12f-177">La plupart du temps de hello, recycler le processus de hello est hello toorecover de façon plus rapide d’un problème.</span><span class="sxs-lookup"><span data-stu-id="db12f-177">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="db12f-178">Bien que vous pouvez toujours redémarrer hello web de l’application directement dans hello portail Azure, AutoHeal fera automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="db12f-178">Though you can always restart hello web app from directly within hello Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="db12f-179">Vous devez toodo est ajoutent des déclencheurs dans le fichier web.config racine de hello pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="db12f-179">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="db12f-180">Notez que ces paramètres fonctionnerait Bonjour même façon, même si votre application n’est pas un .net.</span><span class="sxs-lookup"><span data-stu-id="db12f-180">Note that these settings would work in hello same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="db12f-181">Pour plus d'informations, consultez [Correction automatique de Sites Web Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="db12f-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="db12f-182">Redémarrage de l’application web de hello</span><span class="sxs-lookup"><span data-stu-id="db12f-182">Restart hello web app</span></span>
<span data-ttu-id="db12f-183">Il s’agit souvent hello toorecover de façon la plus simple des problèmes à usage unique.</span><span class="sxs-lookup"><span data-stu-id="db12f-183">This is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="db12f-184">Sur hello [Azure Portal](https://portal.azure.com/), dans Panneau de votre application web, vous avez hello options toostop ou redémarrer votre application.</span><span class="sxs-lookup"><span data-stu-id="db12f-184">On hello [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![Redémarrez l’application toosolve HTTP erreurs 502 Passerelle incorrecte et 503 service non disponible](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="db12f-186">Vous pouvez également gérer votre application web à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db12f-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="db12f-187">Pour plus d'informations, consultez [Utilisation d'Azure PowerShell avec le Gestionnaire de ressources Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="db12f-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

