---
title: "aaaAzure SQL de la base de données des métriques et la journalisation des diagnostics | Documents Microsoft"
description: "En savoir plus sur la configuration de l’utilisation des ressources Azure SQL Database ressource toostore, la connectivité et des statistiques d’exécution de requête."
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
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="e511d-103">Journalisation des métriques et diagnostics d’Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e511d-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="e511d-104">Azure SQL Database peut émettre des journaux de métriques et de diagnostics pour faciliter la surveillance.</span><span class="sxs-lookup"><span data-stu-id="e511d-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="e511d-105">Vous pouvez configurer l’utilisation des ressources toostore base de données SQL Azure, aux employés et les sessions et connectivité dans une de ces ressources Azure :</span><span class="sxs-lookup"><span data-stu-id="e511d-105">You can configure Azure SQL Database toostore resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="e511d-106">**Stockage Azure** : pour archiver des quantités importantes de données de télémétrie à un petit prix</span><span class="sxs-lookup"><span data-stu-id="e511d-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="e511d-107">**Azure Event Hub** : pour intégrer des données de télémétrie Azure SQL Database à votre solution de surveillance personnalisée ou à vos pipelines très actifs</span><span class="sxs-lookup"><span data-stu-id="e511d-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="e511d-108">**Azure Analytique de journal**: pour prédéfinies hello solution avec reporting, de génération d’alertes et de limiter les fonctionnalités de surveillance</span><span class="sxs-lookup"><span data-stu-id="e511d-108">**Azure Log Analytics**: For out of hello box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![architecture](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="e511d-110">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="e511d-110">Enable logging</span></span>

<span data-ttu-id="e511d-111">La journalisation des métriques et diagnostics n’est pas activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="e511d-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="e511d-112">Vous pouvez activer et gérer des mesures et journalisation des diagnostics à l’aide d’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="e511d-112">You can enable and manage metrics and diagnostics logging using one of hello following methods:</span></span>
- <span data-ttu-id="e511d-113">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e511d-113">Azure portal</span></span>
- <span data-ttu-id="e511d-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e511d-114">PowerShell</span></span>
- <span data-ttu-id="e511d-115">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="e511d-115">Azure CLI</span></span>
- <span data-ttu-id="e511d-116">API REST</span><span class="sxs-lookup"><span data-stu-id="e511d-116">REST API</span></span> 
- <span data-ttu-id="e511d-117">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e511d-117">Resource Manager template</span></span>

<span data-ttu-id="e511d-118">Lorsque vous activez les métriques et la journalisation des diagnostics, vous devez toospecify hello ressource Azure où les données sélectionnées sont collectées.</span><span class="sxs-lookup"><span data-stu-id="e511d-118">When you enable metrics and diagnostics logging, you need toospecify hello Azure resource where selected data is collected.</span></span> <span data-ttu-id="e511d-119">Options disponibles :</span><span class="sxs-lookup"><span data-stu-id="e511d-119">Options available:</span></span>
- <span data-ttu-id="e511d-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e511d-120">Log analytics</span></span>
- <span data-ttu-id="e511d-121">Event Hub</span><span class="sxs-lookup"><span data-stu-id="e511d-121">Event Hub</span></span>
- <span data-ttu-id="e511d-122">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="e511d-122">Azure Storage</span></span> 

<span data-ttu-id="e511d-123">Vous pouvez approvisionner une nouvelle ressource Azure ou sélectionner une ressource existante.</span><span class="sxs-lookup"><span data-stu-id="e511d-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="e511d-124">Après avoir sélectionné la ressource de stockage hello, vous devez toospecify le toocollect de données.</span><span class="sxs-lookup"><span data-stu-id="e511d-124">After selecting hello storage resource, you need toospecify which data toocollect.</span></span> <span data-ttu-id="e511d-125">Les options disponibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e511d-125">Options available include:</span></span>

