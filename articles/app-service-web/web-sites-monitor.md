---
title: Analyser les application dans Azure App Service | Microsoft Docs
description: "Découvrez comment surveiller les applications dans Azure App Service à l’aide du Portail Azure."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 25d3776920d683fffedcd8ac6ed0e84dfe875974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="d7bc9-103">Surveillance des applications dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d7bc9-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="d7bc9-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) fournit des fonctionnalités de surveillance intégrées dans le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7bc9-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in the [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="d7bc9-105">Ces fonctionnalités comprennent notamment la possibilité d’examiner les **quotas** et les **métriques** d’une application et du plan App Service, la configuration **d’alertes**, et même une **mise à l’échelle** automatique en fonction de ces métriques.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-105">This includes the ability to review **quotas** and **metrics** for an app as well as the App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="d7bc9-106">Présentation des quotas et des métriques</span><span class="sxs-lookup"><span data-stu-id="d7bc9-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="d7bc9-107">Quotas</span><span class="sxs-lookup"><span data-stu-id="d7bc9-107">Quotas</span></span>
<span data-ttu-id="d7bc9-108">Les applications hébergées dans App Service sont soumises à certaines *limites* concernant les ressources qu’elles peuvent utiliser.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-108">Applications hosted in App Service are subject to certain *limits* on the resources they can use.</span></span> <span data-ttu-id="d7bc9-109">Ces limites sont définies par le **plan App Service** associé à l’application.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-109">The limits are defined by the **App Service plan** associated with the app.</span></span>

<span data-ttu-id="d7bc9-110">Si l’application est hébergée dans un plan **Gratuit** ou **Partagé**, les limites relatives aux ressources utilisables par l’application sont définies sous la forme de **quotas**.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-110">If the application is hosted in a **Free** or **Shared** plan, then the limits on the resources the app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="d7bc9-111">Si l’application est hébergée dans un plan **De base**, **Standard** ou **Premium**, les limites applicables aux ressources que l’application peut utiliser sont définies par la **taille** (Petite, Moyenne, Grande) et par le **nombre d’instances** (1, 2, 3, ...) du **plan App Service**.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-111">If the application is hosted in a **Basic**, **Standard** or **Premium** plan, then the limits on the resources they can use are set by the **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of the **App Service plan**.</span></span>

<span data-ttu-id="d7bc9-112">Les **quotas** des applications **gratuites** ou **partagées** sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="d7bc9-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="d7bc9-113">**CPU(short)**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="d7bc9-114">Quantité d’UC autorisée pour cette application dans un intervalle de cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="d7bc9-115">Ce quota se réinitialise toutes les cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="d7bc9-116">**CPU(Day)**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="d7bc9-117">Quantité totale d’UC autorisée pour cette application sur une journée.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="d7bc9-118">Ce quota se réinitialise toutes les 24 heures à minuit en temps universel coordonné.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="d7bc9-119">**Mémoire**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-119">**Memory**</span></span>
  * <span data-ttu-id="d7bc9-120">Quantité totale de mémoire autorisée pour cette application.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="d7bc9-121">**Bande passante**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-121">**Bandwidth**</span></span>
  * <span data-ttu-id="d7bc9-122">Quantité totale de bande passante sortante autorisée pour cette application sur une journée.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="d7bc9-123">Ce quota se réinitialise toutes les 24 heures à minuit en temps universel coordonné.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="d7bc9-124">**Système de fichiers**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-124">**Filesystem**</span></span>
  * <span data-ttu-id="d7bc9-125">Quantité totale de stockage autorisée.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="d7bc9-126">Le seul quota applicable aux applications hébergées sur les plans **De base**, **Standard** et **Premium** est **Système de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-126">The only quota applicable to apps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="d7bc9-127">Pour plus d’informations sur les quotas, limites et fonctionnalités spécifiques disponibles pour les différentes références (SKU) App Service, consultez [Limites du service d’abonnement Azure](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="d7bc9-127">More information about the specific quotas, limits and features available to the different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="d7bc9-128">Application de quotas</span><span class="sxs-lookup"><span data-stu-id="d7bc9-128">Quota Enforcement</span></span>
