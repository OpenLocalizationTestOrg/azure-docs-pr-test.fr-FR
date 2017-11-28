---
title: alertes de tooset aaaUse Powershell dans Application Insights | Documents Microsoft
description: "Automatiser la configuration des e-mails de tooget Application Insights sur les modifications de métriques."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a><span data-ttu-id="706a7-103">Utilisez PowerShell tooset alertes dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="706a7-103">Use PowerShell tooset alerts in Application Insights</span></span>
<span data-ttu-id="706a7-104">Vous pouvez automatiser la configuration de hello de [alertes](app-insights-alerts.md) dans [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="706a7-104">You can automate hello configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="706a7-105">En outre, vous pouvez [définir webhooks tooautomate votre alerte tooan de réponse](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="706a7-105">In addition, you can [set webhooks tooautomate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="706a7-106">Si vous souhaitez que les ressources toocreate et des alertes sur hello même temps, envisagez de [à l’aide d’un modèle Azure Resource Manager](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="706a7-106">If you want toocreate resources and alerts at hello same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="706a7-107">Installation unique</span><span class="sxs-lookup"><span data-stu-id="706a7-107">One-time setup</span></span>
<span data-ttu-id="706a7-108">Si vous n’avez pas utilisé précédemment PowerShell avec votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="706a7-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="706a7-109">Installez le module de Azure Powershell de hello sur ordinateur hello où vous souhaitez les scripts toorun hello.</span><span class="sxs-lookup"><span data-stu-id="706a7-109">Install hello Azure Powershell module on hello machine where you want toorun hello scripts.</span></span>

* <span data-ttu-id="706a7-110">Installez le programme [Microsoft Web Platform Installer (v5 ou version ultérieure)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="706a7-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="706a7-111">Utiliser tooinstall Microsoft Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="706a7-111">Use it tooinstall Microsoft Azure Powershell</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="706a7-112">Se connecter tooAzure</span><span class="sxs-lookup"><span data-stu-id="706a7-112">Connect tooAzure</span></span>
<span data-ttu-id="706a7-113">Démarrer PowerShell d’Azure et [connecter tooyour abonnement](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="706a7-113">Start Azure PowerShell and [connect tooyour subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="706a7-114">Obtention d’alertes</span><span class="sxs-lookup"><span data-stu-id="706a7-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="706a7-115">Ajout d’alerte</span><span class="sxs-lookup"><span data-stu-id="706a7-115">Add alert</span></span>
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a><span data-ttu-id="706a7-116">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="706a7-116">Example 1</span></span>
<span data-ttu-id="706a7-117">M’avertir si les demandes de tooHTTP de réponse du serveur hello, moyenne plus de 5 minutes, est inférieure à 1 seconde.</span><span class="sxs-lookup"><span data-stu-id="706a7-117">Email me if hello server's response tooHTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="706a7-118">Ma ressource Application Insights est appelée IceCreamWebApp et se trouve dans le groupe de ressources Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="706a7-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="706a7-119">Je suis propriétaire hello Hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="706a7-119">I am hello owner of hello Azure subscription.</span></span>

<span data-ttu-id="706a7-120">Hello GUID est l’ID d’abonnement hello (pas hello clé d’instrumentation de l’application hello).</span><span class="sxs-lookup"><span data-stu-id="706a7-120">hello GUID is hello subscription ID (not hello instrumentation key of hello application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="706a7-121">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="706a7-121">Example 2</span></span>
<span data-ttu-id="706a7-122">J’ai une application dans laquelle utiliser [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport une mesure nommée « salesPerHour ».</span><span class="sxs-lookup"><span data-stu-id="706a7-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport a metric named "salesPerHour."</span></span> <span data-ttu-id="706a7-123">Envoyer un courrier électronique toomy collègues si « salesPerHour » est inférieur à 100, en moyenne plus de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="706a7-123">Send an email toomy colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

<span data-ttu-id="706a7-124">Hello même règle peut être utilisé pour la métrique de hello signalées à l’aide de hello [paramètre de mesure](app-insights-api-custom-events-metrics.md#properties) de suivi d’un autre appel de TrackEvent ou trackPageView.</span><span class="sxs-lookup"><span data-stu-id="706a7-124">hello same rule can be used for hello metric reported by using hello [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="706a7-125">Noms de métrique</span><span class="sxs-lookup"><span data-stu-id="706a7-125">Metric names</span></span>
| <span data-ttu-id="706a7-126">Nom de métrique</span><span class="sxs-lookup"><span data-stu-id="706a7-126">Metric name</span></span> | <span data-ttu-id="706a7-127">Nom d’écran</span><span class="sxs-lookup"><span data-stu-id="706a7-127">Screen name</span></span> | <span data-ttu-id="706a7-128">Description</span><span class="sxs-lookup"><span data-stu-id="706a7-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="706a7-129">Exceptions du navigateur</span><span class="sxs-lookup"><span data-stu-id="706a7-129">Browser exceptions</span></span> |<span data-ttu-id="706a7-130">Nombre d’exceptions non interceptées levées dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="706a7-130">Count of uncaught exceptions thrown in hello browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="706a7-131">Exceptions de serveur</span><span class="sxs-lookup"><span data-stu-id="706a7-131">Server exceptions</span></span> |<span data-ttu-id="706a7-132">Nombre d’exceptions non gérées levées par une application hello</span><span class="sxs-lookup"><span data-stu-id="706a7-132">Count of unhandled exceptions thrown by hello app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="706a7-133">Temps de traitement du client</span><span class="sxs-lookup"><span data-stu-id="706a7-133">Client processing time</span></span> |<span data-ttu-id="706a7-134">Temps écoulé entre la réception hello dernier octet d’un document jusqu'à ce que le chargement de DOM hello.</span><span class="sxs-lookup"><span data-stu-id="706a7-134">Time between receiving hello last byte of a document until hello DOM is loaded.</span></span> <span data-ttu-id="706a7-135">Les demandes asynchrones peuvent encore être en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="706a7-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="706a7-136">Temps de connexion au réseau pour le chargement de page</span><span class="sxs-lookup"><span data-stu-id="706a7-136">Page load network connect time</span></span> |<span data-ttu-id="706a7-137">Navigateur de hello temps prend tooconnect toohello réseau.</span><span class="sxs-lookup"><span data-stu-id="706a7-137">Time hello browser takes tooconnect toohello network.</span></span> <span data-ttu-id="706a7-138">Peut être 0 en cas de mise en cache.</span><span class="sxs-lookup"><span data-stu-id="706a7-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="706a7-139">Temps de réception de réponse</span><span class="sxs-lookup"><span data-stu-id="706a7-139">Receiving response time</span></span> |<span data-ttu-id="706a7-140">Temps écoulé entre l’envoi demande toostarting tooreceive réponse de navigateur.</span><span class="sxs-lookup"><span data-stu-id="706a7-140">Time between browser sending request toostarting tooreceive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="706a7-141">Temps d’envoi de demande</span><span class="sxs-lookup"><span data-stu-id="706a7-141">Send request time</span></span> |<span data-ttu-id="706a7-142">Temps nécessaire à la demande de toosend de navigateur.</span><span class="sxs-lookup"><span data-stu-id="706a7-142">Time taken by browser toosend request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="706a7-143">Temps de chargement de la page de navigateur</span><span class="sxs-lookup"><span data-stu-id="706a7-143">Browser page load time</span></span> |<span data-ttu-id="706a7-144">Temps s’écoulant entre la demande de l’utilisateur et le chargement du DOM, des feuilles de style, des scripts et des images.</span><span class="sxs-lookup"><span data-stu-id="706a7-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="706a7-145">Mémoire disponible</span><span class="sxs-lookup"><span data-stu-id="706a7-145">Available memory</span></span> |<span data-ttu-id="706a7-146">Mémoire physique immédiatement disponible pour un processus ou pour une utilisation du système.</span><span class="sxs-lookup"><span data-stu-id="706a7-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="706a7-147">Taux d’E/S du processus</span><span class="sxs-lookup"><span data-stu-id="706a7-147">Process IO Rate</span></span> |<span data-ttu-id="706a7-148">Nombre total d’octets par seconde et toofiles écrite, réseau et périphériques.</span><span class="sxs-lookup"><span data-stu-id="706a7-148">Total bytes per second read and written toofiles, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="706a7-149">Taux d’exceptions</span><span class="sxs-lookup"><span data-stu-id="706a7-149">exception rate</span></span> |<span data-ttu-id="706a7-150">Exceptions levées par seconde.</span><span class="sxs-lookup"><span data-stu-id="706a7-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="706a7-151">Processeur de processus</span><span class="sxs-lookup"><span data-stu-id="706a7-151">Process CPU</span></span> |<span data-ttu-id="706a7-152">Hello pourcentage de temps de tous les threads de processus utilisé par les instructions tooexecution du processeur hello pour les processus des applications hello.</span><span class="sxs-lookup"><span data-stu-id="706a7-152">hello percentage of elapsed time of all process threads used by hello processor tooexecution instructions for hello applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="706a7-153">Temps processeur</span><span class="sxs-lookup"><span data-stu-id="706a7-153">Processor time</span></span> |<span data-ttu-id="706a7-154">pourcentage de Hello de temps qui hello processeur passe dans des threads non inactifs.</span><span class="sxs-lookup"><span data-stu-id="706a7-154">hello percentage of time that hello processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="706a7-155">Octets privés du processus</span><span class="sxs-lookup"><span data-stu-id="706a7-155">Process private bytes</span></span> |<span data-ttu-id="706a7-156">Mémoire exclusivement affectée toohello surveiller le processus de l’application.</span><span class="sxs-lookup"><span data-stu-id="706a7-156">Memory exclusively assigned toohello monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="706a7-157">Durée d’exécution de la demande ASP.NET</span><span class="sxs-lookup"><span data-stu-id="706a7-157">ASP.NET request execution time</span></span> |<span data-ttu-id="706a7-158">Durée d’exécution de la demande la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="706a7-158">Execution time of hello most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="706a7-159">Demandes ASP.NET en file d’attente d’exécution</span><span class="sxs-lookup"><span data-stu-id="706a7-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="706a7-160">Longueur de file d’attente de demandes d’application hello.</span><span class="sxs-lookup"><span data-stu-id="706a7-160">Length of hello application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="706a7-161">Taux de demandes ASP.NET</span><span class="sxs-lookup"><span data-stu-id="706a7-161">ASP.NET request rate</span></span> |<span data-ttu-id="706a7-162">Taux de toutes les demandes application toohello par seconde à partir de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="706a7-162">Rate of all requests toohello application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="706a7-163">Défaillances de dépendance</span><span class="sxs-lookup"><span data-stu-id="706a7-163">Dependency failures</span></span> |<span data-ttu-id="706a7-164">Nombre d’échecs des appels effectués par hello server application tooexternal des ressources.</span><span class="sxs-lookup"><span data-stu-id="706a7-164">Count of failed calls made by hello server application tooexternal resources.</span></span> |
| `request.duration` |<span data-ttu-id="706a7-165">Temps de réponse du serveur</span><span class="sxs-lookup"><span data-stu-id="706a7-165">Server response time</span></span> |<span data-ttu-id="706a7-166">Temps écoulé entre la réception d’une demande HTTP et la fin de l’envoi de réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="706a7-166">Time between receiving an HTTP request and finishing sending hello response.</span></span> |
| `request.rate` |<span data-ttu-id="706a7-167">Taux de demandes</span><span class="sxs-lookup"><span data-stu-id="706a7-167">Request rate</span></span> |<span data-ttu-id="706a7-168">Taux de toutes les demandes d’application toohello par seconde.</span><span class="sxs-lookup"><span data-stu-id="706a7-168">Rate of all requests toohello application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="706a7-169">Demandes ayant échoué</span><span class="sxs-lookup"><span data-stu-id="706a7-169">Failed requests</span></span> |<span data-ttu-id="706a7-170">Nombre de requêtes HTTP qui ont abouti au code de réponse > = 400</span><span class="sxs-lookup"><span data-stu-id="706a7-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="706a7-171">Affichages de page</span><span class="sxs-lookup"><span data-stu-id="706a7-171">Page views</span></span> |<span data-ttu-id="706a7-172">Nombre de demandes d’utilisateur client pour une page web.</span><span class="sxs-lookup"><span data-stu-id="706a7-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="706a7-173">Le trafic synthétique est filtré.</span><span class="sxs-lookup"><span data-stu-id="706a7-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="706a7-174">{nom de votre mesure personnalisée}</span><span class="sxs-lookup"><span data-stu-id="706a7-174">{your custom metric name}</span></span> |<span data-ttu-id="706a7-175">{nom de votre mesure}</span><span class="sxs-lookup"><span data-stu-id="706a7-175">{Your metric name}</span></span> |<span data-ttu-id="706a7-176">Votre valeur métrique signalés par [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) ou Bonjour [paramètre de mesures d’un appel de suivi](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="706a7-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in hello [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="706a7-177">métriques de Hello sont envoyés par les modules de télémétrie différents :</span><span class="sxs-lookup"><span data-stu-id="706a7-177">hello metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="706a7-178">Groupe de mesures</span><span class="sxs-lookup"><span data-stu-id="706a7-178">Metric group</span></span> | <span data-ttu-id="706a7-179">Module du collecteur</span><span class="sxs-lookup"><span data-stu-id="706a7-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="706a7-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="706a7-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="706a7-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="706a7-181">clientPerformance,</span></span><br/><span data-ttu-id="706a7-182">view</span><span class="sxs-lookup"><span data-stu-id="706a7-182">view</span></span> |[<span data-ttu-id="706a7-183">JavaScript du navigateur</span><span class="sxs-lookup"><span data-stu-id="706a7-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="706a7-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="706a7-184">performanceCounter</span></span> |[<span data-ttu-id="706a7-185">Performances</span><span class="sxs-lookup"><span data-stu-id="706a7-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="706a7-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="706a7-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="706a7-187">Dépendance</span><span class="sxs-lookup"><span data-stu-id="706a7-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="706a7-188">request,</span><span class="sxs-lookup"><span data-stu-id="706a7-188">request,</span></span><br/><span data-ttu-id="706a7-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="706a7-189">requestFailed</span></span> |[<span data-ttu-id="706a7-190">Demande serveur</span><span class="sxs-lookup"><span data-stu-id="706a7-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="706a7-191">Webhooks</span><span class="sxs-lookup"><span data-stu-id="706a7-191">Webhooks</span></span>
<span data-ttu-id="706a7-192">Vous pouvez [automatiser votre alerte tooan de réponse](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="706a7-192">You can [automate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="706a7-193">Azure appelle une adresse web de votre choix lorsqu’une alerte est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="706a7-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="706a7-194">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="706a7-194">See also</span></span>
* [<span data-ttu-id="706a7-195">Script tooconfigure Application Insights</span><span class="sxs-lookup"><span data-stu-id="706a7-195">Script tooconfigure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="706a7-196">Créer des ressources Application Insights et de test Web  templates à partir de modèles (en anglais)</span><span class="sxs-lookup"><span data-stu-id="706a7-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="706a7-197">Automatiser le couplage Insights tooApplication de Microsoft Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="706a7-197">Automate coupling Microsoft Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="706a7-198">Automatiser votre alerte tooan de réponse</span><span class="sxs-lookup"><span data-stu-id="706a7-198">Automate your response tooan alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
