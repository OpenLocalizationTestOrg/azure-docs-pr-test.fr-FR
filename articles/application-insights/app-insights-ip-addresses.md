---
title: "Adresses IP utilisées par Application Insights | Microsoft Docs"
description: Exceptions de pare-feu de serveur requises par Application Insights
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 3bb076c63223fc1567c6b7b25c1a513bbc81ed58
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="ae846-103">Adresses IP utilisées par Application Insights</span><span class="sxs-lookup"><span data-stu-id="ae846-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="ae846-104">Le service [Azure Application Insights](app-insights-overview.md) utilise plusieurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="ae846-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="ae846-105">Vous devrez peut-être connaître ces adresses si l’application que vous surveillez est hébergée derrière un pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ae846-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="ae846-106">Bien que ces adresses soient statiques, il est possible que nous devions les modifier de temps à autre.</span><span class="sxs-lookup"><span data-stu-id="ae846-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="ae846-107">Ports sortants</span><span class="sxs-lookup"><span data-stu-id="ae846-107">Outgoing ports</span></span>
<span data-ttu-id="ae846-108">Vous devez ouvrir des ports sortants dans le pare-feu de votre serveur pour autoriser le Kit de développement logiciel (SDK) Application Insights et/ou Status Monitor à envoyer des données sur le portail :</span><span class="sxs-lookup"><span data-stu-id="ae846-108">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span></span>

