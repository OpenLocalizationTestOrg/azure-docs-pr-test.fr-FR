---
title: aaaMonitor Apps dans Azure App Service | Documents Microsoft
description: "Découvrez comment les applications toomonitor dans Azure App Service à l’aide de hello portail Azure."
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
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="46810-103">Surveillance des applications dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="46810-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="46810-104">[Service d’applications](http://go.microsoft.com/fwlink/?LinkId=529714) offre des fonctionnalités de surveillance intégrée dans hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="46810-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in hello [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="46810-105">Cela inclut les hello capacité tooreview **quotas** et **métriques** pour une application, ainsi que les hello plan App Service, configuration **alertes** et même **demiseàl’échelle** automatiquement en fonction de ces mesures.</span><span class="sxs-lookup"><span data-stu-id="46810-105">This includes hello ability tooreview **quotas** and **metrics** for an app as well as hello App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="46810-106">Présentation des quotas et des métriques</span><span class="sxs-lookup"><span data-stu-id="46810-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="46810-107">Quotas</span><span class="sxs-lookup"><span data-stu-id="46810-107">Quotas</span></span>
<span data-ttu-id="46810-108">Les applications hébergées dans le Service d’applications sont sujet toocertain *limites* sur les ressources qu’ils peuvent utiliser.</span><span class="sxs-lookup"><span data-stu-id="46810-108">Applications hosted in App Service are subject toocertain *limits* on the resources they can use.</span></span> <span data-ttu-id="46810-109">Hello limites sont définies par hello **plan App Service** associé application hello.</span><span class="sxs-lookup"><span data-stu-id="46810-109">hello limits are defined by hello **App Service plan** associated with hello app.</span></span>

<span data-ttu-id="46810-110">Si l’application hello est hébergée dans un **libre** ou **Shared** planifier, puis hello des limites sur les ressources hello hello application peut utiliser sont définies par **Quotas**.</span><span class="sxs-lookup"><span data-stu-id="46810-110">If hello application is hosted in a **Free** or **Shared** plan, then hello limits on hello resources hello app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="46810-111">Si l’application hello est hébergée dans un **base**, **Standard** ou **Premium** planifier, puis les limites de hello sur ils peuvent utiliser des ressources hello sont définies par hello **taille** (Petite, moyenne, grande) et **le nombre d’instances** (1, 2, 3,...) de hello **plan App Service**.</span><span class="sxs-lookup"><span data-stu-id="46810-111">If hello application is hosted in a **Basic**, **Standard** or **Premium** plan, then hello limits on hello resources they can use are set by hello **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of hello **App Service plan**.</span></span>

<span data-ttu-id="46810-112">Les **quotas** des applications **gratuites** ou **partagées** sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="46810-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="46810-113">**CPU(short)**</span><span class="sxs-lookup"><span data-stu-id="46810-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="46810-114">Quantité d’UC autorisée pour cette application dans un intervalle de cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="46810-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="46810-115">Ce quota se réinitialise toutes les cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="46810-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="46810-116">**CPU(Day)**</span><span class="sxs-lookup"><span data-stu-id="46810-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="46810-117">Quantité totale d’UC autorisée pour cette application sur une journée.</span><span class="sxs-lookup"><span data-stu-id="46810-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="46810-118">Ce quota se réinitialise toutes les 24 heures à minuit en temps universel coordonné.</span><span class="sxs-lookup"><span data-stu-id="46810-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="46810-119">**Mémoire**</span><span class="sxs-lookup"><span data-stu-id="46810-119">**Memory**</span></span>
  * <span data-ttu-id="46810-120">Quantité totale de mémoire autorisée pour cette application.</span><span class="sxs-lookup"><span data-stu-id="46810-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="46810-121">**Bande passante**</span><span class="sxs-lookup"><span data-stu-id="46810-121">**Bandwidth**</span></span>
  * <span data-ttu-id="46810-122">Quantité totale de bande passante sortante autorisée pour cette application sur une journée.</span><span class="sxs-lookup"><span data-stu-id="46810-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="46810-123">Ce quota se réinitialise toutes les 24 heures à minuit en temps universel coordonné.</span><span class="sxs-lookup"><span data-stu-id="46810-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="46810-124">**Système de fichiers**</span><span class="sxs-lookup"><span data-stu-id="46810-124">**Filesystem**</span></span>
  * <span data-ttu-id="46810-125">Quantité totale de stockage autorisée.</span><span class="sxs-lookup"><span data-stu-id="46810-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="46810-126">Hello uniquement quota applicable tooapps hébergé sur **base**, **Standard** et **Premium** plans est **système de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="46810-126">hello only quota applicable tooapps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="46810-127">Trouverez ici plus d’informations sur les fonctionnalités disponibles pour hello références (SKU) du Service d’application différents, les limites et quotas spécifiques de hello : [limites de Service d’abonnement Azure](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="46810-127">More information about hello specific quotas, limits and features available to hello different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="46810-128">Application de quotas</span><span class="sxs-lookup"><span data-stu-id="46810-128">Quota Enforcement</span></span>
<span data-ttu-id="46810-129">Si une application dans son utilisation dépasse hello **processeur (en bref)**, **UC (jour)**, ou **la bande passante** quota puis hello application s’arrête jusqu'à ce que le quota de hello définit nouveau.</span><span class="sxs-lookup"><span data-stu-id="46810-129">If an application in its usage exceeds hello **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then hello application will be stopped until hello quota re-sets.</span></span> <span data-ttu-id="46810-130">Pendant ce laps de temps, toutes les requêtes entrantes donneront lieu à une erreur **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="46810-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="46810-131">Si hello application **mémoire** quota est dépassé, l’application hello sera redémarrage.</span><span class="sxs-lookup"><span data-stu-id="46810-131">If hello application **memory** quota is exceeded, then hello application will be re-started.</span></span>

<span data-ttu-id="46810-132">Si hello **Filesystem** quota est dépassé, puis toute écriture échoue, cela inclut l’écriture toologs.</span><span class="sxs-lookup"><span data-stu-id="46810-132">If hello **Filesystem** quota is exceeded, then any write operation will fail, this includes writing toologs.</span></span>

<span data-ttu-id="46810-133">Vous pouvez augmenter ou supprimer les quotas de votre application en procédant à la mise à niveau de votre plan App Service.</span><span class="sxs-lookup"><span data-stu-id="46810-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="46810-134">Mesures</span><span class="sxs-lookup"><span data-stu-id="46810-134">Metrics</span></span>
<span data-ttu-id="46810-135">**Métriques** fournissent des informations sur l’application hello, ou le comportement du plan App Service.</span><span class="sxs-lookup"><span data-stu-id="46810-135">**Metrics** provide information about hello app, or App Service plan's behavior.</span></span>

<span data-ttu-id="46810-136">Pour un **Application**, hello les métriques disponibles sont :</span><span class="sxs-lookup"><span data-stu-id="46810-136">For an **Application**, hello available metrics are:</span></span>

* <span data-ttu-id="46810-137">**Temps de réponse moyen**</span><span class="sxs-lookup"><span data-stu-id="46810-137">**Average Response Time**</span></span>
  * <span data-ttu-id="46810-138">temps moyen de Hello nécessaire pour les demandes de tooserve application hello en ms.</span><span class="sxs-lookup"><span data-stu-id="46810-138">hello average time taken for hello app tooserve requests in ms.</span></span>
* <span data-ttu-id="46810-139">**Plage de travail moyenne de la mémoire**</span><span class="sxs-lookup"><span data-stu-id="46810-139">**Average memory working set**</span></span>
  * <span data-ttu-id="46810-140">durée moyenne de Hello de mémoire en MIB utilisé par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="46810-140">hello average amount of memory in MiBs used by hello app.</span></span>
* <span data-ttu-id="46810-141">**Temps processeur**</span><span class="sxs-lookup"><span data-stu-id="46810-141">**CPU Time**</span></span>
  * <span data-ttu-id="46810-142">quantité de Hello d’UC en secondes consommées par une application hello.</span><span class="sxs-lookup"><span data-stu-id="46810-142">hello amount of CPU in seconds consumed by hello app.</span></span> <span data-ttu-id="46810-143">Pour plus d’informations sur cette métrique, voir [Temps processeur et pourcentage UC](#cpu-time-vs-cpu-percentage).</span><span class="sxs-lookup"><span data-stu-id="46810-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="46810-144">**Données entrantes**</span><span class="sxs-lookup"><span data-stu-id="46810-144">**Data In**</span></span>
  * <span data-ttu-id="46810-145">Durée Hello consommée par l’application hello dans MIB de la bande passante entrante.</span><span class="sxs-lookup"><span data-stu-id="46810-145">hello amount of incoming bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="46810-146">**Données sortantes**</span><span class="sxs-lookup"><span data-stu-id="46810-146">**Data Out**</span></span>
  * <span data-ttu-id="46810-147">Durée Hello sortants de la bande passante consommée par l’application hello dans MIB.</span><span class="sxs-lookup"><span data-stu-id="46810-147">hello amount of outgoing bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="46810-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="46810-148">**Http 2xx**</span></span>
  * <span data-ttu-id="46810-149">Nombre de requêtes donnant lieu à un code d’état HTTP >= 200, mais < 300.</span><span class="sxs-lookup"><span data-stu-id="46810-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="46810-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="46810-150">**Http 3xx**</span></span>
  * <span data-ttu-id="46810-151">Nombre de requêtes donnant lieu à un code d’état HTTP >= 300, mais < 400.</span><span class="sxs-lookup"><span data-stu-id="46810-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="46810-152">**Http 401**</span><span class="sxs-lookup"><span data-stu-id="46810-152">**Http 401**</span></span>
  * <span data-ttu-id="46810-153">Nombre de requêtes donnant lieu à un code d’état HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="46810-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="46810-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="46810-154">**Http 403**</span></span>
  * <span data-ttu-id="46810-155">Nombre de requêtes donnant lieu à un code d’état HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="46810-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="46810-156">**Http 404**</span><span class="sxs-lookup"><span data-stu-id="46810-156">**Http 404**</span></span>
  * <span data-ttu-id="46810-157">Nombre de requêtes donnant lieu à un code d’état HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="46810-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="46810-158">**Http 406**</span><span class="sxs-lookup"><span data-stu-id="46810-158">**Http 406**</span></span>
  * <span data-ttu-id="46810-159">Nombre de requêtes donnant lieu à un code d’état HTTP 406.</span><span class="sxs-lookup"><span data-stu-id="46810-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="46810-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="46810-160">**Http 4xx**</span></span>
  * <span data-ttu-id="46810-161">Nombre de requêtes donnant lieu à un code d’état HTTP >= 400, mais < 500.</span><span class="sxs-lookup"><span data-stu-id="46810-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="46810-162">**Erreurs de serveur http**</span><span class="sxs-lookup"><span data-stu-id="46810-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="46810-163">Nombre de requêtes donnant lieu à un code d’état HTTP >= 500, mais < 600.</span><span class="sxs-lookup"><span data-stu-id="46810-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="46810-164">**Plage de travail de la mémoire**</span><span class="sxs-lookup"><span data-stu-id="46810-164">**Memory working set**</span></span>
  * <span data-ttu-id="46810-165">Quantité de mémoire actuellement utilisée par l’application hello dans MIB.</span><span class="sxs-lookup"><span data-stu-id="46810-165">Current amount of memory used by hello app in MiBs.</span></span>
* <span data-ttu-id="46810-166">**Demandes**</span><span class="sxs-lookup"><span data-stu-id="46810-166">**Requests**</span></span>
  * <span data-ttu-id="46810-167">Nombre total de requêtes, quel que soit leur code d’état HTTP résultant.</span><span class="sxs-lookup"><span data-stu-id="46810-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="46810-168">Pour un **plan App Service**, hello les métriques disponibles sont :</span><span class="sxs-lookup"><span data-stu-id="46810-168">For an **App Service plan**, hello available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="46810-169">Les métriques du plan App Service sont uniquement disponibles pour les plans des références (SKU) **De base**, **Standard** et **Premium**.</span><span class="sxs-lookup"><span data-stu-id="46810-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="46810-170">**Pourcentage UC**</span><span class="sxs-lookup"><span data-stu-id="46810-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="46810-171">Hello UC moyenne utilisée par toutes les instances du plan de hello.</span><span class="sxs-lookup"><span data-stu-id="46810-171">hello average CPU used across all instances of hello plan.</span></span>
* <span data-ttu-id="46810-172">**Pourcentage de mémoire**</span><span class="sxs-lookup"><span data-stu-id="46810-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="46810-173">Hello moyenne de la mémoire utilisée par toutes les instances du plan de hello.</span><span class="sxs-lookup"><span data-stu-id="46810-173">hello average memory used across all instances of hello plan.</span></span>
* <span data-ttu-id="46810-174">**Données entrantes**</span><span class="sxs-lookup"><span data-stu-id="46810-174">**Data In**</span></span>
  * <span data-ttu-id="46810-175">Hello entrants la bande passante moyenne utilisée par toutes les instances du plan de hello.</span><span class="sxs-lookup"><span data-stu-id="46810-175">hello average incoming bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="46810-176">**Données sortantes**</span><span class="sxs-lookup"><span data-stu-id="46810-176">**Data Out**</span></span>
  * <span data-ttu-id="46810-177">moyenne Hello sortant de la bande passante utilisée par toutes les instances du plan de hello.</span><span class="sxs-lookup"><span data-stu-id="46810-177">hello average outgoing bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="46810-178">**Longueur de file d'attente de disque**</span><span class="sxs-lookup"><span data-stu-id="46810-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="46810-179">Nombre moyen de Hello de lecture et d’écriture de requêtes qui ont été mises en attente sur le stockage.</span><span class="sxs-lookup"><span data-stu-id="46810-179">hello average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="46810-180">Une longueur de file d’attente du disque élevée est une indication d’une application qui peut ralentir en raison d’e/s de disque tooexcessive.</span><span class="sxs-lookup"><span data-stu-id="46810-180">A high disk queue length is an indication of an application that might be slowing down due tooexcessive disk I/O.</span></span>
* <span data-ttu-id="46810-181">**Longueur de la file d’attente HTTP**</span><span class="sxs-lookup"><span data-stu-id="46810-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="46810-182">Nombre moyen de Hello de requêtes HTTP que toosit sur la file d’attente hello avant la réalisation.</span><span class="sxs-lookup"><span data-stu-id="46810-182">hello average number of HTTP requests that had toosit on hello queue before being fulfilled.</span></span> <span data-ttu-id="46810-183">Une longueur de file d’attente HTTP élevée ou croissante est le symptôme d’un plan surchargé.</span><span class="sxs-lookup"><span data-stu-id="46810-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="46810-184">Temps processeur et pourcentage UC</span><span class="sxs-lookup"><span data-stu-id="46810-184">CPU time vs CPU percentage</span></span>
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="46810-185">2 métriques reflètent l’utilisation de l’UC :</span><span class="sxs-lookup"><span data-stu-id="46810-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="46810-186">**Temps processeur** et**Pourcentage UC**.</span><span class="sxs-lookup"><span data-stu-id="46810-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="46810-187">**Temps processeur** est utile pour les applications hébergées dans **libre** ou **Shared** plans, car l’un de leurs quotas est défini en minutes du processeur utilisées par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="46810-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by hello app.</span></span>

<span data-ttu-id="46810-188">**Pourcentage de processeur** sur hello autre part est utile pour les applications hébergées dans **base**, **standard** et **premium** plans, car ils la montée en puissance et cette mesure est une bonne indication de hello l’utilisation globale dans toutes les instances.</span><span class="sxs-lookup"><span data-stu-id="46810-188">**CPU percentage** on hello other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of hello overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="46810-189">Granularité des métriques et stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="46810-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="46810-190">Métriques pour un plan de service d’application et d’application sont enregistrés et agrégées par service hello avec hello suivant granularités et les stratégies de rétention :</span><span class="sxs-lookup"><span data-stu-id="46810-190">Metrics for an application and app service plan are logged and aggregated by hello service with hello following granularities and retention policies:</span></span>

* <span data-ttu-id="46810-191">Les métriques de granularité **Minute** sont conservées **48 heures**</span><span class="sxs-lookup"><span data-stu-id="46810-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="46810-192">Les métriques de granularité **Hour** sont conservées **30 jours**</span><span class="sxs-lookup"><span data-stu-id="46810-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="46810-193">Les métriques de granularité **Day** sont conservées **90 jours**</span><span class="sxs-lookup"><span data-stu-id="46810-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a><span data-ttu-id="46810-194">Surveillance des Quotas et des mesures hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="46810-194">Monitoring Quotas and Metrics in hello Azure Portal.</span></span>
<span data-ttu-id="46810-195">Vous pouvez consulter le statut hello Hello différents **quotas** et **métriques** affecter une application Bonjour [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="46810-195">You can review hello status of hello different **quotas** and **metrics** affecting an application in hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="46810-196">![][quotas]
Les **quotas** sont accessibles sous Paramètres &gt; **Quotas**.</span><span class="sxs-lookup"><span data-stu-id="46810-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="46810-197">Hello UX permet à examiner : nom de quotas hello (1), (2) l’intervalle de réinitialisation, (3) limite actuelle et sa (4) actuel valeur.</span><span class="sxs-lookup"><span data-stu-id="46810-197">hello UX allows you to review: (1) hello quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="46810-198">![][metrics]
**Mesures** sont accessibles directement depuis le panneau des ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="46810-198">![][metrics]
**Metrics** can be access directly from hello resource blade.</span></span> <span data-ttu-id="46810-199">Vous pouvez également personnaliser le graphique de hello par : (1) **cliquez sur** sur et sélectionnez (2) **modifier le graphique**.</span><span class="sxs-lookup"><span data-stu-id="46810-199">You can also customize hello chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="46810-200">À ce stade, vous pouvez modifier hello (3) **intervalle de temps**, (4) **type de graphique**et (5) **métriques** toodisplay.</span><span class="sxs-lookup"><span data-stu-id="46810-200">From here you can change hello (3) **time range**, (4) **chart type**, and (5) **metrics** toodisplay.</span></span>  

<span data-ttu-id="46810-201">Pour plus d’informations sur les métriques, voir [Surveiller les mesures de qualité du service](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="46810-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="46810-202">Alertes et mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="46810-202">Alerts and Autoscale</span></span>
<span data-ttu-id="46810-203">Métriques pour un plan de l’application ou le Service d’applications peut être rattachée tooalerts, toolearn plus d’informations, consultez [recevoir des notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="46810-203">Metrics for an App or App Service plan can be hooked up tooalerts, toolearn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="46810-204">Les applications App Service hébergées dans les plans App Service De base, Standard ou Premium prennent en charge la **mise à l’échelle automatique**.</span><span class="sxs-lookup"><span data-stu-id="46810-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="46810-205">Cela vous permet des règles tooconfigure que surveiller les métriques du plan App Service et peuvent augmenter ou diminuer le nombre d’instance hello en fournissant des ressources supplémentaires en fonction des besoins ou enregistrement money lors de l’application hello est excessive.</span><span class="sxs-lookup"><span data-stu-id="46810-205">This allows you tooconfigure rules that monitor the App Service plan metrics and can increase or decrease hello instance count providing additional resources as needed, or saving money when hello application is over-provision.</span></span> <span data-ttu-id="46810-206">Plus d’informations sur l’échelle automatique ici : [comment tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) et ici [meilleures pratiques pour l’échelle automatique du moniteur de Windows Azure](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="46810-206">You can learn more about auto scale here: [How tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="46810-207">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="46810-207">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="46810-208">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="46810-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="46810-209">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="46810-209">What's changed</span></span>
* <span data-ttu-id="46810-210">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="46810-210">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