<span data-ttu-id="d7bc9-129">Si l’utilisation d’une application dépasse le quota **CPU (short)** (Temps processeur (jour)), **CPU (Day)** (Temps processeur (jour)) ou **Bande passante**, l’application sera arrêtée jusqu’à la réinitialisation du quota.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-129">If an application in its usage exceeds the **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then the application will be stopped until the quota re-sets.</span></span> <span data-ttu-id="d7bc9-130">Pendant ce laps de temps, toutes les requêtes entrantes donneront lieu à une erreur **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="d7bc9-131">Si le quota **Mémoire** d’une application est dépassé, l’application sera redémarrée.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-131">If the application **memory** quota is exceeded, then the application will be re-started.</span></span>

<span data-ttu-id="d7bc9-132">En cas de dépassement du quota **Système de fichiers** , toute opération d’écriture échouera, y compris l’écriture dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-132">If the **Filesystem** quota is exceeded, then any write operation will fail, this includes writing to logs.</span></span>

<span data-ttu-id="d7bc9-133">Vous pouvez augmenter ou supprimer les quotas de votre application en procédant à la mise à niveau de votre plan App Service.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="d7bc9-134">Mesures</span><span class="sxs-lookup"><span data-stu-id="d7bc9-134">Metrics</span></span>
<span data-ttu-id="d7bc9-135">**Mesures** fournissent des informations sur le comportement de l’application ou du plan App Service.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-135">**Metrics** provide information about the app, or App Service plan's behavior.</span></span>

<span data-ttu-id="d7bc9-136">Pour une **application**, les métriques disponibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7bc9-136">For an **Application**, the available metrics are:</span></span>

* <span data-ttu-id="d7bc9-137">**Temps de réponse moyen**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-137">**Average Response Time**</span></span>
  * <span data-ttu-id="d7bc9-138">Temps moyen, en millisecondes, nécessaire à l’application pour traiter les requêtes.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-138">The average time taken for the app to serve requests in ms.</span></span>
* <span data-ttu-id="d7bc9-139">**Plage de travail moyenne de la mémoire**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-139">**Average memory working set**</span></span>
  * <span data-ttu-id="d7bc9-140">Quantité moyenne de mémoire, en MiB, utilisée par l’application.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-140">The average amount of memory in MiBs used by the app.</span></span>
* <span data-ttu-id="d7bc9-141">**Temps processeur**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-141">**CPU Time**</span></span>
  * <span data-ttu-id="d7bc9-142">Quantité d’UC, en secondes, consommée par l’application.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-142">The amount of CPU in seconds consumed by the app.</span></span> <span data-ttu-id="d7bc9-143">Pour plus d’informations sur cette métrique, voir [Temps processeur et pourcentage UC](#cpu-time-vs-cpu-percentage).</span><span class="sxs-lookup"><span data-stu-id="d7bc9-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="d7bc9-144">**Données entrantes**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-144">**Data In**</span></span>
  * <span data-ttu-id="d7bc9-145">Quantité de bande passante entrante, en MiB, consommée par l’application.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-145">The amount of incoming bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="d7bc9-146">**Données sortantes**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-146">**Data Out**</span></span>
  * <span data-ttu-id="d7bc9-147">Quantité de bande passante sortante, en MiB, consommée par l’application.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-147">The amount of outgoing bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="d7bc9-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-148">**Http 2xx**</span></span>
  * <span data-ttu-id="d7bc9-149">Nombre de requêtes donnant lieu à un code d’état HTTP >= 200, mais < 300.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="d7bc9-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-150">**Http 3xx**</span></span>
  * <span data-ttu-id="d7bc9-151">Nombre de requêtes donnant lieu à un code d’état HTTP >= 300, mais < 400.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="d7bc9-152">**Http 401**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-152">**Http 401**</span></span>
  * <span data-ttu-id="d7bc9-153">Nombre de requêtes donnant lieu à un code d’état HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="d7bc9-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-154">**Http 403**</span></span>
  * <span data-ttu-id="d7bc9-155">Nombre de requêtes donnant lieu à un code d’état HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="d7bc9-156">**Http 404**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-156">**Http 404**</span></span>
  * <span data-ttu-id="d7bc9-157">Nombre de requêtes donnant lieu à un code d’état HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="d7bc9-158">**Http 406**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-158">**Http 406**</span></span>
  * <span data-ttu-id="d7bc9-159">Nombre de requêtes donnant lieu à un code d’état HTTP 406.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="d7bc9-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-160">**Http 4xx**</span></span>
  * <span data-ttu-id="d7bc9-161">Nombre de requêtes donnant lieu à un code d’état HTTP >= 400, mais < 500.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="d7bc9-162">**Erreurs de serveur http**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="d7bc9-163">Nombre de requêtes donnant lieu à un code d’état HTTP >= 500, mais < 600.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="d7bc9-164">**Plage de travail de la mémoire**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-164">**Memory working set**</span></span>
  * <span data-ttu-id="d7bc9-165">Quantité de mémoire actuelle, en MiB, utilisée par l’application.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-165">Current amount of memory used by the app in MiBs.</span></span>