| <span data-ttu-id="ae846-109">Objectif</span><span class="sxs-lookup"><span data-stu-id="ae846-109">Purpose</span></span> | <span data-ttu-id="ae846-110">URL</span><span class="sxs-lookup"><span data-stu-id="ae846-110">URL</span></span> | <span data-ttu-id="ae846-111">IP</span><span class="sxs-lookup"><span data-stu-id="ae846-111">IP</span></span> | <span data-ttu-id="ae846-112">Ports</span><span class="sxs-lookup"><span data-stu-id="ae846-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ae846-113">Télémétrie</span><span class="sxs-lookup"><span data-stu-id="ae846-113">Telemetry</span></span> |<span data-ttu-id="ae846-114">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="ae846-115">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="ae846-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="ae846-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="ae846-116">40.114.241.141</span></span><br/><span data-ttu-id="ae846-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="ae846-117">104.45.136.42</span></span><br/><span data-ttu-id="ae846-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="ae846-118">40.84.189.107</span></span><br/><span data-ttu-id="ae846-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="ae846-119">168.63.242.221</span></span><br/><span data-ttu-id="ae846-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="ae846-120">52.167.221.184</span></span><br/><span data-ttu-id="ae846-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="ae846-121">52.169.64.244</span></span> |<span data-ttu-id="ae846-122">443</span><span class="sxs-lookup"><span data-stu-id="ae846-122">443</span></span> |
| <span data-ttu-id="ae846-123">Live Metrics Stream (Flux continu de mesures)</span><span class="sxs-lookup"><span data-stu-id="ae846-123">Live Metrics Stream</span></span> |<span data-ttu-id="ae846-124">rt.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="ae846-125">rt.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="ae846-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="ae846-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="ae846-126">23.96.28.38</span></span><br/><span data-ttu-id="ae846-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="ae846-127">13.92.40.198</span></span> |<span data-ttu-id="ae846-128">443</span><span class="sxs-lookup"><span data-stu-id="ae846-128">443</span></span> |
| <span data-ttu-id="ae846-129">Télémétrie interne</span><span class="sxs-lookup"><span data-stu-id="ae846-129">Internal Telemetry</span></span> |<span data-ttu-id="ae846-130">breeze.aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="ae846-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="ae846-131">52.161.11.71</span></span> |<span data-ttu-id="ae846-132">443</span><span class="sxs-lookup"><span data-stu-id="ae846-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="ae846-133">Status Monitor</span><span class="sxs-lookup"><span data-stu-id="ae846-133">Status Monitor</span></span>
<span data-ttu-id="ae846-134">Configuration de Status Monitor (nécessaire uniquement pour apporter des modifications).</span><span class="sxs-lookup"><span data-stu-id="ae846-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="ae846-135">Objectif</span><span class="sxs-lookup"><span data-stu-id="ae846-135">Purpose</span></span> | <span data-ttu-id="ae846-136">URL</span><span class="sxs-lookup"><span data-stu-id="ae846-136">URL</span></span> | <span data-ttu-id="ae846-137">IP</span><span class="sxs-lookup"><span data-stu-id="ae846-137">IP</span></span> | <span data-ttu-id="ae846-138">Ports</span><span class="sxs-lookup"><span data-stu-id="ae846-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ae846-139">Configuration</span><span class="sxs-lookup"><span data-stu-id="ae846-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="ae846-140">Configuration</span><span class="sxs-lookup"><span data-stu-id="ae846-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="ae846-141">Configuration</span><span class="sxs-lookup"><span data-stu-id="ae846-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="ae846-142">Configuration</span><span class="sxs-lookup"><span data-stu-id="ae846-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="ae846-143">Configuration</span><span class="sxs-lookup"><span data-stu-id="ae846-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="ae846-144">Configuration</span><span class="sxs-lookup"><span data-stu-id="ae846-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="ae846-145">Configuration</span><span class="sxs-lookup"><span data-stu-id="ae846-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="ae846-146">Installation</span><span class="sxs-lookup"><span data-stu-id="ae846-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="ae846-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="ae846-147">HockeyApp</span></span>
| <span data-ttu-id="ae846-148">Objectif</span><span class="sxs-lookup"><span data-stu-id="ae846-148">Purpose</span></span> | <span data-ttu-id="ae846-149">URL</span><span class="sxs-lookup"><span data-stu-id="ae846-149">URL</span></span> | <span data-ttu-id="ae846-150">IP</span><span class="sxs-lookup"><span data-stu-id="ae846-150">IP</span></span> | <span data-ttu-id="ae846-151">Ports</span><span class="sxs-lookup"><span data-stu-id="ae846-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ae846-152">Données d’incident</span><span class="sxs-lookup"><span data-stu-id="ae846-152">Crash data</span></span> |<span data-ttu-id="ae846-153">gate.hockeyapp.net</span><span class="sxs-lookup"><span data-stu-id="ae846-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="ae846-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="ae846-154">104.45.136.42</span></span> |<span data-ttu-id="ae846-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="ae846-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="ae846-156">Tests de disponibilité</span><span class="sxs-lookup"><span data-stu-id="ae846-156">Availability tests</span></span>
<span data-ttu-id="ae846-157">Voici la liste des adresses à partir desquelles les [tests web de disponibilité](app-insights-monitor-web-app-availability.md) sont exécutés.</span><span class="sxs-lookup"><span data-stu-id="ae846-157">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="ae846-158">Si vous souhaitez exécuter des tests web sur votre application, mais que votre serveur web est limité au service de clients spécifiques, vous devrez alors autoriser le trafic entrant depuis nos serveurs de test de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="ae846-158">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="ae846-159">Ouvrez les ports 80 (http) et 443 (https) pour le trafic entrant à partir de ces adresses (les adresses IP sont regroupées par emplacement) :</span><span class="sxs-lookup"><span data-stu-id="ae846-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="ae846-160">API d’accès aux données</span><span class="sxs-lookup"><span data-stu-id="ae846-160">Data access API</span></span>
| <span data-ttu-id="ae846-161">Objectif</span><span class="sxs-lookup"><span data-stu-id="ae846-161">Purpose</span></span> | <span data-ttu-id="ae846-162">URI</span><span class="sxs-lookup"><span data-stu-id="ae846-162">URI</span></span> | <span data-ttu-id="ae846-163">IP</span><span class="sxs-lookup"><span data-stu-id="ae846-163">IP</span></span> | <span data-ttu-id="ae846-164">Ports</span><span class="sxs-lookup"><span data-stu-id="ae846-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ae846-165">API</span><span class="sxs-lookup"><span data-stu-id="ae846-165">API</span></span> |<span data-ttu-id="ae846-166">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="ae846-167">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="ae846-168">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="ae846-169">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="ae846-170">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="ae846-171">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="ae846-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="ae846-172">13.82.26.252</span></span><br/><span data-ttu-id="ae846-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="ae846-173">40.76.213.73</span></span> |<span data-ttu-id="ae846-174">80,443</span><span class="sxs-lookup"><span data-stu-id="ae846-174">80,443</span></span> |
| <span data-ttu-id="ae846-175">Documents API</span><span class="sxs-lookup"><span data-stu-id="ae846-175">API docs</span></span> |<span data-ttu-id="ae846-176">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="ae846-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="ae846-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="ae846-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="ae846-179">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="ae846-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="ae846-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="ae846-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="ae846-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="ae846-182">13.82.24.149</span></span><br/><span data-ttu-id="ae846-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="ae846-183">40.114.82.10</span></span> |<span data-ttu-id="ae846-184">80,443</span><span class="sxs-lookup"><span data-stu-id="ae846-184">80,443</span></span> |
| <span data-ttu-id="ae846-185">API interne</span><span class="sxs-lookup"><span data-stu-id="ae846-185">Internal API</span></span> |<span data-ttu-id="ae846-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="ae846-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="ae846-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="ae846-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="ae846-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="ae846-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="ae846-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="ae846-193">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-193">dynamic</span></span>|<span data-ttu-id="ae846-194">443</span><span class="sxs-lookup"><span data-stu-id="ae846-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="ae846-195">Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="ae846-195">Application Insights Analytics</span></span>

