---
title: "aaaMonitor gestion des API avec l’Analyseur de Azure | Documents Microsoft"
description: "Découvrez comment toomonitor Azure API Management de service à l’aide du moniteur de Windows Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="71a28-103">Gestion des API avec Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="71a28-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="71a28-104">Azure Monitor est un nouveau service Azure qui fournit une source unique d’analyse pour toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="71a28-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="71a28-105">Dans le Gestionnaire d’Azure, vous pouvez visualiser, interroger, Router, archiver et prendre des mesures sur les métriques hello et journaux provenant des ressources Azure telles que la gestion de l’API.</span><span class="sxs-lookup"><span data-stu-id="71a28-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on hello metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="71a28-106">Hello suivant vidéo montre comment toomonitor gestion des API à l’aide du moniteur de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="71a28-106">hello following video shows how toomonitor API Management using Azure Monitor.</span></span> <span data-ttu-id="71a28-107">Pour en savoir plus sur Azure Monitor, consultez [Prise en main d’Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="71a28-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="71a28-108">Mesures</span><span class="sxs-lookup"><span data-stu-id="71a28-108">Metrics</span></span>
<span data-ttu-id="71a28-109">Gestion des API émet actuellement cinq métriques et nous prévoyons de tooadd plus Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="71a28-109">API Management currently emits five metrics and we plan tooadd more in hello future.</span></span> <span data-ttu-id="71a28-110">Ces mesures sont émis à chaque minute, pratiquement visibilité en temps réel dans l’état de hello et l’intégrité de votre API.</span><span class="sxs-lookup"><span data-stu-id="71a28-110">These metrics are emitted every minute, giving you near real-time visibility into hello state and health of your APIs.</span></span> <span data-ttu-id="71a28-111">Voici un résumé des métriques de hello :</span><span class="sxs-lookup"><span data-stu-id="71a28-111">Following is a summary of hello metrics:</span></span>
* <span data-ttu-id="71a28-112">Nombre total de demandes de passerelle : nombre hello de l’API des demandes de période de hello.</span><span class="sxs-lookup"><span data-stu-id="71a28-112">Total Gateway Requests: hello number of API requests in hello period.</span></span> 
* <span data-ttu-id="71a28-113">Demandes réussies de passerelle : hello différentes demandes d’API qui a reçu des codes de réponse HTTP réussies, y compris 304, 307 et rien de plus petite que 301 (par exemple, 200).</span><span class="sxs-lookup"><span data-stu-id="71a28-113">Successful Gateway Requests: hello number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="71a28-114">Passerelle de demandes ayant échoué : le nombre de hello de demandes de l’API qui a reçu des codes de réponse HTTP erronés, y compris 400 et toute valeur supérieure à 500.</span><span class="sxs-lookup"><span data-stu-id="71a28-114">Failed Gateway Requests: hello number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="71a28-115">Demandes non autorisées de passerelle : nombre de hello de demandes d’API qui a reçu des codes de réponse HTTP, y compris 401 et 403 429.</span><span class="sxs-lookup"><span data-stu-id="71a28-115">Unauthorized Gateway Requests: hello number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="71a28-116">Autres demandes de passerelle : nombre de hello des demandes de l’API qui a reçu des codes de réponse HTTP qui n’appartiennent pas tooany Hello précédant les catégories (par exemple, 418).</span><span class="sxs-lookup"><span data-stu-id="71a28-116">Other Gateway Requests: hello number of API requests that received HTTP response codes that do not belong tooany of hello preceding categories (for example, 418).</span></span>

<span data-ttu-id="71a28-117">Vous pouvez accéder aux mesures dans votre service de gestion des API, ou accéder aux mesures de toutes vos ressources Azure dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="71a28-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="71a28-118">métriques de tooview dans votre service de gestion des API :</span><span class="sxs-lookup"><span data-stu-id="71a28-118">tooview metrics in your API Management service:</span></span>
1. <span data-ttu-id="71a28-119">Ouvrez hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="71a28-119">Open hello Azure portal.</span></span>
2. <span data-ttu-id="71a28-120">Atteindre le service de gestion des API tooyour.</span><span class="sxs-lookup"><span data-stu-id="71a28-120">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="71a28-121">Cliquez sur **Mesures**.</span><span class="sxs-lookup"><span data-stu-id="71a28-121">Click **Metrics**.</span></span>

![Panneau Mesures][metrics-blade]

<span data-ttu-id="71a28-123">Pour plus d’informations sur la façon toouse métriques, consultez [vue d’ensemble de mesures].</span><span class="sxs-lookup"><span data-stu-id="71a28-123">For more information about how toouse Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="71a28-124">Journaux d’activité</span><span class="sxs-lookup"><span data-stu-id="71a28-124">Activity Logs</span></span>
<span data-ttu-id="71a28-125">Journaux d’activité donnent une idée des opérations hello qui ont été effectuées sur les services de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="71a28-125">Activity logs provide insight into hello operations that were performed on your API Management services.</span></span> <span data-ttu-id="71a28-126">Ils étaient auparavant nommés « Journaux d’audit » ou « Journaux des opérations ».</span><span class="sxs-lookup"><span data-stu-id="71a28-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="71a28-127">À l’aide des journaux d’activité, vous pouvez déterminer hello », qui et à quel moment » pour toutes les opérations (PUT, POST, DELETE) effectuées sur votre service de gestion des API d’écriture.</span><span class="sxs-lookup"><span data-stu-id="71a28-127">Using activity logs, you can determine hello "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="71a28-128">Journaux d’activité n’incluent pas les opérations de lecture (GET) ou les opérations effectuées dans hello portail classique de serveur de publication ou à l’aide de hello des API de gestion d’origine.</span><span class="sxs-lookup"><span data-stu-id="71a28-128">Activity logs do not include read (GET) operations or operations performed in hello classic Publisher Portal or using hello original Management APIs.</span></span>

<span data-ttu-id="71a28-129">Vous pouvez accéder aux journaux d’activité dans votre service de Gestion des API, ou accéder aux journaux de toutes vos ressources Azure dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="71a28-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="71a28-130">tooview activité enregistre dans votre service de gestion des API :</span><span class="sxs-lookup"><span data-stu-id="71a28-130">tooview activity logs in your API Management service:</span></span>
1. <span data-ttu-id="71a28-131">Ouvrez hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="71a28-131">Open hello Azure portal.</span></span>
2. <span data-ttu-id="71a28-132">Atteindre le service de gestion des API tooyour.</span><span class="sxs-lookup"><span data-stu-id="71a28-132">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="71a28-133">Cliquez sur **Journal d’activité**.</span><span class="sxs-lookup"><span data-stu-id="71a28-133">Click **Activity log**.</span></span>

![Panneau Journaux d’activité][activity-logs-blade]

<span data-ttu-id="71a28-135">Pour plus d’informations sur la façon toouse métriques, consultez [vue d’ensemble des journaux d’activité].</span><span class="sxs-lookup"><span data-stu-id="71a28-135">For more information about how toouse Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="71a28-136">Alertes</span><span class="sxs-lookup"><span data-stu-id="71a28-136">Alerts</span></span>
<span data-ttu-id="71a28-137">Vous pouvez configurer des alertes tooreceive basés sur les journaux d’activité et de métriques.</span><span class="sxs-lookup"><span data-stu-id="71a28-137">You can configure tooreceive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="71a28-138">Moniteur de Azure vous permet de tooconfigure un hello toodo alerte suivant lorsqu’il déclenche :</span><span class="sxs-lookup"><span data-stu-id="71a28-138">Azure Monitor allows you tooconfigure an alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="71a28-139">Envoyer un e-mail de notification</span><span class="sxs-lookup"><span data-stu-id="71a28-139">Send an email notification</span></span>
* <span data-ttu-id="71a28-140">Appeler un webhook</span><span class="sxs-lookup"><span data-stu-id="71a28-140">Call a webhook</span></span>
* <span data-ttu-id="71a28-141">Appeler une application logique Azure</span><span class="sxs-lookup"><span data-stu-id="71a28-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="71a28-142">Vous pouvez configurer des règles d’alerte dans votre service de Gestion des API, ou dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="71a28-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="71a28-143">tooconfigure dans Gestion des API :</span><span class="sxs-lookup"><span data-stu-id="71a28-143">tooconfigure them in API Management:</span></span> 
1. <span data-ttu-id="71a28-144">Ouvrez hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="71a28-144">Open hello Azure portal.</span></span>
2. <span data-ttu-id="71a28-145">Atteindre le service de gestion des API tooyour.</span><span class="sxs-lookup"><span data-stu-id="71a28-145">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="71a28-146">Cliquez sur **Règles d'alerte**.</span><span class="sxs-lookup"><span data-stu-id="71a28-146">Click **Alert rules**.</span></span>

![Panneau Règles d’alerte][alert-rules-blade]

<span data-ttu-id="71a28-148">Pour plus d’informations sur l’utilisation des alertes, consultez [Présentation des alertes].</span><span class="sxs-lookup"><span data-stu-id="71a28-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="71a28-149">Journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="71a28-149">Diagnostic Logs</span></span>
<span data-ttu-id="71a28-150">Les journaux de diagnostic offrent des informations détaillées sur les opérations et erreurs qui sont importantes pour l’audit ainsi qu’à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="71a28-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="71a28-151">Les journaux de diagnostic diffèrent des journaux d’activité.</span><span class="sxs-lookup"><span data-stu-id="71a28-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="71a28-152">Journaux d’activité fournissent des informations sur les opérations de hello qui ont été effectuées sur vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="71a28-152">Activity logs provide insights into hello operations that were performed on your Azure resources.</span></span> <span data-ttu-id="71a28-153">Les journaux de diagnostic fournissent des informations sur les opérations effectuées par votre ressource.</span><span class="sxs-lookup"><span data-stu-id="71a28-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="71a28-154">Gestion des API fournit actuellement des tests de diagnostic des journaux (traités par lot toutes les heures) API individuel demander à chaque entrée ayant hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="71a28-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having hello following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="71a28-155">Vous pouvez accéder aux journaux de diagnostic dans votre service de Gestion des API, ou accéder aux journaux de toutes vos ressources Azure dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="71a28-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="71a28-156">tooview des journaux de diagnostic dans votre service de gestion des API :</span><span class="sxs-lookup"><span data-stu-id="71a28-156">tooview diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="71a28-157">Ouvrez hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="71a28-157">Open hello Azure portal.</span></span>
2. <span data-ttu-id="71a28-158">Atteindre le service de gestion des API tooyour.</span><span class="sxs-lookup"><span data-stu-id="71a28-158">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="71a28-159">Cliquez sur **Journal de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="71a28-159">Click **Diagnostic log**.</span></span>

![Panneau Journaux de diagnostic][diagnostic-logs-blade]

<span data-ttu-id="71a28-161">Pour plus d’informations sur la façon toouse métriques, consultez [vue d’ensemble des journaux de Diagnostic].</span><span class="sxs-lookup"><span data-stu-id="71a28-161">For more information about how toouse Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="71a28-162">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="71a28-162">Next Step</span></span>

* <span data-ttu-id="71a28-163">[Prise en main d’Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="71a28-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="71a28-164">[vue d’ensemble de mesures]</span><span class="sxs-lookup"><span data-stu-id="71a28-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="71a28-165">[vue d’ensemble des journaux d’activité]</span><span class="sxs-lookup"><span data-stu-id="71a28-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="71a28-166">[vue d’ensemble des journaux de Diagnostic]</span><span class="sxs-lookup"><span data-stu-id="71a28-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="71a28-167">[Présentation des alertes]</span><span class="sxs-lookup"><span data-stu-id="71a28-167">[Overview of Alerts]</span></span>

[Prise en main d’Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[vue d’ensemble de mesures]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[vue d’ensemble des journaux d’activité]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[vue d’ensemble des journaux de Diagnostic]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Présentation des alertes]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