- <span data-ttu-id="e511d-126">**[Métriques de 1 minute](sql-database-metrics-diag-logging.md#1-minute-metrics)** : contient Pourcentage DTU, Limite DTU, Pourcentage UC, Pourcentage de lecture de données physiques, Pourcentage d’écriture du journal, Connexions réussies/en échec/bloquées par pare-feu, Pourcentage de sessions, Pourcentage de workers, Stockage, Pourcentage de stockage, Pourcentage de stockage XTP</span><span class="sxs-lookup"><span data-stu-id="e511d-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="e511d-127">Si vous spécifiez un compte de AzureStorage ou de concentrateur d’événements, vous pouvez spécifier un toospecify de stratégie de rétention de données qui est antérieures à la période de temps sélectionné est supprimé.</span><span class="sxs-lookup"><span data-stu-id="e511d-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy toospecify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="e511d-128">Si vous spécifiez Analytique de journal, stratégie de rétention hello dépend de niveau de tarification sélectionné hello.</span><span class="sxs-lookup"><span data-stu-id="e511d-128">If you specify Log Analytics, hello retention policy depends on hello selected pricing tier.</span></span> <span data-ttu-id="e511d-129">Pour en savoir plus, voir [Tarification de Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="e511d-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="e511d-130">Nous vous recommandons de lire les deux hello [vue d’ensemble des métriques dans Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) et [vue d’ensemble de Azure des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) les articles toogain comprendre non seulement comment journalisation tooenable, mais hello les catégories de journaux et les mesures prises en charge par hello divers services Azure.</span><span class="sxs-lookup"><span data-stu-id="e511d-130">We recommend that you read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="e511d-131">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e511d-131">Azure portal</span></span>

<span data-ttu-id="e511d-132">métriques de tooenable et de collection de journaux de diagnostic Bonjour portail Azure, accédez de base de données SQL Azure tooyour ou page de pool élastique, puis cliquez sur **les paramètres de Diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="e511d-132">tooenable metrics and diagnostic logs collection in hello Azure portal, navigate tooyour Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![Activer Bonjour portail Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="e511d-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e511d-134">PowerShell</span></span>

<span data-ttu-id="e511d-135">tooenable métriques et la journalisation des diagnostics à l’aide de PowerShell, utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="e511d-135">tooenable metrics and diagnostics logging using PowerShell, use hello following commands:</span></span>

- <span data-ttu-id="e511d-136">stockage tooenable de journaux de Diagnostic dans un compte de stockage, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="e511d-136">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="e511d-137">Hello ID de compte de stockage concerne les id de ressource hello toowhich de compte de stockage hello souhaité toosend hello se connecte.</span><span class="sxs-lookup"><span data-stu-id="e511d-137">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="e511d-138">tooenable de diffusion en continu de journaux de Diagnostic tooan concentrateur d’événements, utilisez la commande :</span><span class="sxs-lookup"><span data-stu-id="e511d-138">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="e511d-139">Hello ID de règle de Bus de Service est une chaîne au format suivant :</span><span class="sxs-lookup"><span data-stu-id="e511d-139">hello Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="e511d-140">Utilisez la commande tooenable envoi de journaux de Diagnostic tooa Analytique de journal espace de travail :</span><span class="sxs-lookup"><span data-stu-id="e511d-140">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="e511d-141">Vous pouvez obtenir l’id de ressource hello de votre espace de travail Analytique des journaux à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e511d-141">You can obtain hello resource id of your Log Analytics workspace using hello following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="e511d-142">Vous pouvez combiner ces paramètres tooenable plusieurs options de sortie.</span><span class="sxs-lookup"><span data-stu-id="e511d-142">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="e511d-143">Interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="e511d-143">CLI</span></span>

<span data-ttu-id="e511d-144">métriques de tooenable et à l’aide de la journalisation de diagnostics hello CLI d’Azure, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="e511d-144">tooenable metrics and diagnostics logging using hello Azure CLI, use hello following commands:</span></span>

- <span data-ttu-id="e511d-145">stockage tooenable de journaux de Diagnostic dans un compte de stockage, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="e511d-145">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="e511d-146">Hello ID de compte de stockage concerne les id de ressource hello toowhich de compte de stockage hello souhaité toosend hello se connecte.</span><span class="sxs-lookup"><span data-stu-id="e511d-146">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="e511d-147">tooenable de diffusion en continu de journaux de Diagnostic tooan concentrateur d’événements, utilisez la commande :</span><span class="sxs-lookup"><span data-stu-id="e511d-147">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="e511d-148">Hello ID de règle de Bus de Service est une chaîne au format suivant :</span><span class="sxs-lookup"><span data-stu-id="e511d-148">hello Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="e511d-149">Utilisez la commande tooenable envoi de journaux de Diagnostic tooa Analytique de journal espace de travail :</span><span class="sxs-lookup"><span data-stu-id="e511d-149">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

<span data-ttu-id="e511d-150">Vous pouvez combiner ces paramètres tooenable plusieurs options de sortie.</span><span class="sxs-lookup"><span data-stu-id="e511d-150">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="e511d-151">API REST</span><span class="sxs-lookup"><span data-stu-id="e511d-151">REST API</span></span>

<span data-ttu-id="e511d-152">Découvrez comment trop[modifier les paramètres de Diagnostic à l’aide de hello API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="e511d-152">Read about how too[change Diagnostic settings using hello Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="e511d-153">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e511d-153">Resource Manager template</span></span>

<span data-ttu-id="e511d-154">Découvrez comment trop[activer les paramètres de Diagnostic lors de la création de ressources à l’aide du Gestionnaire de ressources du modèle](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="e511d-154">Read about how too[enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="e511d-155">Envoyer à Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e511d-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="e511d-156">Les journaux de diagnostic et les mesures de base de données SQL Azure peuvent être diffusés en Analytique de journal à l’aide d’option intégrée « envoi » tooLog Analytique de hello dans le portail de hello, ou en activant l’Analytique des journaux dans un paramètre de diagnostic via les applets de commande Azure PowerShell, CLI d’Azure ou Azure moniteur reste API.</span><span class="sxs-lookup"><span data-stu-id="e511d-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using hello built-in “Send tooLog Analytics” option in hello portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="e511d-157">Vue d’ensemble de l’installation</span><span class="sxs-lookup"><span data-stu-id="e511d-157">Installation overview</span></span>

<span data-ttu-id="e511d-158">La surveillance d’une flotte Azure SQL Database est simple avec Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e511d-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="e511d-159">Trois étapes sont requises :</span><span class="sxs-lookup"><span data-stu-id="e511d-159">Three steps are required:</span></span>

1.  <span data-ttu-id="e511d-160">Créer une ressource Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e511d-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="e511d-161">Configurer des métriques de toorecord de bases de données et les journaux de diagnostic dans hello créé Analytique de journal</span><span class="sxs-lookup"><span data-stu-id="e511d-161">Configure databases toorecord metrics and diagnostic logs into hello created Log Analytics</span></span>
3.  <span data-ttu-id="e511d-162">Installer la solution **Azure SQL Analytics** à partir de la galerie de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e511d-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="e511d-163">Créer une ressource Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e511d-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="e511d-164">Cliquez sur **nouveau** dans le menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="e511d-164">Click **New** in hello left-hand menu.</span></span>
2. <span data-ttu-id="e511d-165">Cliquez sur **Surveillance et gestion**.</span><span class="sxs-lookup"><span data-stu-id="e511d-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="e511d-166">Cliquez sur **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e511d-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="e511d-167">Remplissez hello Analytique de journal formulaire avec des informations supplémentaires hello requis : nom de l’espace de travail, abonnement, groupe de ressources, l’emplacement et niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="e511d-167">Fill in hello Log Analytics form with hello additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a><span data-ttu-id="e511d-169">Configurer des métriques de toorecord de bases de données et les journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="e511d-169">Configure databases toorecord metrics and diagnostic logs</span></span>

<span data-ttu-id="e511d-170">Hello tooconfigure de façon plus simple où les bases de données enregistrent leurs mesures est hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e511d-170">hello easiest way tooconfigure where databases record their metrics is through hello Azure portal.</span></span> <span data-ttu-id="e511d-171">Dans hello portail Azure, accédez de ressource de base de données SQL Azure tooyour et cliquez sur **paramètres de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="e511d-171">In hello Azure portal, navigate tooyour Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="e511d-172">Installer la solution d’Analytique de SQL Azure hello à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="e511d-172">Install hello Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="e511d-173">Une fois hello ressource d’Analytique de journal est créée et vos données circulent dans celui-ci, installer des solutions d’Analytique de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e511d-173">Once hello Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="e511d-174">Cela peut être effectué à partir de hello **galerie des Solutions** que vous pouvez trouver sur la page d’accueil de hello OMS et dans le menu latéral de hello.</span><span class="sxs-lookup"><span data-stu-id="e511d-174">This can be done through hello **Solutions Gallery** that you can find on hello OMS homepage and in hello side menu.</span></span> <span data-ttu-id="e511d-175">Dans la galerie hello, recherchez et cliquez sur **Analytique de SQL Azure** solution et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e511d-175">In hello gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![solution de surveillance](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="e511d-177">Dans votre page d’accueil de Microsoft Operations Management Suite, une nouvelle vignette intitulée **Azure SQL Analytics** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e511d-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="e511d-178">En sélectionnant cette vignette, tableau de bord hello Analytique de SQL Azure s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e511d-178">Selecting this tile opens hello Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="e511d-179">Utilisation de la solution Azure SQL Analytics</span><span class="sxs-lookup"><span data-stu-id="e511d-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="e511d-180">Analytique de SQL Azure est un tableau de bord hiérarchique qui vous permet de toonavigate via la hiérarchie de hello de ressources de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e511d-180">Azure SQL Analytics is a hierarchical dashboard that allows you toonavigate through hello hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="e511d-181">Cela permet de capacité vous toodo principales analyse également, mais il vous permet de tooscope votre droit de hello toojust analyse jeu de ressources.</span><span class="sxs-lookup"><span data-stu-id="e511d-181">This capability enables you toodo high-level monitoring but it also enables you tooscope your monitoring toojust hello right set of resources.</span></span>
<span data-ttu-id="e511d-182">Tableau de bord contient des listes de hello de différentes ressources sous la ressource de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e511d-182">Dashboard contains hello lists of different resources under hello selected resource.</span></span> <span data-ttu-id="e511d-183">Par exemple, pour un abonnement sélectionné, vous pouvez voir hello tous les serveurs, les pools élastiques et les bases de données qui appartiennent toohello sélectionné l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="e511d-183">For example, for a selected subscription you can see hello all servers, elastic pools and databases that belong toohello selected subscription.</span></span> <span data-ttu-id="e511d-184">En outre, pour les bases de données et les Pools élastiques, vous pouvez voir les métriques d’utilisation de ressources hello d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="e511d-184">Additionally, for Elastic Pools and databases, you can see hello resource usage metrics of that resource.</span></span> <span data-ttu-id="e511d-185">Celles-ci incluent des graphiques pour DTU, UC, E/S, journal, sessions, workers, connexions et stockage en Go.</span><span class="sxs-lookup"><span data-stu-id="e511d-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="e511d-186">Envoyer à Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="e511d-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="e511d-187">Les journaux de diagnostic et les mesures de base de données SQL Azure peuvent être diffusés à un concentrateur d’événements à l’aide d’option d’intégré « flux tooan concentrateur d’événements » hello dans le portail de hello, ou en activant l’Id de règle de Bus de Service dans un paramètre de diagnostic via les applets de commande PowerShell Azure, CLI d’Azure ou Azure moniteur reste API.</span><span class="sxs-lookup"><span data-stu-id="e511d-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using hello built-in “Stream tooan event hub” option in hello portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="e511d-188">Quelles toodo avec des métriques et des journaux de diagnostic dans le concentrateur d’événements ?</span><span class="sxs-lookup"><span data-stu-id="e511d-188">What toodo with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="e511d-189">Une fois que les données de salutation sélectionnée sont diffusée en continu dans le concentrateur d’événements, vous êtes un tooenabling proche étape des scénarios d’analyses avancés.</span><span class="sxs-lookup"><span data-stu-id="e511d-189">Once hello selected data is streamed into Event Hub, you are one step closer tooenabling advanced monitoring scenarios.</span></span> <span data-ttu-id="e511d-190">Concentrateurs d’événements joue le rôle hello « porte d’entrée » pour un pipeline d’événements, et une fois que les données sont collectées dans un concentrateur d’événements, il peut être transformé et stockées à l’aide de n’importe quel fournisseur analytique en temps réel ou des cartes de traitement par lot/stockage.</span><span class="sxs-lookup"><span data-stu-id="e511d-190">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="e511d-191">Concentrateurs d’événements dissocie production hello d’un flux d’événements à partir de la consommation de ces événements, hello afin que les consommateurs d’événements peuvent accéder à des événements de hello sur leur propre calendrier.</span><span class="sxs-lookup"><span data-stu-id="e511d-191">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span> <span data-ttu-id="e511d-192">Pour plus d’informations sur Event Hub, voir :</span><span class="sxs-lookup"><span data-stu-id="e511d-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="e511d-193">[Qu’est-ce qu’Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) ?</span><span class="sxs-lookup"><span data-stu-id="e511d-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="e511d-194">Prise en main des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="e511d-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="e511d-195">Voici quelques méthodes que vous pouvez utiliser la capacité de diffusion en continu de hello :</span><span class="sxs-lookup"><span data-stu-id="e511d-195">Here are just a few ways you might use hello streaming capability:</span></span>

-   <span data-ttu-id="e511d-196">Afficher l’intégrité du service par diffusion en continu de « chemin réactif » données tooPowerBI - concentrateurs d’événements à l’aide de flux Analytique et Power BI, vous pouvez facilement transformer vos données métriques et des diagnostics dans près des informations en temps réel sur vos services Azure.</span><span class="sxs-lookup"><span data-stu-id="e511d-196">View service health by streaming “hot path” data tooPowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="e511d-197">Pour une vue d’ensemble du mode de tooset d’un service Event Hubs, traiter les données avec le flux de données Analytique et utiliser Power BI comme sortie, consultez [Analytique de flux de données et Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="e511d-197">For an overview of how tooset up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="e511d-198">Flux de données des journaux toothird tiers journalisation et les données de télémétrie flux – concentrateurs d’événements à l’aide de diffusion en continu vous peuvent obtenir de vos mesures et les journaux de diagnostic dans toodifferent des journaux et surveillance analytique solutions tierces.</span><span class="sxs-lookup"><span data-stu-id="e511d-198">Stream logs toothird-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in toodifferent third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="e511d-199">Générer une télémétrie personnalisée et la plateforme de journalisation : Si vous disposez déjà d’une plateforme de télémétrie personnalisées ou sont simplement penser à la génération 1, hello hautement évolutive de publication / abonnement nature des concentrateurs d’événements vous permet de tooflexibly d’acquisition des journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="e511d-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="e511d-200">Consultez [toousing de guide de Dan Rosanova concentrateurs d’événements dans une plateforme de télémétrie à l’échelle mondiale](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="e511d-200">See [Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="e511d-201">Envoyer à Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="e511d-201">Stream into Azure Storage</span></span>

<span data-ttu-id="e511d-202">Les journaux de diagnostic et les mesures de base de données SQL Azure peuvent être stockées dans le stockage Azure à l’aide de l’option des « Archiver le compte de stockage tooa » hello intégrée Bonjour portail Azure, ou en activant le stockage Azure dans un paramètre de diagnostic via les applets de commande PowerShell Azure, CLI d’Azure ou Azure API REST de moniteur.</span><span class="sxs-lookup"><span data-stu-id="e511d-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using hello built-in "Archive tooa storage account” option in hello Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a><span data-ttu-id="e511d-203">Schéma des métriques et des journaux de diagnostic dans le compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="e511d-203">Schema of metrics and diagnostic logs in hello storage account</span></span>

<span data-ttu-id="e511d-204">Une fois que vous avez configuré des mesures et de collection de journaux de diagnostic, un conteneur de stockage est créé dans le compte de stockage hello sélectionné lorsque hello premières lignes de données sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="e511d-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in hello storage account you selected when hello first rows of data are available.</span></span> <span data-ttu-id="e511d-205">structure Hello de ces objets BLOB est la suivante :</span><span class="sxs-lookup"><span data-stu-id="e511d-205">hello structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="e511d-206">Ou, plus simplement :</span><span class="sxs-lookup"><span data-stu-id="e511d-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="e511d-207">Par exemple, un nom d’objet blob pour des métriques sur 1 minute pourrait être :</span><span class="sxs-lookup"><span data-stu-id="e511d-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="e511d-208">Au cas où vous souhaiteriez données hello toorecord hello Pool élastique, le nom d’objet blob est un peu différent :</span><span class="sxs-lookup"><span data-stu-id="e511d-208">In case you want toorecord hello data from hello Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="e511d-209">Télécharger les métriques et journaux de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="e511d-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="e511d-210">Consultez [Télécharger les journaux de métriques et diagnostics de Stockage Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).</span><span class="sxs-lookup"><span data-stu-id="e511d-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="e511d-211">Métriques de 1 minute</span><span class="sxs-lookup"><span data-stu-id="e511d-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="e511d-212">**Ressource**</span><span class="sxs-lookup"><span data-stu-id="e511d-212">**Resource**</span></span>|<span data-ttu-id="e511d-213">**Métriques**</span><span class="sxs-lookup"><span data-stu-id="e511d-213">**Metrics**</span></span>|
|<span data-ttu-id="e511d-214">Base de données</span><span class="sxs-lookup"><span data-stu-id="e511d-214">Database</span></span>|<span data-ttu-id="e511d-215">Pourcentage DTU, Limite DTU, Pourcentage UC, Pourcentage de lecture de données physiques, Pourcentage d’écriture du journal, Connexions réussies/en échec/bloquées par pare-feu, Pourcentage de sessions, Pourcentage de workers, Stockage, Pourcentage de stockage, Pourcentage de stockage XTP, blocages</span><span class="sxs-lookup"><span data-stu-id="e511d-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="e511d-216">Pool élastique</span><span class="sxs-lookup"><span data-stu-id="e511d-216">Elastic pool</span></span>|<span data-ttu-id="e511d-217">Pourcentage DTU, eDTU utilisé, Limite eDTU, Pourcentage UC, Pourcentage de lecture de données physiques, Pourcentage d’écriture du journal, Pourcentage de sessions, Pourcentage de workers, Stockage, Pourcentage de stockage, Limite de stockage, Pourcentage de stockage XTP</span><span class="sxs-lookup"><span data-stu-id="e511d-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="e511d-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e511d-218">Next steps</span></span>

- <span data-ttu-id="e511d-219">Lire les deux hello [vue d’ensemble des métriques dans Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) et [vue d’ensemble de Azure des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain comprendre non seulement comment tooenable journalisation, mais hello métriques et connecter les catégories prise en charge par hello divers services Azure.</span><span class="sxs-lookup"><span data-stu-id="e511d-219">Read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>
- <span data-ttu-id="e511d-220">Lisez ces toolearn des articles sur les concentrateurs d’événements :</span><span class="sxs-lookup"><span data-stu-id="e511d-220">Read these articles toolearn about event hubs:</span></span>
   - <span data-ttu-id="e511d-221">[Qu’est-ce qu’Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) ?</span><span class="sxs-lookup"><span data-stu-id="e511d-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="e511d-222">Prise en main des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="e511d-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="e511d-223">Consultez [Télécharger les journaux de métriques et diagnostics de Stockage Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).</span><span class="sxs-lookup"><span data-stu-id="e511d-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
