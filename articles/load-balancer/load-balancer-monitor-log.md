---
title: "aaaMonitor opérations, les événements et les compteurs pour l’équilibrage de charge | Documents Microsoft"
description: "Découvrez comment tooenable les événements d’alerte et sonde d’enregistrement de l’état d’intégrité pour l’équilibrage de charge Azure"
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
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="3899d-103">Analyse des journaux de l'équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="3899d-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="3899d-104">Vous pouvez utiliser différents types de journaux dans Azure toomanage et résoudre les problèmes d’équilibreurs de charge.</span><span class="sxs-lookup"><span data-stu-id="3899d-104">You can use different types of logs in Azure toomanage and troubleshoot load balancers.</span></span> <span data-ttu-id="3899d-105">Certaines de ces journaux sont accessibles via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="3899d-105">Some of these logs can be accessed through hello portal.</span></span> <span data-ttu-id="3899d-106">Tous les journaux peuvent être extraits à partir d’un stockage Blob Azure et affichés dans différents outils, comme Excel et PowerBI.</span><span class="sxs-lookup"><span data-stu-id="3899d-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="3899d-107">Pour plus d’informations sur hello différents types de journaux à partir de la liste de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3899d-107">You can learn more about hello different types of logs from hello list below.</span></span>

* <span data-ttu-id="3899d-108">**Journaux d’audit :** que vous pouvez utiliser [les journaux d’Audit Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anciennement journaux opérationnels) tooview toutes les opérations en cours tooyour soumis un ou plusieurs abonnements Azure, ainsi que leur état.</span><span class="sxs-lookup"><span data-stu-id="3899d-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) tooview all operations being submitted tooyour Azure subscription(s), and their status.</span></span> <span data-ttu-id="3899d-109">Journaux d’audit sont activées par défaut et peuvent être consultées dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3899d-109">Audit logs are enabled by default, and can be viewed in hello Azure portal.</span></span>
* <span data-ttu-id="3899d-110">**Journaux des événements d’alerte :** vous pouvez utiliser cette rasied d’alertes de tooview journal par l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="3899d-110">**Alert event logs:** You can use this log tooview alerts rasied by hello load balancer.</span></span> <span data-ttu-id="3899d-111">état Hello pour l’équilibrage de charge hello est collecté toutes les cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="3899d-111">hello status for hello load balancer is collected every five minutes.</span></span> <span data-ttu-id="3899d-112">Ce journal est écrit uniquement si un événement d'alerte d’équilibreur de charge est généré.</span><span class="sxs-lookup"><span data-stu-id="3899d-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="3899d-113">**Journaux de sonde d’intégrité :** vous pouvez utiliser cette tooview des journaux des problèmes détectés par votre sonde d’intégrité, telles que nombre hello d’instances dans votre pool principal ne reçoivent pas les demandes d’équilibrage de charge hello en raison d’échecs de sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="3899d-113">**Health probe logs:** You can use this log tooview problems detected by your health probe, such as hello number of instances in your backend-pool that are not receiving requests from hello load balancer because of health probe failures.</span></span> <span data-ttu-id="3899d-114">Ce fichier journal est écrit toowhen un changement dans l’état d’intégrité sonde hello.</span><span class="sxs-lookup"><span data-stu-id="3899d-114">This log is written toowhen there is a change in hello health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3899d-115">L'analyse des journaux s’applique uniquement aux équilibreurs de charge accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="3899d-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="3899d-116">Les journaux sont uniquement disponibles pour les ressources déployées dans le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="3899d-116">Logs are only available for resources deployed in hello Resource Manager deployment model.</span></span> <span data-ttu-id="3899d-117">Vous ne pouvez pas utiliser les journaux pour les ressources dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="3899d-117">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="3899d-118">Pour plus d’informations sur les modèles de déploiement hello, consultez [déploiement du Gestionnaire de ressources de présentation et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3899d-118">For more information about hello deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="3899d-119">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="3899d-119">Enable logging</span></span>

<span data-ttu-id="3899d-120">La journalisation d’audit est automatiquement activée pour chaque ressource Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3899d-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="3899d-121">Vous devez les événements tooenable et toostart de journalisation de sonde d’intégrité collecte des données hello ces journaux.</span><span class="sxs-lookup"><span data-stu-id="3899d-121">You need tooenable event and health probe logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="3899d-122">Utilisez hello après la journalisation tooenable étapes.</span><span class="sxs-lookup"><span data-stu-id="3899d-122">Use hello following steps tooenable logging.</span></span>

