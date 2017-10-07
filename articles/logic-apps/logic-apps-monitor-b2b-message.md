---
title: les transactions aaaMonitor B2B et de journalisation - Azure Logic Apps | Documents Microsoft
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
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="3d995-103">Surveiller et configurer la journalisation des diagnostics pour la communication B2B dans des comptes d’intégration</span><span class="sxs-lookup"><span data-stu-id="3d995-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="3d995-104">Une fois la communication B2B configurée entre deux processus ou applications d’entreprise en cours d’exécution via votre compte d’intégration, ces entités peuvent échanger des messages entre elles.</span><span class="sxs-lookup"><span data-stu-id="3d995-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="3d995-105">tooconfirm cette communication fonctionne comme prévu, vous pouvez définir la surveillance pour AS2, X12, et les messages EDIFACT, ainsi que de la journalisation des diagnostics pour votre compte d’intégration via hello [Analytique de journal Azure](../log-analytics/log-analytics-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="3d995-105">tooconfirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="3d995-106">Ce service dans [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) surveille vos environnements cloud et local pour vous aider à maintenir leur disponibilité et leurs performances, et collecte des détails d’exécution et des événements pour un débogage enrichi.</span><span class="sxs-lookup"><span data-stu-id="3d995-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="3d995-107">Vous pouvez également [utiliser vos données de diagnostic avec d’autres services](#extend-diagnostic-data), tels que Stockage Azure et Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3d995-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="3d995-108">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="3d995-108">Requirements</span></span>

* <span data-ttu-id="3d995-109">Une application logique configurée avec une journalisation des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="3d995-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="3d995-110">En savoir plus [comment tooset configure une journalisation pour cette application logique](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="3d995-110">Learn [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="3d995-111">Une fois que vous avez répondu cette exigence, vous devez disposer d’un espace de travail Bonjour [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d995-111">After you've met this requirement, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="3d995-112">Vous devez utiliser hello même espace de travail OMS lorsque vous configurez la journalisation pour votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="3d995-112">You should use hello same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="3d995-113">Si vous n’avez pas un espace de travail OMS, Découvrez [comment toocreate un espace de travail OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3d995-113">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="3d995-114">Un compte d’intégration qui a lié tooyour logique application.</span><span class="sxs-lookup"><span data-stu-id="3d995-114">An integration account that's linked tooyour logic app.</span></span> <span data-ttu-id="3d995-115">En savoir plus [comment toocreate une intégration compte avec une application de la logique de lien tooyour](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="3d995-115">Learn [how toocreate an integration account with a link tooyour logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="3d995-116">Activer la journalisation des diagnostics pour votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="3d995-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="3d995-117">Vous pouvez activer la journalisation directement à partir de votre compte d’intégration ou [via hello service Azure moniteur](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="3d995-117">You can turn on logging either directly from your integration account or [through hello Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="3d995-118">Azure Monitor exerce une surveillance de base avec des données de niveau de l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="3d995-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="3d995-119">En savoir plus sur [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="3d995-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="3d995-120">Activer la journalisation des diagnostics directement à partir de votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="3d995-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="3d995-121">Bonjour [portail Azure](https://portal.azure.com), recherchez et sélectionnez votre compte de l’intégration.</span><span class="sxs-lookup"><span data-stu-id="3d995-121">In hello [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="3d995-122">Sous **Surveillance**, choisissez **Journaux de diagnostic** comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="3d995-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Rechercher et sélectionner votre compte d’intégration, choisissez « Journaux de diagnostic »](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="3d995-124">Une fois que vous sélectionnez votre compte d’intégration, hello valeurs suivantes est automatiquement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3d995-124">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="3d995-125">Si ces valeurs sont correctes, choisissez **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="3d995-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="3d995-126">Sinon, sélectionnez les valeurs hello que vous voulez :</span><span class="sxs-lookup"><span data-stu-id="3d995-126">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="3d995-127">Sous **abonnement**, sélectionnez hello abonnement Azure que vous utilisez avec votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="3d995-127">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="3d995-128">Sous **groupe de ressources**, sélectionnez groupe de ressources hello que vous utilisez avec votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="3d995-128">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="3d995-129">Sous **Type de ressource**, sélectionnez **Comptes d'intégration**.</span><span class="sxs-lookup"><span data-stu-id="3d995-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="3d995-130">Sous **Ressource**, sélectionnez votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="3d995-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="3d995-131">Choisissez **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="3d995-131">Choose **Turn on diagnostics**.</span></span>

   ![Configurer les diagnostics pour votre compte d’intégration](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="3d995-133">Sous **Paramètres de diagnostic**, puis **État**, choisissez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="3d995-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Activer Azure Diagnostics](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="3d995-135">Sélectionnez maintenant, hello OMS espace de travail et les données toouse pour la journalisation comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="3d995-135">Now select hello OMS workspace and data toouse for logging as shown:</span></span>

   1. <span data-ttu-id="3d995-136">Sélectionnez **envoyer tooLog Analytique**.</span><span class="sxs-lookup"><span data-stu-id="3d995-136">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="3d995-137">Sous **Log Analytics**, choisissez **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="3d995-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="3d995-138">Sous **espaces de travail OMS**, sélectionnez toouse d’espace de travail OMS hello pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="3d995-138">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="3d995-139">Sous **journal**, sélectionnez hello **IntegrationAccountTrackingEvents** catégorie.</span><span class="sxs-lookup"><span data-stu-id="3d995-139">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="3d995-140">Choisissez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3d995-140">Choose **Save**.</span></span>

   ![Configurer Analytique de journal et d’envoyer un journal de tooa de données de diagnostic](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="3d995-142">À présent, [configurez le suivi de vos messages B2B dans OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="3d995-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="3d995-143">Activer la journalisation des diagnostics via Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="3d995-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="3d995-144">Bonjour [portail Azure](https://portal.azure.com), on hello menu Azure principal, choisissez **moniteur**, **les journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="3d995-144">In hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="3d995-145">Sélectionnez ensuite votre compte d’intégration comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="3d995-145">Then select your integration account as shown here:</span></span>

   ![Choisir « Surveiller », « Journaux de diagnostic », sélectionner votre compte d’intégration](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="3d995-147">Une fois que vous sélectionnez votre compte d’intégration, hello valeurs suivantes est automatiquement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3d995-147">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="3d995-148">Si ces valeurs sont correctes, choisissez **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="3d995-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="3d995-149">Sinon, sélectionnez les valeurs hello que vous voulez :</span><span class="sxs-lookup"><span data-stu-id="3d995-149">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="3d995-150">Sous **abonnement**, sélectionnez hello abonnement Azure que vous utilisez avec votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="3d995-150">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="3d995-151">Sous **groupe de ressources**, sélectionnez groupe de ressources hello que vous utilisez avec votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="3d995-151">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="3d995-152">Sous **Type de ressource**, sélectionnez **Comptes d'intégration**.</span><span class="sxs-lookup"><span data-stu-id="3d995-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="3d995-153">Sous **Ressource**, sélectionnez votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="3d995-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="3d995-154">Choisissez **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="3d995-154">Choose **Turn on diagnostics**.</span></span>

   ![Configurer les diagnostics pour votre compte d’intégration](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="3d995-156">Sous **Paramètres de diagnostic**, choisissez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="3d995-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Activer Azure Diagnostics](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="3d995-158">Sélectionnez maintenant hello OMS espace de travail et les événements catégorie journalisation comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="3d995-158">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="3d995-159">Sélectionnez **envoyer tooLog Analytique**.</span><span class="sxs-lookup"><span data-stu-id="3d995-159">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="3d995-160">Sous **Log Analytics**, choisissez **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="3d995-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="3d995-161">Sous **espaces de travail OMS**, sélectionnez toouse d’espace de travail OMS hello pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="3d995-161">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="3d995-162">Sous **journal**, sélectionnez hello **IntegrationAccountTrackingEvents** catégorie.</span><span class="sxs-lookup"><span data-stu-id="3d995-162">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="3d995-163">Une fois ces opérations effectuées, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3d995-163">When you're done, choose **Save**.</span></span>

   ![Configurer Analytique de journal et d’envoyer un journal de tooa de données de diagnostic](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="3d995-165">À présent, [configurez le suivi de vos messages B2B dans OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="3d995-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="3d995-166">Étendre la manière dont vous utilisez les données de diagnostic et l’emplacement où vous les utilisez avec d’autres services</span><span class="sxs-lookup"><span data-stu-id="3d995-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="3d995-167">Avec Azure Log Analytics, vous pouvez étendre le mode d’utilisation des données de diagnostic de votre application logique avec d’autres services Azure, par exemple :</span><span class="sxs-lookup"><span data-stu-id="3d995-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="3d995-168">Archivage des journaux de diagnostic Azure</span><span class="sxs-lookup"><span data-stu-id="3d995-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="3d995-169">Flux de données des journaux de Diagnostics Azure tooAzure concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="3d995-169">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="3d995-170">Vous pouvez ensuite obtenir une surveillance en temps réel en utilisant les ressources de télémétrie et d’analyse d’autres services, tels que [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) et [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="3d995-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="3d995-171">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3d995-171">For example:</span></span>

* [<span data-ttu-id="3d995-172">Données de flux de données à partir de concentrateurs d’événements tooStream Analytique</span><span class="sxs-lookup"><span data-stu-id="3d995-172">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="3d995-173">Analyser les données de diffusion avec Stream Analytics et créer un tableau de bord analytique en temps réel dans Power BI</span><span class="sxs-lookup"><span data-stu-id="3d995-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="3d995-174">Selon les options de hello que vous voulez configurer, assurez-vous que vous première [créer un compte de stockage Azure](../storage/common/storage-create-storage-account.md) ou [créer un concentrateur d’événements Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="3d995-174">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="3d995-175">Puis sélectionnez les options de hello où vous souhaitez toosend les données de diagnostic :</span><span class="sxs-lookup"><span data-stu-id="3d995-175">Then select hello options for where you want toosend diagnostic data:</span></span>

![Envoyer des données tooAzure stockage compte ou événement un concentrateur](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="3d995-177">Périodes de rétention s’appliquent uniquement lorsque vous choisissez un compte de stockage toouse.</span><span class="sxs-lookup"><span data-stu-id="3d995-177">Retention periods apply only when you choose toouse a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="3d995-178">Schémas de suivi pris en charge</span><span class="sxs-lookup"><span data-stu-id="3d995-178">Supported tracking schemas</span></span>

<span data-ttu-id="3d995-179">Azure prend en charge ces types de schéma, qui ont des schémas, sauf le type personnalisé de hello fixes de suivi.</span><span class="sxs-lookup"><span data-stu-id="3d995-179">Azure supports these tracking schema types, which all have fixed schemas except hello Custom type.</span></span>

* [<span data-ttu-id="3d995-180">Schéma de suivi AS2</span><span class="sxs-lookup"><span data-stu-id="3d995-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="3d995-181">Schéma de suivi X12</span><span class="sxs-lookup"><span data-stu-id="3d995-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="3d995-182">Schéma de suivi personnalisé</span><span class="sxs-lookup"><span data-stu-id="3d995-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="3d995-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3d995-183">Next steps</span></span>

* [<span data-ttu-id="3d995-184">Suivre les messages B2B dans OMS</span><span class="sxs-lookup"><span data-stu-id="3d995-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Suivre les messages B2B dans OMS")
* [<span data-ttu-id="3d995-185">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="3d995-185">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")

