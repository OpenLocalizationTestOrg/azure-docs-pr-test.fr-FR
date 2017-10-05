---
title: "Surveiller les opérations, les événements et les compteurs pour l’équilibrage de charge | Microsoft Docs"
description: "Découvrez comment activer la journalisation des événements d'alerte et de l'état des sondes d'intégrité pour l'équilibreur de charge Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 638ecd5e02889bd8cb6e7429dfcec335feaac4a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="c81a0-103">Analyse des journaux de l'équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="c81a0-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="c81a0-104">Vous pouvez utiliser différents types de journaux dans Azure pour gérer les équilibreurs de charge et résoudre les problèmes associés.</span><span class="sxs-lookup"><span data-stu-id="c81a0-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="c81a0-105">Certains de ces journaux sont accessibles via le portail.</span><span class="sxs-lookup"><span data-stu-id="c81a0-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="c81a0-106">Tous les journaux peuvent être extraits à partir d’un stockage Blob Azure et affichés dans différents outils, comme Excel et PowerBI.</span><span class="sxs-lookup"><span data-stu-id="c81a0-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="c81a0-107">Pour en savoir plus sur les différents types de journaux, consultez la liste ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c81a0-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="c81a0-108">**Journaux d’audit :** vous pouvez utiliser les [journaux d’audit Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anciennement journaux des opérations) pour afficher toutes les opérations soumises à votre ou vos abonnements Azure, ainsi que leur état.</span><span class="sxs-lookup"><span data-stu-id="c81a0-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="c81a0-109">Les journaux d’audit sont activés par défaut et peuvent être affichés dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c81a0-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="c81a0-110">**Journaux des événements d’alerte :** vous pouvez utiliser ce journal pour afficher les alertes générées par l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="c81a0-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="c81a0-111">L'état de l'équilibreur de charge est collecté toutes les cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="c81a0-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="c81a0-112">Ce journal est écrit uniquement si un événement d'alerte d’équilibreur de charge est généré.</span><span class="sxs-lookup"><span data-stu-id="c81a0-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="c81a0-113">**Journaux de sondes d’intégrité :** vous pouvez utiliser ce journal pour afficher les problèmes détectés par votre sonde d’intégrité, tels que le nombre d’instances dans votre pool principal qui ne reçoivent pas les demandes de l’équilibreur de charge en raison d’échecs de sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="c81a0-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="c81a0-114">Toute modification de l’état de la sonde d’intégrité est indiquée dans ce journal.</span><span class="sxs-lookup"><span data-stu-id="c81a0-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c81a0-115">L'analyse des journaux s’applique uniquement aux équilibreurs de charge accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="c81a0-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="c81a0-116">Les journaux ne sont disponibles que pour les ressources déployées avec le modèle de déploiement de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c81a0-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="c81a0-117">Vous ne pouvez pas les utiliser pour les ressources utilisant le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="c81a0-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="c81a0-118">Pour plus d’informations sur les modèles de déploiement, consultez [Présentation du déploiement Resource Manager et du déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c81a0-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="c81a0-119">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="c81a0-119">Enable logging</span></span>

<span data-ttu-id="c81a0-120">La journalisation d’audit est automatiquement activée pour chaque ressource Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c81a0-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="c81a0-121">Vous devez activer la journalisation des événements et des sondes d’intégrité pour commencer à collecter les données disponibles dans ces journaux.</span><span class="sxs-lookup"><span data-stu-id="c81a0-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="c81a0-122">Utilisez les étapes suivantes pour activer la journalisation.</span><span class="sxs-lookup"><span data-stu-id="c81a0-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="c81a0-123">Connectez-vous au [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c81a0-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="c81a0-124">Si vous ne disposez pas déjà d'un équilibreur de charge, [créez un équilibreur de charge](load-balancer-get-started-internet-arm-ps.md) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="c81a0-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="c81a0-125">Dans le portail, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="c81a0-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="c81a0-126">Sélectionnez **Équilibreurs de charge**.</span><span class="sxs-lookup"><span data-stu-id="c81a0-126">Select **Load Balancers**.</span></span>

    ![portail - équilibreur-charge](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="c81a0-128">Sélectionnez un équilibreur de charge existant >> **Tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="c81a0-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="c81a0-129">Sur le côté droit de la boîte de dialogue, sous le nom de l’équilibrage de charge, accédez à **Surveillance**, puis cliquez sur **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="c81a0-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![portail - paramètres-équilibreur-charge](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="c81a0-131">Dans le volet **Diagnostics**, sous **État**, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="c81a0-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="c81a0-132">Cliquez sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="c81a0-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="c81a0-133">Sous **LOGS**, sélectionnez un compte de stockage existant ou créez-en un nouveau.</span><span class="sxs-lookup"><span data-stu-id="c81a0-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="c81a0-134">Utilisez le curseur pour déterminer la durée en jours pendant laquelle les données d’événement sont stockées dans les journaux d’événements.</span><span class="sxs-lookup"><span data-stu-id="c81a0-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="c81a0-135">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="c81a0-135">Click **Save**.</span></span>

    ![Portail - Journaux de diagnostics](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="c81a0-137">Les journaux d’audit ne nécessitent pas de compte de stockage distinct.</span><span class="sxs-lookup"><span data-stu-id="c81a0-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="c81a0-138">L’utilisation du stockage pour la journalisation des événements et des sondes d’intégrité occasionnera des frais de service.</span><span class="sxs-lookup"><span data-stu-id="c81a0-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="c81a0-139">Journal d’audit</span><span class="sxs-lookup"><span data-stu-id="c81a0-139">Audit log</span></span>

<span data-ttu-id="c81a0-140">Le journal d’audit est généré par défaut.</span><span class="sxs-lookup"><span data-stu-id="c81a0-140">The audit log is generated by default.</span></span> <span data-ttu-id="c81a0-141">Les journaux sont conservés pendant 90 jours dans la banque de Journaux d’événements d’Azure.</span><span class="sxs-lookup"><span data-stu-id="c81a0-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="c81a0-142">Pour en savoir plus sur ces journaux, lisez l’article [Affichage des événements et des journaux d’audit](../monitoring-and-diagnostics/insights-debugging-with-events.md) .</span><span class="sxs-lookup"><span data-stu-id="c81a0-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="c81a0-143">Journal des événements d'alerte</span><span class="sxs-lookup"><span data-stu-id="c81a0-143">Alert event log</span></span>

<span data-ttu-id="c81a0-144">Ce journal n’est généré que si vous l’avez activé au niveau de chaque équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="c81a0-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="c81a0-145">Les événements sont journalisés au format JSON et stockés dans le compte de stockage spécifié lors de l’activation de la journalisation.</span><span class="sxs-lookup"><span data-stu-id="c81a0-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="c81a0-146">Vous trouverez ci-dessous un exemple d’événement.</span><span class="sxs-lookup"><span data-stu-id="c81a0-146">The following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="c81a0-147">La sortie JSON affiche la propriété *eventname* qui décrit la raison pour laquelle l'équilibreur de charge a créé une alerte.</span><span class="sxs-lookup"><span data-stu-id="c81a0-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="c81a0-148">Dans ce cas, l'alerte a été générée en raison de l'épuisement du port TCP à cause des limites de l’IP NAT source (SNAT).</span><span class="sxs-lookup"><span data-stu-id="c81a0-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="c81a0-149">Journal des sondes d’intégrité</span><span class="sxs-lookup"><span data-stu-id="c81a0-149">Health probe log</span></span>

<span data-ttu-id="c81a0-150">Ce journal n’est généré que si vous l’avez activé au niveau de chaque équilibreur de charge, comme détaillé ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c81a0-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="c81a0-151">Les données sont stockées dans le compte de stockage spécifié lors de l’activation de la journalisation.</span><span class="sxs-lookup"><span data-stu-id="c81a0-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="c81a0-152">Un conteneur nommé « insights-logs-loadbalancerprobehealthstatus » est créé et les données suivantes sont enregistrées :</span><span class="sxs-lookup"><span data-stu-id="c81a0-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="c81a0-153">La sortie JSON apparaît dans le champ des propriétés des informations de base pour l'état des sondes d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="c81a0-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="c81a0-154">La propriété *dipDownCount* indique le nombre total d'instances sur le serveur principal qui ne reçoivent pas le trafic réseau en raison d’une absence de réponse de la part de la sonde.</span><span class="sxs-lookup"><span data-stu-id="c81a0-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="c81a0-155">Afficher et analyser le journal d’audit</span><span class="sxs-lookup"><span data-stu-id="c81a0-155">View and analyze the audit log</span></span>

<span data-ttu-id="c81a0-156">Vous pouvez afficher et analyser les données du journal d’audit en utilisant l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c81a0-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="c81a0-157">**Outils Azure :** récupérez les informations à partir des journaux via Azure PowerShell, l’interface de ligne de commande Azure, l’API REST Azure ou le portail Azure en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="c81a0-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="c81a0-158">Des instructions détaillées pour chaque méthode sont détaillées dans l’article [Opérations d’audit avec Resource Manager](../azure-resource-manager/resource-group-audit.md) .</span><span class="sxs-lookup"><span data-stu-id="c81a0-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="c81a0-159">**Power BI :** si vous n’avez pas encore de compte [Power BI](https://powerbi.microsoft.com/pricing) , vous pouvez l’essayer gratuitement.</span><span class="sxs-lookup"><span data-stu-id="c81a0-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="c81a0-160">À l’aide du [pack de contenus des journaux d’audit Azure pour Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), vous pouvez analyser vos données avec des tableaux de bord préconfigurés ou personnaliser les vues selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="c81a0-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="c81a0-161">Afficher et analyser les journaux des sondes d’intégrité et des événements</span><span class="sxs-lookup"><span data-stu-id="c81a0-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="c81a0-162">Vous devez vous connecter à votre compte de stockage et récupérer les entrées de journal JSON pour les journaux des événements et des sondes d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="c81a0-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="c81a0-163">Une fois que vous avez téléchargé les fichiers JSON, vous pouvez les convertir en CSV et les afficher dans Excel, PowerBI ou tout autre outil de visualisation de données.</span><span class="sxs-lookup"><span data-stu-id="c81a0-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="c81a0-164">Si vous connaissez bien Visual Studio et les concepts de base de la modification des valeurs de constantes et variables en C#, vous pouvez utiliser les [outils de convertisseur de journaux](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponibles dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="c81a0-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c81a0-165">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c81a0-165">Additional resources</span></span>

* <span data-ttu-id="c81a0-166">[Visualiser vos journaux d’audit Azure avec Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c81a0-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="c81a0-167">[Afficher et analyser les journaux d’audit Azure dans Power BI et bien plus encore](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .</span><span class="sxs-lookup"><span data-stu-id="c81a0-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c81a0-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c81a0-168">Next steps</span></span>

[<span data-ttu-id="c81a0-169">Comprendre les sondes de l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c81a0-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