<span data-ttu-id="3899d-123">Connectez-vous toohello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3899d-123">Sign-in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="3899d-124">Si vous ne disposez pas déjà d'un équilibreur de charge, [créez un équilibreur de charge](load-balancer-get-started-internet-arm-ps.md) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="3899d-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="3899d-125">Dans le portail de hello, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="3899d-125">In hello portal, click **Browse**.</span></span>
2. <span data-ttu-id="3899d-126">Sélectionnez **Équilibreurs de charge**.</span><span class="sxs-lookup"><span data-stu-id="3899d-126">Select **Load Balancers**.</span></span>

    ![portail - équilibreur-charge](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="3899d-128">Sélectionnez un équilibreur de charge existant >> **Tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="3899d-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="3899d-129">Hello droite de la boîte de dialogue hello sous nom hello d’équilibrage de charge hello, faites défiler trop**analyse**, cliquez sur **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="3899d-129">On hello right side of hello dialog under hello name of hello load balancer, scroll too**Monitoring**, click **Diagnostics**.</span></span>

    ![portail - paramètres-équilibreur-charge](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="3899d-131">Bonjour **Diagnostics** volet, sous **état**, sélectionnez **sur**.</span><span class="sxs-lookup"><span data-stu-id="3899d-131">In hello **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="3899d-132">Cliquez sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="3899d-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="3899d-133">Sous **LOGS**, sélectionnez un compte de stockage existant ou créez-en un nouveau.</span><span class="sxs-lookup"><span data-stu-id="3899d-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="3899d-134">Utilisez hello curseur toodetermine le nombre de jours des données d’événement sont stockés dans les journaux des événements hello.</span><span class="sxs-lookup"><span data-stu-id="3899d-134">Use hello slider toodetermine how many days worth of event data will be stored in hello event logs.</span></span> 
8. <span data-ttu-id="3899d-135">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3899d-135">Click **Save**.</span></span>

    ![Portail - Journaux de diagnostics](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="3899d-137">Les journaux d’audit ne nécessitent pas de compte de stockage distinct.</span><span class="sxs-lookup"><span data-stu-id="3899d-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="3899d-138">Hello d’utilisation du stockage pour les événements et d’intégrité sonde journalisation occasionnent des frais de service.</span><span class="sxs-lookup"><span data-stu-id="3899d-138">hello use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="3899d-139">Journal d’audit</span><span class="sxs-lookup"><span data-stu-id="3899d-139">Audit log</span></span>

<span data-ttu-id="3899d-140">journal d’audit de Hello est généré par défaut.</span><span class="sxs-lookup"><span data-stu-id="3899d-140">hello audit log is generated by default.</span></span> <span data-ttu-id="3899d-141">Hello journaux sont conservées pendant 90 jours dans le magasin de journaux des événements d’Azure.</span><span class="sxs-lookup"><span data-stu-id="3899d-141">hello logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="3899d-142">En savoir plus sur ces journaux en lisant hello [afficher les événements et journaux d’audit](../monitoring-and-diagnostics/insights-debugging-with-events.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="3899d-142">Learn more about these logs by reading hello [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="3899d-143">Journal des événements d'alerte</span><span class="sxs-lookup"><span data-stu-id="3899d-143">Alert event log</span></span>

<span data-ttu-id="3899d-144">Ce journal n’est généré que si vous l’avez activé au niveau de chaque équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="3899d-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="3899d-145">événements de Hello sont enregistrés au format JSON et stockées dans le compte de stockage hello que vous avez spécifié lorsque vous avez activé la journalisation hello.</span><span class="sxs-lookup"><span data-stu-id="3899d-145">hello events are logged in JSON format and stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="3899d-146">Hello Voici un exemple d’événement.</span><span class="sxs-lookup"><span data-stu-id="3899d-146">hello following is an example of an event.</span></span>

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

<span data-ttu-id="3899d-147">Hello JSON de sortie montre hello *eventname* propriété qui décrit la raison hello pour l’équilibrage de charge hello créé une alerte.</span><span class="sxs-lookup"><span data-stu-id="3899d-147">hello JSON output shows hello *eventname* property which will describe hello reason for hello load balancer created an alert.</span></span> <span data-ttu-id="3899d-148">Dans ce cas, alerte hello générée était due tooTCP épuisement du port fait source QU'IP NAT limite (SNAT).</span><span class="sxs-lookup"><span data-stu-id="3899d-148">In this case, hello alert generated was due tooTCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="3899d-149">Journal des sondes d’intégrité</span><span class="sxs-lookup"><span data-stu-id="3899d-149">Health probe log</span></span>

<span data-ttu-id="3899d-150">Ce journal n’est généré que si vous l’avez activé au niveau de chaque équilibreur de charge, comme détaillé ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3899d-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="3899d-151">les données de salutation sont stockées dans le compte de stockage hello que vous avez spécifié lorsque vous avez activé la journalisation hello.</span><span class="sxs-lookup"><span data-stu-id="3899d-151">hello data is stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="3899d-152">Un conteneur nommé « insights-journaux-loadbalancerprobehealthstatus » est créé et hello suivant des données est enregistré :</span><span class="sxs-lookup"><span data-stu-id="3899d-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and hello following data is logged:</span></span>

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

<span data-ttu-id="3899d-153">montre la sortie JSON Hello hello propriétés champ hello informations de base pour l’état d’intégrité de sonde hello.</span><span class="sxs-lookup"><span data-stu-id="3899d-153">hello JSON output shows in hello properties field hello basic information for hello probe health status.</span></span> <span data-ttu-id="3899d-154">Hello *dipDownCount* propriété indique le nombre total de hello d’instances sur hello principaux qui ne reçoivent pas de trafic réseau en raison de réponses de sonde toofailed.</span><span class="sxs-lookup"><span data-stu-id="3899d-154">hello *dipDownCount* property shows hello total number of instances on hello back-end which are not receiving network traffic due toofailed probe responses.</span></span>

## <a name="view-and-analyze-hello-audit-log"></a><span data-ttu-id="3899d-155">Afficher et analyser le journal d’audit de hello</span><span class="sxs-lookup"><span data-stu-id="3899d-155">View and analyze hello audit log</span></span>

<span data-ttu-id="3899d-156">Vous pouvez afficher et analyser les données du journal d’audit à l’aide d’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="3899d-156">You can view and analyze audit log data using any of hello following methods:</span></span>

* <span data-ttu-id="3899d-157">**Windows Azure tools :** récupère des informations à partir des journaux d’audit hello Azure PowerShell, hello Azure Interface de ligne de commande (CLI), hello API REST de Azure, ou hello portail Azure preview.</span><span class="sxs-lookup"><span data-stu-id="3899d-157">**Azure tools:** Retrieve information from hello audit logs through Azure PowerShell, hello Azure Command Line Interface (CLI), hello Azure REST API, or hello Azure preview portal.</span></span> <span data-ttu-id="3899d-158">Des instructions détaillées pour chaque méthode sont détaillées dans hello [opérations avec le Gestionnaire de ressources de l’Audit](../azure-resource-manager/resource-group-audit.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="3899d-158">Step-by-step instructions for each method are detailed in hello [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="3899d-159">**Power BI :** si vous n’avez pas encore de compte [Power BI](https://powerbi.microsoft.com/pricing) , vous pouvez l’essayer gratuitement.</span><span class="sxs-lookup"><span data-stu-id="3899d-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="3899d-160">À l’aide de hello [les journaux d’Audit Azure pack de contenu pour Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), vous pouvez analyser vos données avec des tableaux de bord préconfigurés, ou vous pouvez personnaliser les vues toosuit vos besoins.</span><span class="sxs-lookup"><span data-stu-id="3899d-160">Using hello [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views toosuit your requirements.</span></span>

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a><span data-ttu-id="3899d-161">Afficher et analyser le journal des événements et la sonde d’intégrité de hello</span><span class="sxs-lookup"><span data-stu-id="3899d-161">View and analyze hello health probe and event log</span></span>

<span data-ttu-id="3899d-162">Vous devez tooconnect tooyour stockage compte et récupérer les entrées de journal hello JSON pour les journaux de sonde d’intégrité et les événements.</span><span class="sxs-lookup"><span data-stu-id="3899d-162">You need tooconnect tooyour storage account and retrieve hello JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="3899d-163">Une fois que vous téléchargez des fichiers au format JSON hello, vous pouvez les convertir tooCSV et view dans Excel, Power BI ou tout autre outil de visualisation de données.</span><span class="sxs-lookup"><span data-stu-id="3899d-163">Once you download hello JSON files, you can convert them tooCSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="3899d-164">Si vous êtes familiarisé avec Visual Studio et les concepts de base de la modification des valeurs de constantes et variables dans c#, vous pouvez utiliser hello [ouvrir une session outils de convertisseur](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponible à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3899d-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3899d-165">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3899d-165">Additional resources</span></span>

* <span data-ttu-id="3899d-166">[Visualiser vos journaux d’audit Azure avec Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3899d-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="3899d-167">[Afficher et analyser les journaux d’audit Azure dans Power BI et bien plus encore](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .</span><span class="sxs-lookup"><span data-stu-id="3899d-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3899d-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3899d-168">Next steps</span></span>

[<span data-ttu-id="3899d-169">Comprendre les sondes de l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="3899d-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