| <span data-ttu-id="ae846-196">Objectif</span><span class="sxs-lookup"><span data-stu-id="ae846-196">Purpose</span></span> | <span data-ttu-id="ae846-197">URI</span><span class="sxs-lookup"><span data-stu-id="ae846-197">URI</span></span> | <span data-ttu-id="ae846-198">IP</span><span class="sxs-lookup"><span data-stu-id="ae846-198">IP</span></span> | <span data-ttu-id="ae846-199">Ports</span><span class="sxs-lookup"><span data-stu-id="ae846-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ae846-200">Portail Analytics</span><span class="sxs-lookup"><span data-stu-id="ae846-200">Analytics Portal</span></span> | <span data-ttu-id="ae846-201">analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="ae846-202">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-202">dynamic</span></span> | <span data-ttu-id="ae846-203">80,443</span><span class="sxs-lookup"><span data-stu-id="ae846-203">80,443</span></span> |
| <span data-ttu-id="ae846-204">CDN</span><span class="sxs-lookup"><span data-stu-id="ae846-204">CDN</span></span> | <span data-ttu-id="ae846-205">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="ae846-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="ae846-206">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-206">dynamic</span></span> | <span data-ttu-id="ae846-207">80,443</span><span class="sxs-lookup"><span data-stu-id="ae846-207">80,443</span></span> |
| <span data-ttu-id="ae846-208">CDN multimédia</span><span class="sxs-lookup"><span data-stu-id="ae846-208">Media CDN</span></span> | <span data-ttu-id="ae846-209">applicationanalyticsmedia.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="ae846-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="ae846-210">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-210">dynamic</span></span> | <span data-ttu-id="ae846-211">80,443</span><span class="sxs-lookup"><span data-stu-id="ae846-211">80,443</span></span> |

<span data-ttu-id="ae846-212">Remarque : Le domaine *.applicationinsights.io appartient à l’équipe Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ae846-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="ae846-213">Extension du Portail Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="ae846-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="ae846-214">Objectif</span><span class="sxs-lookup"><span data-stu-id="ae846-214">Purpose</span></span> | <span data-ttu-id="ae846-215">URI</span><span class="sxs-lookup"><span data-stu-id="ae846-215">URI</span></span> | <span data-ttu-id="ae846-216">IP</span><span class="sxs-lookup"><span data-stu-id="ae846-216">IP</span></span> | <span data-ttu-id="ae846-217">Ports</span><span class="sxs-lookup"><span data-stu-id="ae846-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ae846-218">Extension Application Insights</span><span class="sxs-lookup"><span data-stu-id="ae846-218">Application Insights Extension</span></span> | <span data-ttu-id="ae846-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="ae846-220">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-220">dynamic</span></span> | <span data-ttu-id="ae846-221">80,443</span><span class="sxs-lookup"><span data-stu-id="ae846-221">80,443</span></span> |
| <span data-ttu-id="ae846-222">CDN de l’extension Application Insights</span><span class="sxs-lookup"><span data-stu-id="ae846-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="ae846-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="ae846-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="ae846-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="ae846-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ae846-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="ae846-226">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-226">dynamic</span></span> | <span data-ttu-id="ae846-227">80,443</span><span class="sxs-lookup"><span data-stu-id="ae846-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="ae846-228">SDK Application Insights</span><span class="sxs-lookup"><span data-stu-id="ae846-228">Application Insights SDKs</span></span>