* <span data-ttu-id="d7bc9-166">**Demandes**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-166">**Requests**</span></span>
  * <span data-ttu-id="d7bc9-167">Nombre total de requêtes, quel que soit leur code d’état HTTP résultant.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="d7bc9-168">Pour un **plan App Service**, les métriques disponibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7bc9-168">For an **App Service plan**, the available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="d7bc9-169">Les métriques du plan App Service sont uniquement disponibles pour les plans des références (SKU) **De base**, **Standard** et **Premium**.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="d7bc9-170">**Pourcentage UC**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="d7bc9-171">Utilisation moyenne de l’UC dans toutes les instances du plan.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-171">The average CPU used across all instances of the plan.</span></span>
* <span data-ttu-id="d7bc9-172">**Pourcentage de mémoire**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="d7bc9-173">Utilisation moyenne de la mémoire dans toutes les instances du plan.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-173">The average memory used across all instances of the plan.</span></span>
* <span data-ttu-id="d7bc9-174">**Données entrantes**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-174">**Data In**</span></span>
  * <span data-ttu-id="d7bc9-175">Utilisation moyenne de la bande passante entrante dans toutes les instances du plan.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-175">The average incoming bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="d7bc9-176">**Données sortantes**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-176">**Data Out**</span></span>
  * <span data-ttu-id="d7bc9-177">Utilisation moyenne de la bande passante sortante dans toutes les instances du plan.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-177">The average outgoing bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="d7bc9-178">**Longueur de file d'attente de disque**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="d7bc9-179">Nombre moyen de requêtes de lecture et d’écriture mises en file d’attente sur le stockage.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-179">The average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="d7bc9-180">Une longueur de file d’attente de disque élevée est une indication d’une application susceptible d’être ralentie en raison d’un nombre d’E/S de disque excessif.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-180">A high disk queue length is an indication of an application that might be slowing down due to excessive disk I/O.</span></span>
* <span data-ttu-id="d7bc9-181">**Longueur de la file d’attente HTTP**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="d7bc9-182">Nombre moyen de requêtes HTTP qui devaient se trouver dans la file d’attente avant d’être exécutées.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-182">The average number of HTTP requests that had to sit on the queue before being fulfilled.</span></span> <span data-ttu-id="d7bc9-183">Une longueur de file d’attente HTTP élevée ou croissante est le symptôme d’un plan surchargé.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="d7bc9-184">Temps processeur et pourcentage UC</span><span class="sxs-lookup"><span data-stu-id="d7bc9-184">CPU time vs CPU percentage</span></span>
<!-- To do: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="d7bc9-185">2 métriques reflètent l’utilisation de l’UC :</span><span class="sxs-lookup"><span data-stu-id="d7bc9-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="d7bc9-186">**Temps processeur** et**Pourcentage UC**.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="d7bc9-187">La métrique **Temps processeur** est utile pour les applications hébergées dans un plan **Gratuit** ou**Partagé**, car l’un des quotas de ces applications est défini en minutes d’UC utilisées par l’application.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by the app.</span></span>

