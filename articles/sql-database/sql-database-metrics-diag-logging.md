---
title: "Journalisation des métriques et diagnostics d’Azure SQL Database | Microsoft Docs"
description: "Découvrez comment configurer une ressource Azure SQL Database pour stocker les statistiques d’utilisation des ressources, de connectivité et d’exécution de requête."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: bf41aa530c68ea0e94a09d1dab63237c6f42bce7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="34e95-103">Journalisation des métriques et diagnostics d’Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="34e95-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="34e95-104">Azure SQL Database peut émettre des journaux de métriques et de diagnostics pour faciliter la surveillance.</span><span class="sxs-lookup"><span data-stu-id="34e95-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="34e95-105">Vous pouvez configurer Azure SQL Database pour stocker l’utilisation des ressources, les workers et sessions, ainsi que la connectivité dans l’une des ressources Azure suivantes :</span><span class="sxs-lookup"><span data-stu-id="34e95-105">You can configure Azure SQL Database to store resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="34e95-106">**Stockage Azure** : pour archiver des quantités importantes de données de télémétrie à un petit prix</span><span class="sxs-lookup"><span data-stu-id="34e95-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="34e95-107">**Azure Event Hub** : pour intégrer des données de télémétrie Azure SQL Database à votre solution de surveillance personnalisée ou à vos pipelines très actifs</span><span class="sxs-lookup"><span data-stu-id="34e95-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="34e95-108">**Azure Log Analytics** : pour une solution de surveillance prête à l’emploi avec des fonctionnalités de génération de rapports, d’alerte et d’atténuation</span><span class="sxs-lookup"><span data-stu-id="34e95-108">**Azure Log Analytics**: For out of the box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![architecture](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="34e95-110">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="34e95-110">Enable logging</span></span>

<span data-ttu-id="34e95-111">La journalisation des métriques et diagnostics n’est pas activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="34e95-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="34e95-112">Vous pouvez activer et gérer la journalisation des métriques et diagnostics à l’aide de l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="34e95-112">You can enable and manage metrics and diagnostics logging using one of the following methods:</span></span>
- <span data-ttu-id="34e95-113">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="34e95-113">Azure portal</span></span>
- <span data-ttu-id="34e95-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34e95-114">PowerShell</span></span>
- <span data-ttu-id="34e95-115">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="34e95-115">Azure CLI</span></span>
- <span data-ttu-id="34e95-116">API REST</span><span class="sxs-lookup"><span data-stu-id="34e95-116">REST API</span></span> 
- <span data-ttu-id="34e95-117">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="34e95-117">Resource Manager template</span></span>

<span data-ttu-id="34e95-118">Lorsque vous activez la journalisation des métriques et diagnostics, vous devez spécifier la ressource Azure dans laquelle les données sélectionnées sont collectées.</span><span class="sxs-lookup"><span data-stu-id="34e95-118">When you enable metrics and diagnostics logging, you need to specify the Azure resource where selected data is collected.</span></span> <span data-ttu-id="34e95-119">Options disponibles :</span><span class="sxs-lookup"><span data-stu-id="34e95-119">Options available:</span></span>
- <span data-ttu-id="34e95-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="34e95-120">Log analytics</span></span>
- <span data-ttu-id="34e95-121">Event Hub</span><span class="sxs-lookup"><span data-stu-id="34e95-121">Event Hub</span></span>
- <span data-ttu-id="34e95-122">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="34e95-122">Azure Storage</span></span> 

<span data-ttu-id="34e95-123">Vous pouvez approvisionner une nouvelle ressource Azure ou sélectionner une ressource existante.</span><span class="sxs-lookup"><span data-stu-id="34e95-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="34e95-124">Après avoir sélectionné la ressource de stockage, vous devez spécifier les données à collecter.</span><span class="sxs-lookup"><span data-stu-id="34e95-124">After selecting the storage resource, you need to specify which data to collect.</span></span> <span data-ttu-id="34e95-125">Les options disponibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="34e95-125">Options available include:</span></span>

- <span data-ttu-id="34e95-126">**[Métriques de 1 minute](sql-database-metrics-diag-logging.md#1-minute-metrics)**  : contient Pourcentage DTU, Limite DTU, Pourcentage UC, Pourcentage de lecture de données physiques, Pourcentage d’écriture du journal, Connexions réussies/en échec/bloquées par pare-feu, Pourcentage de sessions, Pourcentage de workers, Stockage, Pourcentage de stockage, Pourcentage de stockage XTP</span><span class="sxs-lookup"><span data-stu-id="34e95-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="34e95-127">Si vous spécifiez un compte Event Hub ou Stockage Azure, vous pouvez définir une stratégie de rétention pour spécifier que les données antérieures à un intervalle de temps sélectionné sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="34e95-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy to specify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="34e95-128">Si vous spécifiez Log Analytics, la stratégie de rétention dépend du niveau tarifaire sélectionné.</span><span class="sxs-lookup"><span data-stu-id="34e95-128">If you specify Log Analytics, the retention policy depends on the selected pricing tier.</span></span> <span data-ttu-id="34e95-129">Pour en savoir plus, voir [Tarification de Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="34e95-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="34e95-130">Pour comprendre non seulement comment activer la journalisation, mais aussi les métriques et les catégories de journaux prises en charge par les différents services Azure, nous vous recommandons de lire les articles [Vue d’ensemble des mesures dans Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) et [Présentation des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="34e95-130">We recommend that you read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="34e95-131">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="34e95-131">Azure portal</span></span>

<span data-ttu-id="34e95-132">Pour activer la collecte des journaux de métriques et de diagnostics dans le portail Azure, accédez à votre base de données SQL Azure ou à une page de pool élastique, puis cliquez sur **Paramètres de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="34e95-132">To enable metrics and diagnostic logs collection in the Azure portal, navigate to your Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![activer dans le portail Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="34e95-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34e95-134">PowerShell</span></span>

<span data-ttu-id="34e95-135">Pour activer la journalisation des métriques et diagnostics à l’aide de PowerShell, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="34e95-135">To enable metrics and diagnostics logging using PowerShell, use the following commands:</span></span>

- <span data-ttu-id="34e95-136">Pour activer le stockage des journaux de diagnostic dans un compte de stockage, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="34e95-136">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="34e95-137">L’ID de compte de stockage est l’ID de ressource pour le compte de stockage auquel vous souhaitez envoyer les journaux.</span><span class="sxs-lookup"><span data-stu-id="34e95-137">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="34e95-138">Pour activer la diffusion en continu des journaux de diagnostic vers un Event Hub, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="34e95-138">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="34e95-139">L’ID de règle Service Bus est une chaîne au format suivant :</span><span class="sxs-lookup"><span data-stu-id="34e95-139">The Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="34e95-140">Pour activer l’envoi des journaux de diagnostic à un espace de travail Log Analytics, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="34e95-140">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="34e95-141">Vous pouvez obtenir l’ID de ressource de votre espace de travail Log Analytics à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="34e95-141">You can obtain the resource id of your Log Analytics workspace using the following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="34e95-142">Vous pouvez combiner ces paramètres pour activer plusieurs options de sortie.</span><span class="sxs-lookup"><span data-stu-id="34e95-142">You can combine these parameters to enable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="34e95-143">Interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="34e95-143">CLI</span></span>

<span data-ttu-id="34e95-144">Pour activer la journalisation des métriques et diagnostics à l’aide d’Azure CLI, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="34e95-144">To enable metrics and diagnostics logging using the Azure CLI, use the following commands:</span></span>

- <span data-ttu-id="34e95-145">Pour activer le stockage des journaux de diagnostic dans un compte de stockage, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="34e95-145">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="34e95-146">L’ID de compte de stockage est l’ID de ressource pour le compte de stockage auquel vous souhaitez envoyer les journaux.</span><span class="sxs-lookup"><span data-stu-id="34e95-146">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="34e95-147">Pour activer la diffusion en continu des journaux de diagnostic vers un Event Hub, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="34e95-147">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="34e95-148">L’ID de règle Service Bus est une chaîne au format suivant :</span><span class="sxs-lookup"><span data-stu-id="34e95-148">The Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="34e95-149">Pour activer l’envoi des journaux de diagnostic à un espace de travail Log Analytics, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="34e95-149">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

<span data-ttu-id="34e95-150">Vous pouvez combiner ces paramètres pour activer plusieurs options de sortie.</span><span class="sxs-lookup"><span data-stu-id="34e95-150">You can combine these parameters to enable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="34e95-151">API REST</span><span class="sxs-lookup"><span data-stu-id="34e95-151">REST API</span></span>

<span data-ttu-id="34e95-152">Découvrez comment [modifier les paramètres de diagnostic à l’aide de l’API RESTS Azure Monitor](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="34e95-152">Read about how to [change Diagnostic settings using the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="34e95-153">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="34e95-153">Resource Manager template</span></span>

<span data-ttu-id="34e95-154">Découvrez comment [activer automatiquement les paramètres de diagnostic lors de la création de ressources à l’aide d’un modèle Resource Manager](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="34e95-154">Read about how to [enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="34e95-155">Envoyer à Log Analytics</span><span class="sxs-lookup"><span data-stu-id="34e95-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="34e95-156">Les journaux de métriques et diagnostics d’Azure SQL Database peuvent être envoyés à Log Analytics à l’aide de l’option « Envoyer à Log Analytics » intégrée dans le portail, ou en activant Log Analytics dans un paramètre de diagnostic via des applets de commande Azure PowerShell, Azure CLI ou l’API REST Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="34e95-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using the built-in “Send to Log Analytics” option in the portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="34e95-157">Vue d’ensemble de l’installation</span><span class="sxs-lookup"><span data-stu-id="34e95-157">Installation overview</span></span>

<span data-ttu-id="34e95-158">La surveillance d’une flotte Azure SQL Database est simple avec Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="34e95-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="34e95-159">Trois étapes sont requises :</span><span class="sxs-lookup"><span data-stu-id="34e95-159">Three steps are required:</span></span>

1.  <span data-ttu-id="34e95-160">Créer une ressource Log Analytics</span><span class="sxs-lookup"><span data-stu-id="34e95-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="34e95-161">Configurer des bases de données pour enregistrer des journaux de métriques et diagnostics dans la ressource Log Analytics créée</span><span class="sxs-lookup"><span data-stu-id="34e95-161">Configure databases to record metrics and diagnostic logs into the created Log Analytics</span></span>
3.  <span data-ttu-id="34e95-162">Installer la solution **Azure SQL Analytics** à partir de la galerie de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="34e95-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="34e95-163">Créer une ressource Log Analytics</span><span class="sxs-lookup"><span data-stu-id="34e95-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="34e95-164">Cliquez sur **Nouveau** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="34e95-164">Click **New** in the left-hand menu.</span></span>
2. <span data-ttu-id="34e95-165">Cliquez sur **Surveillance et gestion**.</span><span class="sxs-lookup"><span data-stu-id="34e95-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="34e95-166">Cliquez sur **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="34e95-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="34e95-167">Complétez le formulaire de Log Analytics avec les informations supplémentaires requises : nom d’espace de travail, abonnement, groupe de ressources, emplacement et niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="34e95-167">Fill in the Log Analytics form with the additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-to-record-metrics-and-diagnostic-logs"></a><span data-ttu-id="34e95-169">Configurer des bases de données pour enregistrer des journaux de métriques et diagnostics</span><span class="sxs-lookup"><span data-stu-id="34e95-169">Configure databases to record metrics and diagnostic logs</span></span>

<span data-ttu-id="34e95-170">La manière la plus simple de configurer l’emplacement où les bases de données enregistrent leurs mesures est d’utiliser le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="34e95-170">The easiest way to configure where databases record their metrics is through the Azure portal.</span></span> <span data-ttu-id="34e95-171">Dans le portail Azure, accédez à vos ressources Azure SQL Database, puis cliquez sur **Paramètres de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="34e95-171">In the Azure portal, navigate to your Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-the-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="34e95-172">Installer la solution Azure SQL Analytics à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="34e95-172">Install the Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="34e95-173">Une fois la ressource Log Analytics créée et vos données en circulation dans celle-ci, installez la solution Azure SQL Analytics.</span><span class="sxs-lookup"><span data-stu-id="34e95-173">Once the Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="34e95-174">Vous pouvez faire cela via la **Galerie de solutions** accessible dans la page d’accueil de Microsoft Operations Management Suite et dans le menu latéral.</span><span class="sxs-lookup"><span data-stu-id="34e95-174">This can be done through the **Solutions Gallery** that you can find on the OMS homepage and in the side menu.</span></span> <span data-ttu-id="34e95-175">Dans la galerie, trouvez la solution **Azure SQL Analytics**, cliquez dessus, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="34e95-175">In the gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![solution de surveillance](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="34e95-177">Dans votre page d’accueil de Microsoft Operations Management Suite, une nouvelle vignette intitulée **Azure SQL Analytics** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="34e95-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="34e95-178">La sélection de cette vignette a pour effet d’ouvrir le tableau de bord Azure SQL Analytics.</span><span class="sxs-lookup"><span data-stu-id="34e95-178">Selecting this tile opens the Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="34e95-179">Utilisation de la solution Azure SQL Analytics</span><span class="sxs-lookup"><span data-stu-id="34e95-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="34e95-180">Azure SQL Analytics est un tableau de bord hiérarchique qui vous permet de naviguer dans la hiérarchie des ressources d’Azure SQL Analytics.</span><span class="sxs-lookup"><span data-stu-id="34e95-180">Azure SQL Analytics is a hierarchical dashboard that allows you to navigate through the hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="34e95-181">Cette fonctionnalité vous permet d’opérer une surveillance générale, ainsi que d’étendre votre analyse à l’ensemble approprié de ressources.</span><span class="sxs-lookup"><span data-stu-id="34e95-181">This capability enables you to do high-level monitoring but it also enables you to scope your monitoring to just the right set of resources.</span></span>
<span data-ttu-id="34e95-182">Le tableau de bord contient les listes des différentes ressources sous la ressource sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="34e95-182">Dashboard contains the lists of different resources under the selected resource.</span></span> <span data-ttu-id="34e95-183">Par exemple, pour un abonnement sélectionné, vous pouvez voir l’ensemble des serveurs, des pools élastiques et des bases appartenant à l’abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="34e95-183">For example, for a selected subscription you can see the all servers, elastic pools and databases that belong to the selected subscription.</span></span> <span data-ttu-id="34e95-184">En outre, pour les pools élastiques et les bases de données, vous pouvez voir les métriques d’utilisation de ces ressources.</span><span class="sxs-lookup"><span data-stu-id="34e95-184">Additionally, for Elastic Pools and databases, you can see the resource usage metrics of that resource.</span></span> <span data-ttu-id="34e95-185">Celles-ci incluent des graphiques pour DTU, UC, E/S, journal, sessions, workers, connexions et stockage en Go.</span><span class="sxs-lookup"><span data-stu-id="34e95-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="34e95-186">Envoyer à Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="34e95-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="34e95-187">Les journaux de métriques et diagnostics d’Azure SQL Database peuvent être envoyés à Azure Event Hub à l’aide de l’option « Diffuser vers Event Hub » intégrée dans le portail, ou en activant l’ID de règle Service Bus dans un paramètre de diagnostic via des applets de commande Azure PowerShell, Azure CLI ou l’API REST Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="34e95-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using the built-in “Stream to an event hub” option in the portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-to-do-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="34e95-188">Que faire des journaux de métriques et diagnostics dans Event Hub ?</span><span class="sxs-lookup"><span data-stu-id="34e95-188">What to do with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="34e95-189">En sélectionnant les données envoyées à Event Hub, vous vous rapprochez de l’activation de scénarios d’analyse avancée.</span><span class="sxs-lookup"><span data-stu-id="34e95-189">Once the selected data is streamed into Event Hub, you are one step closer to enabling advanced monitoring scenarios.</span></span> <span data-ttu-id="34e95-190">Event Hubs fonctionne comme la « porte d'entrée » d’un pipeline d’événements, et une fois que les données sont collectées dans un concentrateur d'événements, peut être transformées et stockées à l'aide de n'importe quel fournisseur d'analyse en temps réel ou d’adaptateurs de traitement par lot ou de stockage.</span><span class="sxs-lookup"><span data-stu-id="34e95-190">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="34e95-191">Les concentrateurs d'événements dissocient la production d'un flux d'événements de la consommation de ces événements, de manière à ce que les consommateurs d'événements puissent accéder aux événements selon leur propre planification.</span><span class="sxs-lookup"><span data-stu-id="34e95-191">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span> <span data-ttu-id="34e95-192">Pour plus d’informations sur Event Hub, voir :</span><span class="sxs-lookup"><span data-stu-id="34e95-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="34e95-193">[Qu’est-ce qu’Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) ?</span><span class="sxs-lookup"><span data-stu-id="34e95-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="34e95-194">Prise en main des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="34e95-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="34e95-195">Voici quelques façons d’utiliser la fonctionnalité de diffusion en continu :</span><span class="sxs-lookup"><span data-stu-id="34e95-195">Here are just a few ways you might use the streaming capability:</span></span>

-   <span data-ttu-id="34e95-196">Afficher l’état d’intégrité du service en diffusant des données de chemin réactif vers PowerBI : en utilisant Event Hubs, Stream Analytics et PowerBI, vous pouvez facilement transformer vos données de métriques et de diagnostic en informations en temps réel sur vos services Azure.</span><span class="sxs-lookup"><span data-stu-id="34e95-196">View service health by streaming “hot path” data to PowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="34e95-197">Pour une vue d’ensemble de la manière de configurer un Event Hub, de traiter les données avec Stream Analytics, et d’utiliser PowerBI comme sortie, voir [Stream Analytics et Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="34e95-197">For an overview of how to set up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="34e95-198">Envoyer les journaux à des flux de journalisation et de télémétrie tiers : une diffusion en continu Event Hubs vous permet d’envoyer vos journaux de métriques et diagnostics à différentes solution tierces de surveillance et d’analytique des journaux.</span><span class="sxs-lookup"><span data-stu-id="34e95-198">Stream logs to third-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in to different third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="34e95-199">Créer une plateforme de journalisation et de télémétrie personnalisée : si vous disposez déjà d’une plateforme de télémétrie personnalisée, ou si vous envisagez d’en créer une, la nature hautement évolutive de publication et d’abonnement d’Event Hubs vous permet d’intégrer avec souplesse les journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="34e95-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="34e95-200">Lisez le [guide de Dan Rosanova sur l’utilisation d’Event Hubs dans une plateforme de télémétrie à l’échelle mondiale](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="34e95-200">See [Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="34e95-201">Envoyer à Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="34e95-201">Stream into Azure Storage</span></span>

<span data-ttu-id="34e95-202">Les journaux de métriques et diagnostics d’Azure SQL Database peuvent être stockés dans Stockage Aure à l’aide de l’option « Archiver dans un compte de stockage » intégrée dans le portail Azure, ou en activant Stockage Azure dans un paramètre de diagnostic via des applets de commande Azure PowerShell, Azure CLI ou l’API REST Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="34e95-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using the built-in "Archive to a storage account” option in the Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="34e95-203">Schéma des journaux de métriques et diagnostics dans le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="34e95-203">Schema of metrics and diagnostic logs in the storage account</span></span>

<span data-ttu-id="34e95-204">Après que vous avez configuré la collecte des journaux de métriques et diagnostics, lorsque les premières lignes de données sont disponibles, un conteneur de stockage est créé dans le compte de stockage que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="34e95-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in the storage account you selected when the first rows of data are available.</span></span> <span data-ttu-id="34e95-205">La structure de ces objets blob est la suivante :</span><span class="sxs-lookup"><span data-stu-id="34e95-205">The structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="34e95-206">Ou, plus simplement :</span><span class="sxs-lookup"><span data-stu-id="34e95-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="34e95-207">Par exemple, un nom d’objet blob pour des métriques sur 1 minute pourrait être :</span><span class="sxs-lookup"><span data-stu-id="34e95-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="34e95-208">Si vous souhaitez enregistrer les données du Pool élastique, le nom d’objet blob est un peu différent :</span><span class="sxs-lookup"><span data-stu-id="34e95-208">In case you want to record the data from the Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="34e95-209">Télécharger les métriques et journaux de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="34e95-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="34e95-210">Consultez [Télécharger les journaux de métriques et diagnostics de Stockage Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).</span><span class="sxs-lookup"><span data-stu-id="34e95-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="34e95-211">Métriques de 1 minute</span><span class="sxs-lookup"><span data-stu-id="34e95-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="34e95-212">**Ressource**</span><span class="sxs-lookup"><span data-stu-id="34e95-212">**Resource**</span></span>|<span data-ttu-id="34e95-213">**Métriques**</span><span class="sxs-lookup"><span data-stu-id="34e95-213">**Metrics**</span></span>|
|<span data-ttu-id="34e95-214">Base de données</span><span class="sxs-lookup"><span data-stu-id="34e95-214">Database</span></span>|<span data-ttu-id="34e95-215">Pourcentage DTU, Limite DTU, Pourcentage UC, Pourcentage de lecture de données physiques, Pourcentage d’écriture du journal, Connexions réussies/en échec/bloquées par pare-feu, Pourcentage de sessions, Pourcentage de workers, Stockage, Pourcentage de stockage, Pourcentage de stockage XTP, blocages</span><span class="sxs-lookup"><span data-stu-id="34e95-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="34e95-216">Pool élastique</span><span class="sxs-lookup"><span data-stu-id="34e95-216">Elastic pool</span></span>|<span data-ttu-id="34e95-217">Pourcentage DTU, eDTU utilisé, Limite eDTU, Pourcentage UC, Pourcentage de lecture de données physiques, Pourcentage d’écriture du journal, Pourcentage de sessions, Pourcentage de workers, Stockage, Pourcentage de stockage, Limite de stockage, Pourcentage de stockage XTP</span><span class="sxs-lookup"><span data-stu-id="34e95-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="34e95-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="34e95-218">Next steps</span></span>

- <span data-ttu-id="34e95-219">Pour comprendre non seulement comment activer la journalisation, mais aussi les métriques et les catégories de journaux prises en charge par les différents services Azure, voir [Vue d’ensemble des mesures dans Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) et [Présentation des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="34e95-219">Read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>
- <span data-ttu-id="34e95-220">Pour en savoir plus sur les concentrateurs d’événements, lisez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="34e95-220">Read these articles to learn about event hubs:</span></span>
   - <span data-ttu-id="34e95-221">[Qu’est-ce qu’Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) ?</span><span class="sxs-lookup"><span data-stu-id="34e95-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="34e95-222">Prise en main des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="34e95-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="34e95-223">Consultez [Télécharger les journaux de métriques et diagnostics de Stockage Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).</span><span class="sxs-lookup"><span data-stu-id="34e95-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