| <span data-ttu-id="ae846-229">Objectif</span><span class="sxs-lookup"><span data-stu-id="ae846-229">Purpose</span></span> | <span data-ttu-id="ae846-230">URI</span><span class="sxs-lookup"><span data-stu-id="ae846-230">URI</span></span> | <span data-ttu-id="ae846-231">IP</span><span class="sxs-lookup"><span data-stu-id="ae846-231">IP</span></span> | <span data-ttu-id="ae846-232">Ports</span><span class="sxs-lookup"><span data-stu-id="ae846-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ae846-233">CDN du SDK JS Application Insights</span><span class="sxs-lookup"><span data-stu-id="ae846-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="ae846-234">az416426.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="ae846-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="ae846-235">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-235">dynamic</span></span> | <span data-ttu-id="ae846-236">80,443</span><span class="sxs-lookup"><span data-stu-id="ae846-236">80,443</span></span> |
| <span data-ttu-id="ae846-237">SDK Java Application Insights</span><span class="sxs-lookup"><span data-stu-id="ae846-237">Application Insights Java SDK</span></span> | <span data-ttu-id="ae846-238">aijavasdk.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ae846-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="ae846-239">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-239">dynamic</span></span> | <span data-ttu-id="ae846-240">80,443</span><span class="sxs-lookup"><span data-stu-id="ae846-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="ae846-241">Profileur</span><span class="sxs-lookup"><span data-stu-id="ae846-241">Profiler</span></span>

| <span data-ttu-id="ae846-242">Objectif</span><span class="sxs-lookup"><span data-stu-id="ae846-242">Purpose</span></span> | <span data-ttu-id="ae846-243">URI</span><span class="sxs-lookup"><span data-stu-id="ae846-243">URI</span></span> | <span data-ttu-id="ae846-244">IP</span><span class="sxs-lookup"><span data-stu-id="ae846-244">IP</span></span> | <span data-ttu-id="ae846-245">Ports</span><span class="sxs-lookup"><span data-stu-id="ae846-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ae846-246">Agent</span><span class="sxs-lookup"><span data-stu-id="ae846-246">Agent</span></span> | <span data-ttu-id="ae846-247">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="ae846-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="ae846-248">*.agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="ae846-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="ae846-249">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-249">dynamic</span></span> | <span data-ttu-id="ae846-250">443</span><span class="sxs-lookup"><span data-stu-id="ae846-250">443</span></span>
| <span data-ttu-id="ae846-251">Portail</span><span class="sxs-lookup"><span data-stu-id="ae846-251">Portal</span></span> | <span data-ttu-id="ae846-252">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="ae846-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="ae846-253">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-253">dynamic</span></span> | <span data-ttu-id="ae846-254">443</span><span class="sxs-lookup"><span data-stu-id="ae846-254">443</span></span>
| <span data-ttu-id="ae846-255">Storage</span><span class="sxs-lookup"><span data-stu-id="ae846-255">Storage</span></span> | <span data-ttu-id="ae846-256">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ae846-256">*.core.windows.net</span></span> | <span data-ttu-id="ae846-257">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-257">dynamic</span></span> | <span data-ttu-id="ae846-258">443</span><span class="sxs-lookup"><span data-stu-id="ae846-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="ae846-259">Débogueur de capture instantanée</span><span class="sxs-lookup"><span data-stu-id="ae846-259">Snapshot Debugger</span></span>

| <span data-ttu-id="ae846-260">Objectif</span><span class="sxs-lookup"><span data-stu-id="ae846-260">Purpose</span></span> | <span data-ttu-id="ae846-261">URI</span><span class="sxs-lookup"><span data-stu-id="ae846-261">URI</span></span> | <span data-ttu-id="ae846-262">IP</span><span class="sxs-lookup"><span data-stu-id="ae846-262">IP</span></span> | <span data-ttu-id="ae846-263">Ports</span><span class="sxs-lookup"><span data-stu-id="ae846-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ae846-264">Agent</span><span class="sxs-lookup"><span data-stu-id="ae846-264">Agent</span></span> | <span data-ttu-id="ae846-265">ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="ae846-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="ae846-266">*.ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="ae846-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="ae846-267">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-267">dynamic</span></span> | <span data-ttu-id="ae846-268">443</span><span class="sxs-lookup"><span data-stu-id="ae846-268">443</span></span>
| <span data-ttu-id="ae846-269">Portail</span><span class="sxs-lookup"><span data-stu-id="ae846-269">Portal</span></span> | <span data-ttu-id="ae846-270">ppe.gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="ae846-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="ae846-271">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-271">dynamic</span></span> | <span data-ttu-id="ae846-272">443</span><span class="sxs-lookup"><span data-stu-id="ae846-272">443</span></span>
| <span data-ttu-id="ae846-273">Storage</span><span class="sxs-lookup"><span data-stu-id="ae846-273">Storage</span></span> | <span data-ttu-id="ae846-274">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ae846-274">*.core.windows.net</span></span> | <span data-ttu-id="ae846-275">dynamique</span><span class="sxs-lookup"><span data-stu-id="ae846-275">dynamic</span></span> | <span data-ttu-id="ae846-276">443</span><span class="sxs-lookup"><span data-stu-id="ae846-276">443</span></span>