<span data-ttu-id="d7bc9-188">D’un autre côté, la métrique **Pourcentage UC** est utile pour les applications hébergées dans les plans **De base**, **Standard** et **Premium**, car le nombre d’instances de ces applications peut être augmenté, et cette métrique est une bonne indication de l’utilisation globale dans toutes les instances.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-188">**CPU percentage** on the other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of the overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="d7bc9-189">Granularité des métriques et stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="d7bc9-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="d7bc9-190">Les métriques d’une application et d’un plan App Service sont journalisées et agrégées par le service avec les granularités et les stratégies de rétention suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7bc9-190">Metrics for an application and app service plan are logged and aggregated by the service with the following granularities and retention policies:</span></span>

* <span data-ttu-id="d7bc9-191">Les métriques de granularité **Minute** sont conservées **48 heures**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="d7bc9-192">Les métriques de granularité **Hour** sont conservées **30 jours**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="d7bc9-193">Les métriques de granularité **Day** sont conservées **90 jours**</span><span class="sxs-lookup"><span data-stu-id="d7bc9-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-the-azure-portal"></a><span data-ttu-id="d7bc9-194">Surveillance des quotas et des métriques dans le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d7bc9-194">Monitoring Quotas and Metrics in the Azure Portal.</span></span>
<span data-ttu-id="d7bc9-195">Vous pouvez examiner l’état des différents **quotas** et **métriques** en affectant une application dans le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7bc9-195">You can review the status of the different **quotas** and **metrics** affecting an application in the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="d7bc9-196">![][quotas]
Les **quotas** sont accessibles sous Paramètres > **Quotas**.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="d7bc9-197">L’expérience utilisateur vous permet de consulter : (1) le nom du quota, (2) son intervalle de réinitialisation, (3) sa limite actuelle et (4) sa valeur actuelle.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-197">The UX allows you to review: (1) the quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="d7bc9-198">![][metrics]
Les **mesures** sont directement accessibles à partir du panneau de ressources.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-198">![][metrics]
**Metrics** can be access directly from the resource blade.</span></span> <span data-ttu-id="d7bc9-199">Vous pouvez également personnaliser le graphique en : (1) **cliquant** sur ce dernier, puis en sélectionnant (2) **Modifier le graphique**.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-199">You can also customize the chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="d7bc9-200">À ce stade, vous pouvez modifier (3) **l’intervalle de temps**, (4) le **type de graphique** et (5) les **métriques** à afficher.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-200">From here you can change the (3) **time range**, (4) **chart type**, and (5) **metrics** to display.</span></span>  

<span data-ttu-id="d7bc9-201">Pour plus d’informations sur les métriques, voir [Surveiller les mesures de qualité du service](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="d7bc9-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="d7bc9-202">Alertes et mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="d7bc9-202">Alerts and Autoscale</span></span>
<span data-ttu-id="d7bc9-203">Les métriques d’une application ou d’un plan App Service peuvent être raccordées aux alertes. Pour plus d’informations, voir [Réception de notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="d7bc9-203">Metrics for an App or App Service plan can be hooked up to alerts, to learn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="d7bc9-204">Les applications App Service hébergées dans les plans App Service De base, Standard ou Premium prennent en charge la **mise à l’échelle automatique**.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="d7bc9-205">Cette fonctionnalité vous permet de configurer des règles qui surveillent les métriques du plan App Service et qui peuvent augmenter ou diminuer le nombre d’instances en fournissant les ressources supplémentaires requises ou en allégeant les coûts lorsque l’application est surapprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-205">This allows you to configure rules that monitor the App Service plan metrics and can increase or decrease the instance count providing additional resources as needed, or saving money when the application is over-provision.</span></span> <span data-ttu-id="d7bc9-206">Pour plus d’informations sur la mise à l’échelle automatique, voir [Mise à l’échelle](../monitoring-and-diagnostics/insights-how-to-scale.md) et [Meilleures pratiques pour la mise à l’échelle automatique d’Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="d7bc9-206">You can learn more about auto scale here: [How to Scale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="d7bc9-207">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-207">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d7bc9-208">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="d7bc9-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="d7bc9-209">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="d7bc9-209">What's changed</span></span>
* <span data-ttu-id="d7bc9-210">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d7bc9-210">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
