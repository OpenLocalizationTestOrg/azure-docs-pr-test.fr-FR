---
title: Surveiller les transactions B2B et configurer la journalisation - Azure Logic Apps | Microsoft Docs
description: "Surveiller les messages AS2, X12 et EDIFACT, démarrer la journalisation des diagnostics pour votre compte d’intégration"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f717dae9a70a96944b623f22b90cf8c5a943f382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="f9f09-103">Surveiller et configurer la journalisation des diagnostics pour la communication B2B dans des comptes d’intégration</span><span class="sxs-lookup"><span data-stu-id="f9f09-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="f9f09-104">Une fois la communication B2B configurée entre deux processus ou applications d’entreprise en cours d’exécution via votre compte d’intégration, ces entités peuvent échanger des messages entre elles.</span><span class="sxs-lookup"><span data-stu-id="f9f09-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="f9f09-105">Pour vérifier que cette communication fonctionne comme prévu, vous pouvez configurer la surveillance des messages AS2, X12 et EDIFACT, ainsi que la journalisation des diagnostics pour votre compte d’intégration via le service [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-105">To confirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through the [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="f9f09-106">Ce service dans [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) surveille vos environnements cloud et local pour vous aider à maintenir leur disponibilité et leurs performances, et collecte des détails d’exécution et des événements pour un débogage enrichi.</span><span class="sxs-lookup"><span data-stu-id="f9f09-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="f9f09-107">Vous pouvez également [utiliser vos données de diagnostic avec d’autres services](#extend-diagnostic-data), tels que Stockage Azure et Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="f9f09-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="f9f09-108">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="f9f09-108">Requirements</span></span>

* <span data-ttu-id="f9f09-109">Une application logique configurée avec une journalisation des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f9f09-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="f9f09-110">Découvrez comment [configurer la journalisation pour cette application logique](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="f9f09-110">Learn [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="f9f09-111">Une fois cette condition remplie, vous devez disposer d’un espace de travail dans [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-111">After you've met this requirement, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="f9f09-112">Vous devez utiliser l’espace de travail OMS que vous avez utilisé quand vous avez configuré la journalisation pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="f9f09-112">You should use the same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="f9f09-113">Si vous n’avez pas d’espace de travail OMS, découvrez comment [créer un espace de travail OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-113">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="f9f09-114">Un compte d’intégration lié à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="f9f09-114">An integration account that's linked to your logic app.</span></span> <span data-ttu-id="f9f09-115">Découvrez comment [créer un compte d’intégration lié à votre application logique](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-115">Learn [how to create an integration account with a link to your logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="f9f09-116">Activer la journalisation des diagnostics pour votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="f9f09-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="f9f09-117">Vous pouvez activer la journalisation directement à partir de votre compte d’intégration ou [via le service Azure Monitor](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="f9f09-117">You can turn on logging either directly from your integration account or [through the Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="f9f09-118">Azure Monitor exerce une surveillance de base avec des données de niveau de l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f9f09-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="f9f09-119">En savoir plus sur [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="f9f09-120">Activer la journalisation des diagnostics directement à partir de votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="f9f09-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="f9f09-121">Dans le [portail Azure](https://portal.azure.com), recherchez et sélectionnez votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="f9f09-121">In the [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="f9f09-122">Sous **Surveillance**, choisissez **Journaux de diagnostic** comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="f9f09-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Rechercher et sélectionner votre compte d’intégration, choisissez « Journaux de diagnostic »](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="f9f09-124">Lorsque vous sélectionnez votre compte d’intégration, les valeurs suivantes sont automatiquement sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="f9f09-124">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="f9f09-125">Si ces valeurs sont correctes, choisissez **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="f9f09-126">Autrement, sélectionnez les valeurs souhaitées :</span><span class="sxs-lookup"><span data-stu-id="f9f09-126">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="f9f09-127">Sous **Abonnement**, sélectionnez l’abonnement Azure que vous utilisez avec votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="f9f09-127">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="f9f09-128">Sous **Groupe de ressources**, sélectionnez le groupe de ressources que vous utilisez avec votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="f9f09-128">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="f9f09-129">Sous **Type de ressource**, sélectionnez **Comptes d'intégration**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="f9f09-130">Sous **Ressource**, sélectionnez votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="f9f09-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="f9f09-131">Choisissez **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-131">Choose **Turn on diagnostics**.</span></span>

   ![Configurer les diagnostics pour votre compte d’intégration](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="f9f09-133">Sous **Paramètres de diagnostic**, puis **État**, choisissez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Activer Azure Diagnostics](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="f9f09-135">Sélectionner à présent l’espace de travail OMS et les données à utiliser pour la journalisation comme illustré :</span><span class="sxs-lookup"><span data-stu-id="f9f09-135">Now select the OMS workspace and data to use for logging as shown:</span></span>

   1. <span data-ttu-id="f9f09-136">Sélectionnez **Envoyer à Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-136">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="f9f09-137">Sous **Log Analytics**, choisissez **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="f9f09-138">Sous **Espaces de travail OMS**, sélectionnez l’espace de travail OMS à utiliser pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="f9f09-138">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="f9f09-139">Sous **Journal**, sélectionnez la catégorie **IntegrationAccountTrackingEvents**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-139">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="f9f09-140">Choisissez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-140">Choose **Save**.</span></span>

   ![Configurer Log Analytics pour pouvoir envoyer des données de diagnostic à un journal](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="f9f09-142">À présent, [configurez le suivi de vos messages B2B dans OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="f9f09-143">Activer la journalisation des diagnostics via Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="f9f09-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="f9f09-144">Dans le [portail Azure](https://portal.azure.com), dans le menu principal Azure, choisissez **Surveiller**, **Journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-144">In the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="f9f09-145">Sélectionnez ensuite votre compte d’intégration comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="f9f09-145">Then select your integration account as shown here:</span></span>

   ![Choisir « Surveiller », « Journaux de diagnostic », sélectionner votre compte d’intégration](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="f9f09-147">Lorsque vous sélectionnez votre compte d’intégration, les valeurs suivantes sont automatiquement sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="f9f09-147">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="f9f09-148">Si ces valeurs sont correctes, choisissez **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="f9f09-149">Autrement, sélectionnez les valeurs souhaitées :</span><span class="sxs-lookup"><span data-stu-id="f9f09-149">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="f9f09-150">Sous **Abonnement**, sélectionnez l’abonnement Azure que vous utilisez avec votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="f9f09-150">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="f9f09-151">Sous **Groupe de ressources**, sélectionnez le groupe de ressources que vous utilisez avec votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="f9f09-151">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="f9f09-152">Sous **Type de ressource**, sélectionnez **Comptes d'intégration**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="f9f09-153">Sous **Ressource**, sélectionnez votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="f9f09-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="f9f09-154">Choisissez **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-154">Choose **Turn on diagnostics**.</span></span>

   ![Configurer les diagnostics pour votre compte d’intégration](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="f9f09-156">Sous **Paramètres de diagnostic**, choisissez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Activer Azure Diagnostics](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="f9f09-158">Sélectionnez à présent l’espace de travail OMS et la catégorie d'événement pour la journalisation comme illustré :</span><span class="sxs-lookup"><span data-stu-id="f9f09-158">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="f9f09-159">Sélectionnez **Envoyer à Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-159">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="f9f09-160">Sous **Log Analytics**, choisissez **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="f9f09-161">Sous **Espaces de travail OMS**, sélectionnez l’espace de travail OMS à utiliser pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="f9f09-161">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="f9f09-162">Sous **Journal**, sélectionnez la catégorie **IntegrationAccountTrackingEvents**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-162">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="f9f09-163">Une fois ces opérations effectuées, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f9f09-163">When you're done, choose **Save**.</span></span>

   ![Configurer Log Analytics pour pouvoir envoyer des données de diagnostic à un journal](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="f9f09-165">À présent, [configurez le suivi de vos messages B2B dans OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="f9f09-166">Étendre la manière dont vous utilisez les données de diagnostic et l’emplacement où vous les utilisez avec d’autres services</span><span class="sxs-lookup"><span data-stu-id="f9f09-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="f9f09-167">Avec Azure Log Analytics, vous pouvez étendre le mode d’utilisation des données de diagnostic de votre application logique avec d’autres services Azure, par exemple :</span><span class="sxs-lookup"><span data-stu-id="f9f09-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="f9f09-168">Archivage des journaux de diagnostic Azure</span><span class="sxs-lookup"><span data-stu-id="f9f09-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="f9f09-169">Diffuser en continu les journaux de diagnostic vers Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f9f09-169">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="f9f09-170">Vous pouvez ensuite obtenir une surveillance en temps réel en utilisant les ressources de télémétrie et d’analyse d’autres services, tels que [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) et [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="f9f09-171">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f9f09-171">For example:</span></span>

* [<span data-ttu-id="f9f09-172">Diffuser les données d’Event Hubs vers Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f9f09-172">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="f9f09-173">Analyser les données de diffusion avec Stream Analytics et créer un tableau de bord analytique en temps réel dans Power BI</span><span class="sxs-lookup"><span data-stu-id="f9f09-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="f9f09-174">Selon les options que vous souhaitez configurer, veillez au préalable à [créer un compte de stockage Azure](../storage/common/storage-create-storage-account.md) ou à [créer un hub d’événements Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="f9f09-174">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="f9f09-175">Sélectionnez ensuite les options concernant l’emplacement où vous souhaitez envoyer les données de diagnostic :</span><span class="sxs-lookup"><span data-stu-id="f9f09-175">Then select the options for where you want to send diagnostic data:</span></span>

![Envoyer des données à un compte de stockage ou à un hub d’événements Azure](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="f9f09-177">Les périodes de rétention s’appliquent uniquement lorsque vous choisissez d’utiliser un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f9f09-177">Retention periods apply only when you choose to use a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="f9f09-178">Schémas de suivi pris en charge</span><span class="sxs-lookup"><span data-stu-id="f9f09-178">Supported tracking schemas</span></span>

<span data-ttu-id="f9f09-179">Azure prend en charge les types de schémas de suivi ci-dessous, qui ont tous des schémas fixes, à l’exception du type personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9f09-179">Azure supports these tracking schema types, which all have fixed schemas except the Custom type.</span></span>

* [<span data-ttu-id="f9f09-180">Schéma de suivi AS2</span><span class="sxs-lookup"><span data-stu-id="f9f09-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="f9f09-181">Schéma de suivi X12</span><span class="sxs-lookup"><span data-stu-id="f9f09-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="f9f09-182">Schéma de suivi personnalisé</span><span class="sxs-lookup"><span data-stu-id="f9f09-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="f9f09-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9f09-183">Next steps</span></span>

* [<span data-ttu-id="f9f09-184">Suivre les messages B2B dans OMS</span><span class="sxs-lookup"><span data-stu-id="f9f09-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Suivre les messages B2B dans OMS")
* [<span data-ttu-id="f9f09-185">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="f9f09-185">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack")

