---
title: "Gestion des API avec Azure Monitor | Microsoft Docs"
description: "Découvrez comment surveiller votre service de Gestion des API Azure avec Azure Monitor."
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
ms.openlocfilehash: 0f64947755c79739bb6f15325929bd074cfd7210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="bd07b-103">Gestion des API avec Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="bd07b-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="bd07b-104">Azure Monitor est un nouveau service Azure qui fournit une source unique d’analyse pour toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="bd07b-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="bd07b-105">Avec Azure Monitor, vous pouvez visualiser, interroger, acheminer, archiver et agir sur les mesures et journaux provenant de vos ressources Azure, comme la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="bd07b-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="bd07b-106">La vidéo suivante montre comment surveiller la gestion des API à l’aide d’Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="bd07b-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="bd07b-107">Pour en savoir plus sur Azure Monitor, consultez [Prise en main d’Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="bd07b-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="bd07b-108">Mesures</span><span class="sxs-lookup"><span data-stu-id="bd07b-108">Metrics</span></span>
<span data-ttu-id="bd07b-109">La gestion des API émet actuellement cinq mesures et nous prévoyons d’en ajouter plus à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="bd07b-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="bd07b-110">Ces mesures sont émises chaque minute, pour une visibilité en quasi temps réel de l’intégrité de vos API.</span><span class="sxs-lookup"><span data-stu-id="bd07b-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="bd07b-111">Voici un résumé des mesures :</span><span class="sxs-lookup"><span data-stu-id="bd07b-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="bd07b-112">Nombre total de demandes de passerelle : le nombre de requêtes d’API dans la période.</span><span class="sxs-lookup"><span data-stu-id="bd07b-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="bd07b-113">Demandes de la passerelle ayant abouti : le nombre de requêtes d’API ayant reçu des codes de réponse HTTP de succès, dont 304, 307 et toute valeur inférieure à 301 (par exemple, 200).</span><span class="sxs-lookup"><span data-stu-id="bd07b-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="bd07b-114">Demandes de la passerelle ayant échoué : le nombre de requêtes d’API ayant reçu des codes de réponse HTTP d’échec, dont 400 et toute valeur supérieure à 500.</span><span class="sxs-lookup"><span data-stu-id="bd07b-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="bd07b-115">Demandes de la passerelle non autorisées : le nombre de requêtes d’API ayant reçu des codes de réponse HTTP comprenant 401, 403 et 429.</span><span class="sxs-lookup"><span data-stu-id="bd07b-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="bd07b-116">Autres demandes de la passerelle : le nombre de requêtes d’API ayant reçu des codes de réponse qui n’appartiennent à aucune des catégories précédentes (par exemple, 418).</span><span class="sxs-lookup"><span data-stu-id="bd07b-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="bd07b-117">Vous pouvez accéder aux mesures dans votre service de gestion des API, ou accéder aux mesures de toutes vos ressources Azure dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="bd07b-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="bd07b-118">Pour voir les mesures dans votre service de Gestion des API :</span><span class="sxs-lookup"><span data-stu-id="bd07b-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="bd07b-119">Ouvrez le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bd07b-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="bd07b-120">Allez à votre service de Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="bd07b-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="bd07b-121">Cliquez sur **Mesures**.</span><span class="sxs-lookup"><span data-stu-id="bd07b-121">Click **Metrics**.</span></span>

![Panneau Mesures][metrics-blade]

<span data-ttu-id="bd07b-123">Pour plus d’informations sur l’utilisation des mesures, consultez la [Présentation des mesures].</span><span class="sxs-lookup"><span data-stu-id="bd07b-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="bd07b-124">Journaux d’activité</span><span class="sxs-lookup"><span data-stu-id="bd07b-124">Activity Logs</span></span>
<span data-ttu-id="bd07b-125">Les journaux d’activité fournissent des informations sur les opérations qui ont été effectuées sur les services de Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="bd07b-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="bd07b-126">Ils étaient auparavant nommés « Journaux d’audit » ou « Journaux des opérations ».</span><span class="sxs-lookup"><span data-stu-id="bd07b-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="bd07b-127">Avec les journaux d’activité, vous pouvez déterminer « qui, quand et quoi » pour toutes les opérations d’écriture (PUT, POST, DELETE) sur vos services de Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="bd07b-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="bd07b-128">Les journaux d’activité n’incluent pas les opérations de lecture (GET) ou les opérations effectuées dans le portail des éditeurs classique ou utilisant les API de gestion d’origine.</span><span class="sxs-lookup"><span data-stu-id="bd07b-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="bd07b-129">Vous pouvez accéder aux journaux d’activité dans votre service de Gestion des API, ou accéder aux journaux de toutes vos ressources Azure dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="bd07b-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="bd07b-130">Pour afficher les journaux d’activité dans votre service de Gestion des API :</span><span class="sxs-lookup"><span data-stu-id="bd07b-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="bd07b-131">Ouvrez le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bd07b-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="bd07b-132">Allez à votre service de Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="bd07b-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="bd07b-133">Cliquez sur **Journal d’activité**.</span><span class="sxs-lookup"><span data-stu-id="bd07b-133">Click **Activity log**.</span></span>

![Panneau Journaux d’activité][activity-logs-blade]

<span data-ttu-id="bd07b-135">Pour plus d’informations sur l’utilisation des mesures, consultez la [Présentation des journaux d’activité].</span><span class="sxs-lookup"><span data-stu-id="bd07b-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="bd07b-136">Alertes</span><span class="sxs-lookup"><span data-stu-id="bd07b-136">Alerts</span></span>
<span data-ttu-id="bd07b-137">Vous pouvez configurer les paramètres pour recevoir des alertes en fonction des mesures et des journaux d’activité.</span><span class="sxs-lookup"><span data-stu-id="bd07b-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="bd07b-138">Azure Monitor vous permet de configurer une alerte pour effectuer les opérations suivantes lors de son déclenchement :</span><span class="sxs-lookup"><span data-stu-id="bd07b-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="bd07b-139">Envoyer un e-mail de notification</span><span class="sxs-lookup"><span data-stu-id="bd07b-139">Send an email notification</span></span>
* <span data-ttu-id="bd07b-140">Appeler un webhook</span><span class="sxs-lookup"><span data-stu-id="bd07b-140">Call a webhook</span></span>
* <span data-ttu-id="bd07b-141">Appeler une application logique Azure</span><span class="sxs-lookup"><span data-stu-id="bd07b-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="bd07b-142">Vous pouvez configurer des règles d’alerte dans votre service de Gestion des API, ou dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="bd07b-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="bd07b-143">Pour les configurer dans la Gestion des API :</span><span class="sxs-lookup"><span data-stu-id="bd07b-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="bd07b-144">Ouvrez le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bd07b-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="bd07b-145">Allez à votre service de Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="bd07b-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="bd07b-146">Cliquez sur **Règles d'alerte**.</span><span class="sxs-lookup"><span data-stu-id="bd07b-146">Click **Alert rules**.</span></span>

![Panneau Règles d’alerte][alert-rules-blade]

<span data-ttu-id="bd07b-148">Pour plus d’informations sur l’utilisation des alertes, consultez [Présentation des alertes].</span><span class="sxs-lookup"><span data-stu-id="bd07b-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="bd07b-149">Journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="bd07b-149">Diagnostic Logs</span></span>
<span data-ttu-id="bd07b-150">Les journaux de diagnostic offrent des informations détaillées sur les opérations et erreurs qui sont importantes pour l’audit ainsi qu’à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="bd07b-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="bd07b-151">Les journaux de diagnostic diffèrent des journaux d’activité.</span><span class="sxs-lookup"><span data-stu-id="bd07b-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="bd07b-152">Le journal d’activité fournit des informations sur les opérations qui ont été effectuées sur vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="bd07b-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="bd07b-153">Les journaux de diagnostic fournissent des informations sur les opérations effectuées par votre ressource.</span><span class="sxs-lookup"><span data-stu-id="bd07b-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="bd07b-154">La Gestion des API fournit actuellement des journaux de diagnostic (par lot toutes les heures) concernant chaque requête d’API. Chaque entrée a la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="bd07b-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

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

<span data-ttu-id="bd07b-155">Vous pouvez accéder aux journaux de diagnostic dans votre service de Gestion des API, ou accéder aux journaux de toutes vos ressources Azure dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="bd07b-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="bd07b-156">Pour afficher les journaux de diagnostic dans votre service de Gestion des API :</span><span class="sxs-lookup"><span data-stu-id="bd07b-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="bd07b-157">Ouvrez le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bd07b-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="bd07b-158">Allez à votre service de Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="bd07b-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="bd07b-159">Cliquez sur **Journal de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="bd07b-159">Click **Diagnostic log**.</span></span>

![Panneau Journaux de diagnostic][diagnostic-logs-blade]

<span data-ttu-id="bd07b-161">Pour plus d’informations sur l’utilisation des mesures, consultez la [Présentation des journaux de diagnostic].</span><span class="sxs-lookup"><span data-stu-id="bd07b-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="bd07b-162">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="bd07b-162">Next Step</span></span>

* <span data-ttu-id="bd07b-163">[Prise en main d’Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="bd07b-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="bd07b-164">[Présentation des mesures]</span><span class="sxs-lookup"><span data-stu-id="bd07b-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="bd07b-165">[Présentation des journaux d’activité]</span><span class="sxs-lookup"><span data-stu-id="bd07b-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="bd07b-166">[Présentation des journaux de diagnostic]</span><span class="sxs-lookup"><span data-stu-id="bd07b-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="bd07b-167">[Présentation des alertes]</span><span class="sxs-lookup"><span data-stu-id="bd07b-167">[Overview of Alerts]</span></span>

<span data-ttu-id="bd07b-168">[Prise en main d’Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span><span class="sxs-lookup"><span data-stu-id="bd07b-168">[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span></span>
<span data-ttu-id="bd07b-169">[Présentation des mesures]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span><span class="sxs-lookup"><span data-stu-id="bd07b-169">[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span></span>
<span data-ttu-id="bd07b-170">[Présentation des journaux d’activité]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span><span class="sxs-lookup"><span data-stu-id="bd07b-170">[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span></span>
<span data-ttu-id="bd07b-171">[Présentation des journaux de diagnostic]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span><span class="sxs-lookup"><span data-stu-id="bd07b-171">[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span></span>
<span data-ttu-id="bd07b-172">[Présentation des alertes]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span><span class="sxs-lookup"><span data-stu-id="bd07b-172">[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span></span>



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
