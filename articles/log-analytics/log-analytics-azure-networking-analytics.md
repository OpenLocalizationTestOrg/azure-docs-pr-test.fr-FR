---
title: "Solution d’analytique du réseau Azure dans Log Analytics | Microsoft Docs"
description: "Vous pouvez utiliser la Solution d’analytique du réseau Azure dans Log Analytics pour consulter les journaux de groupes de sécurité réseau et de passerelle d’application Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 06b67322b3812a668a515ecc357171ede1d85441
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="88479-103">Solutions d’analyse réseaux Azure dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="88479-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="88479-104">Log Analytics propose les solutions suivantes pour la surveillance de vos réseaux :</span><span class="sxs-lookup"><span data-stu-id="88479-104">Log Analytics offers the following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="88479-105">Analyseur de performances réseau (NPM) pour</span><span class="sxs-lookup"><span data-stu-id="88479-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="88479-106">Surveiller l’intégrité de votre réseau</span><span class="sxs-lookup"><span data-stu-id="88479-106">Monitor the health of your network</span></span>
* <span data-ttu-id="88479-107">Azure Application Gateway Analytics à passer en revue</span><span class="sxs-lookup"><span data-stu-id="88479-107">Azure Application Gateway analytics to review</span></span>
 * <span data-ttu-id="88479-108">Journaux Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="88479-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="88479-109">Mesures Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="88479-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="88479-110">Azure Network Security Group Analytics à passer en revue</span><span class="sxs-lookup"><span data-stu-id="88479-110">Azure Network Security Group analytics to review</span></span>
 * <span data-ttu-id="88479-111">Journaux Azure Network Security Group</span><span class="sxs-lookup"><span data-stu-id="88479-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="88479-112">Analyseur de performances réseau (NPM)</span><span class="sxs-lookup"><span data-stu-id="88479-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="88479-113">La solution de gestion [Analyseur de performances réseau](log-analytics-network-performance-monitor.md) est une solution de surveillance du réseau, qui contrôle l’intégrité, la disponibilité et l’accessibilité des réseaux.</span><span class="sxs-lookup"><span data-stu-id="88479-113">The [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors the health, availability and reachability of networks.</span></span>  <span data-ttu-id="88479-114">Elle est utilisée pour contrôler la connectivité entre :</span><span class="sxs-lookup"><span data-stu-id="88479-114">It is used to monitor connectivity between:</span></span>

* <span data-ttu-id="88479-115">le cloud public et le site local ;</span><span class="sxs-lookup"><span data-stu-id="88479-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="88479-116">les centres de données et les emplacements des utilisateurs (filiales) ;</span><span class="sxs-lookup"><span data-stu-id="88479-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="88479-117">les sous-réseaux hébergeant différents niveaux d’une application multiniveau.</span><span class="sxs-lookup"><span data-stu-id="88479-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="88479-118">Pour plus d’informations, consultez l’[Analyseur de performances réseau](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="88479-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="88479-119">Azure Application Gateway et Network Security Group Analytics</span><span class="sxs-lookup"><span data-stu-id="88479-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="88479-120">Pour utiliser les solutions :</span><span class="sxs-lookup"><span data-stu-id="88479-120">To use the solutions:</span></span>
1. <span data-ttu-id="88479-121">Ajoutez la solution de gestion dans Log Analytics, et</span><span class="sxs-lookup"><span data-stu-id="88479-121">Add the management solution to Log Analytics, and</span></span>
2. <span data-ttu-id="88479-122">Activez les diagnostics pour les orienter vers un espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="88479-122">Enable diagnostics to direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="88479-123">Il n’est pas nécessaire d’écrire les journaux dans le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="88479-123">It is not necessary to write the logs to Azure Blob storage.</span></span>

<span data-ttu-id="88479-124">Vous pouvez activer les diagnostics et la solution correspondante pour Application Gateway, Networking Security Groups ou les deux.</span><span class="sxs-lookup"><span data-stu-id="88479-124">You can enable diagnostics and the corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="88479-125">Si vous n’activez pas la journalisation des diagnostics pour un type de ressource en particulier, mais que vous installez la solution, les panneaux du tableau de bord de cette ressource sont vides et affichent un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="88479-125">If you do not enable diagnostic logging for a particular resource type, but install the solution, the dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="88479-126">En janvier 2017, la méthode prise en charge pour envoyer des journaux à Log Analytics à partir d’Application Gateways et de Network Security Groups a été modifiée.</span><span class="sxs-lookup"><span data-stu-id="88479-126">In January 2017, the supported way of sending logs from Application Gateways and Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="88479-127">Si vous voyez la solution **Azure Networking Analytics (déconseillée)**, consultez [Migration à partir de l’ancienne solution Azure Networking](#migrating-from-the-old-networking-analytics-solution) pour connaître les étapes à suivre.</span><span class="sxs-lookup"><span data-stu-id="88479-127">If you see the **Azure Networking Analytics (deprecated)** solution, refer to [migrating from the old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need to follow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="88479-128">Consulter les détails de la collecte de données réseaux Azure</span><span class="sxs-lookup"><span data-stu-id="88479-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="88479-129">Les solutions de gestion de l’analytique Azure Application Gateway et l’analytique Network Security Group collectent des journaux de diagnostic directement à partir d’Azure Application Gateways et Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="88479-129">The Azure Application Gateway analytics and the Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="88479-130">Il n’est pas nécessaire d’écrire les journaux dans le stockage Blob Azure, et aucun agent n’est requis pour la collecte de données.</span><span class="sxs-lookup"><span data-stu-id="88479-130">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="88479-131">Le tableau suivant présente les méthodes de collecte des données et d’autres informations sur le mode de collecte des données pour l’analytique Azure Application Gateway et l’analytique Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="88479-131">The following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and the Network Security Group analytics.</span></span>

| <span data-ttu-id="88479-132">Plateforme</span><span class="sxs-lookup"><span data-stu-id="88479-132">Platform</span></span> | <span data-ttu-id="88479-133">Agent direct</span><span class="sxs-lookup"><span data-stu-id="88479-133">Direct agent</span></span> | <span data-ttu-id="88479-134">Agent Systems Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="88479-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="88479-135">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="88479-135">Azure</span></span> | <span data-ttu-id="88479-136">Operations Manager requis ?</span><span class="sxs-lookup"><span data-stu-id="88479-136">Operations Manager required?</span></span> | <span data-ttu-id="88479-137">Données de l’agent Operations Manager envoyées via un groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="88479-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="88479-138">Fréquence de collecte</span><span class="sxs-lookup"><span data-stu-id="88479-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="88479-139">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="88479-139">Azure</span></span> |  |  |<span data-ttu-id="88479-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="88479-140">&#8226;</span></span> |  |  |<span data-ttu-id="88479-141">si connecté</span><span class="sxs-lookup"><span data-stu-id="88479-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="88479-142">Solution d’analytique Azure Application Gateway dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="88479-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Symbole d’Azure Application Gateway Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="88479-144">Les journaux pris en charge pour les passerelles d’application sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="88479-144">The following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="88479-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="88479-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="88479-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="88479-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="88479-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="88479-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="88479-148">Les métriques prises en charge pour les passerelles d’application sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="88479-148">The following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="88479-149">Débit de 5 minutes</span><span class="sxs-lookup"><span data-stu-id="88479-149">5 minute throughput</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="88479-150">Installer et configurer la solution</span><span class="sxs-lookup"><span data-stu-id="88479-150">Install and configure the solution</span></span>
<span data-ttu-id="88479-151">Pour installer et configurer la solution d’analytique Azure Application Gateway, suivez les instructions suivantes :</span><span class="sxs-lookup"><span data-stu-id="88479-151">Use the following instructions to install and configure the Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="88479-152">Activez la solution Azure Application Gateway Analytics depuis la [Place de marché Microsoft Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) ou en procédant de la manière décrite dans [Ajouter des solutions Log Analytics à partir de la galerie de solutions](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="88479-152">Enable the Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="88479-153">Activez la journalisation des diagnostics pour les [Application Gateways](../application-gateway/application-gateway-diagnostics.md) que vous voulez surveiller.</span><span class="sxs-lookup"><span data-stu-id="88479-153">Enable diagnostics logging for the [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want to monitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-the-portal"></a><span data-ttu-id="88479-154">Activer les diagnostics Azure Application Gateway dans le portail</span><span class="sxs-lookup"><span data-stu-id="88479-154">Enable Azure Application Gateway diagnostics in the portal</span></span>

1. <span data-ttu-id="88479-155">Dans le Portail Azure, accédez à la ressource Application Gateway à surveiller.</span><span class="sxs-lookup"><span data-stu-id="88479-155">In the Azure portal, navigate to the Application Gateway resource to monitor</span></span>
2. <span data-ttu-id="88479-156">Sélectionnez *Journaux de diagnostic* pour ouvrir la page suivante.</span><span class="sxs-lookup"><span data-stu-id="88479-156">Select *Diagnostics logs* to open the following page</span></span>

   ![Image de la ressource Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="88479-158">Cliquez sur *Activer les diagnostics* pour ouvrir la page suivante.</span><span class="sxs-lookup"><span data-stu-id="88479-158">Click *Turn on diagnostics* to open the following page</span></span>

   ![Image de la ressource Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="88479-160">Pour activer les diagnostics, cliquez sur *Activé* sous *État*.</span><span class="sxs-lookup"><span data-stu-id="88479-160">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="88479-161">Cochez la case à côté de l’option *Envoyer à Log Analytics*.</span><span class="sxs-lookup"><span data-stu-id="88479-161">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="88479-162">Sélectionnez un espace de travail Log Analytics existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="88479-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="88479-163">Cochez la case sous **Journal** pour chacun des types de journaux à collecter.</span><span class="sxs-lookup"><span data-stu-id="88479-163">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="88479-164">Cliquez sur *Enregistrer* pour activer la journalisation des diagnostics dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="88479-164">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="88479-165">Activez les diagnostics de réseau Azure avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="88479-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="88479-166">Le script PowerShell suivant fournit un exemple montrant comment activer la journalisation des diagnostics pour les Application Gateways.</span><span class="sxs-lookup"><span data-stu-id="88479-166">The following PowerShell script provides an example of how to enable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="88479-167">Utiliser l’analytique Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="88479-167">Use Azure Application Gateway analytics</span></span>
![Image de la mosaïque d’analytique Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="88479-169">Une fois que vous avez cliqué sur la mosaïque **d’analytique Azure Application Gateway** dans la Vue d’ensemble, vous pouvez consulter les résumés de vos journaux et entrer dans les détails des catégories suivantes :</span><span class="sxs-lookup"><span data-stu-id="88479-169">After you click the **Azure Application Gateway analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="88479-170">Journaux d’accès à la passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="88479-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="88479-171">Erreurs client et serveur pour les journaux d’accès à la passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="88479-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="88479-172">Nombre de demandes par heure pour chaque passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="88479-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="88479-173">Nombre d’échecs de demande par heure pour chaque passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="88479-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="88479-174">Erreurs de l’agent utilisateur pour les passerelles d’application</span><span class="sxs-lookup"><span data-stu-id="88479-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="88479-175">Performances de la passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="88479-175">Application Gateway performance</span></span>
  * <span data-ttu-id="88479-176">Intégrité de l’hôte pour la passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="88479-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="88479-177">Nombre maximal et 95e centile pour les échecs de demande de passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="88479-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![Image du tableau de bord d’analytique Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Image du tableau de bord d’analytique Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="88479-180">Sur le tableau de bord **d’analytique Azure Application Gateway**, consultez les informations du résumé dans l’un des panneaux, puis cliquez sur l’un d’entre eux pour afficher des informations détaillées sur la page de recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="88479-180">On the **Azure Application Gateway analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="88479-181">Sur l’une des pages de recherche de journal, vous pouvez afficher les résultats par date, les résultats détaillés et votre historique de recherches de journaux.</span><span class="sxs-lookup"><span data-stu-id="88479-181">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="88479-182">Vous pouvez également filtrer par facettes pour affiner les résultats.</span><span class="sxs-lookup"><span data-stu-id="88479-182">You can also filter by facets to narrow the results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="88479-183">Solution d’analytique Azure Network Security Group dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="88479-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Symbole d’Azure Network Security Group Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="88479-185">Les fichiers journaux suivants sont pris en charge pour les groupes de sécurité réseau :</span><span class="sxs-lookup"><span data-stu-id="88479-185">The following logs are supported for network security groups:</span></span>

* <span data-ttu-id="88479-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="88479-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="88479-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="88479-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="88479-188">Installer et configurer la solution</span><span class="sxs-lookup"><span data-stu-id="88479-188">Install and configure the solution</span></span>
<span data-ttu-id="88479-189">Pour installer et configurer la solution d’analytique du réseau Azure, suivez les instructions suivantes :</span><span class="sxs-lookup"><span data-stu-id="88479-189">Use the following instructions to install and configure the Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="88479-190">Activez la solution Azure Network Security Group Analytics depuis la [Place de marché Microsoft Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) ou en procédant de la manière décrite dans [Ajouter des solutions Log Analytics à partir de la galerie de solutions](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="88479-190">Enable the Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="88479-191">Activez la journalisation des diagnostics pour les ressources [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) que vous voulez surveiller.</span><span class="sxs-lookup"><span data-stu-id="88479-191">Enable diagnostics logging for the [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want to monitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-the-portal"></a><span data-ttu-id="88479-192">Activer les diagnostics Azure Network Security Group dans le portail</span><span class="sxs-lookup"><span data-stu-id="88479-192">Enable Azure network security group diagnostics in the portal</span></span>

1. <span data-ttu-id="88479-193">Dans le Portail Azure, accédez à la ressource Network Security Group à surveiller.</span><span class="sxs-lookup"><span data-stu-id="88479-193">In the Azure portal, navigate to the Network Security Group resource to monitor</span></span>
2. <span data-ttu-id="88479-194">Sélectionnez *Journaux de diagnostic* pour ouvrir la page suivante.</span><span class="sxs-lookup"><span data-stu-id="88479-194">Select *Diagnostics logs* to open the following page</span></span>

   ![Image de la ressource Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="88479-196">Cliquez sur *Activer les diagnostics* pour ouvrir la page suivante.</span><span class="sxs-lookup"><span data-stu-id="88479-196">Click *Turn on diagnostics* to open the following page</span></span>

   ![Image de la ressource Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="88479-198">Pour activer les diagnostics, cliquez sur *Activé* sous *État*.</span><span class="sxs-lookup"><span data-stu-id="88479-198">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="88479-199">Cochez la case à côté de l’option *Envoyer à Log Analytics*.</span><span class="sxs-lookup"><span data-stu-id="88479-199">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="88479-200">Sélectionnez un espace de travail Log Analytics existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="88479-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="88479-201">Cochez la case sous **Journal** pour chacun des types de journaux à collecter.</span><span class="sxs-lookup"><span data-stu-id="88479-201">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="88479-202">Cliquez sur *Enregistrer* pour activer la journalisation des diagnostics dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="88479-202">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="88479-203">Activez les diagnostics de réseau Azure avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="88479-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="88479-204">Le script PowerShell suivant fournit un exemple montrant comment activer la journalisation des diagnostics pour les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="88479-204">The following PowerShell script provides an example of how to enable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="88479-205">Utiliser l’analytique Azure Network Security Group</span><span class="sxs-lookup"><span data-stu-id="88479-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="88479-206">Une fois que vous avez cliqué sur la mosaïque **d’analytique Azure Network Security Group** dans la Vue d’ensemble, vous pouvez consulter les résumés de vos journaux et entrer dans les détails des catégories suivantes :</span><span class="sxs-lookup"><span data-stu-id="88479-206">After you click the **Azure Network Security Group analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="88479-207">Flux bloqués de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="88479-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="88479-208">Règles de groupe de sécurité réseau avec flux bloqués</span><span class="sxs-lookup"><span data-stu-id="88479-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="88479-209">Adresses MAC avec flux bloqués</span><span class="sxs-lookup"><span data-stu-id="88479-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="88479-210">Flux autorisés de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="88479-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="88479-211">Règles de groupe de sécurité réseau avec flux autorisés</span><span class="sxs-lookup"><span data-stu-id="88479-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="88479-212">Adresses MAC avec flux autorisés</span><span class="sxs-lookup"><span data-stu-id="88479-212">MAC addresses with allowed flows</span></span>

![Image du tableau de bord d’analytique Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Image du tableau de bord d’analytique Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="88479-215">Sur le tableau de bord **d’analytique Azure Network Security Group**, consultez les informations du résumé dans l’un des panneaux, puis cliquez sur l’un d’entre eux pour afficher des informations détaillées sur la page de recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="88479-215">On the **Azure Network Security Group analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="88479-216">Sur l’une des pages de recherche de journal, vous pouvez afficher les résultats par date, les résultats détaillés et votre historique de recherches de journaux.</span><span class="sxs-lookup"><span data-stu-id="88479-216">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="88479-217">Vous pouvez également filtrer par facettes pour affiner les résultats.</span><span class="sxs-lookup"><span data-stu-id="88479-217">You can also filter by facets to narrow the results.</span></span>

## <a name="migrating-from-the-old-networking-analytics-solution"></a><span data-ttu-id="88479-218">Migration à partir de l’ancienne solution Azure Networking</span><span class="sxs-lookup"><span data-stu-id="88479-218">Migrating from the old Networking Analytics solution</span></span>
<span data-ttu-id="88479-219">En janvier 2017, la méthode prise en charge pour envoyer des journaux à Log Analytics à partir d’Azure Application Gateways et Azure Network Security Groups a été modifiée.</span><span class="sxs-lookup"><span data-stu-id="88479-219">In January 2017, the supported way of sending logs from Azure Application Gateways and Azure Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="88479-220">Ces modifications présentent les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="88479-220">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="88479-221">Les journaux sont écrits directement dans Log Analytics sans avoir besoin d’utiliser un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="88479-221">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="88479-222">La durée de latence est plus courte entre le moment où les journaux sont générés et celui où ils deviennent disponibles dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="88479-222">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="88479-223">Le nombre d’étapes de configuration est réduit.</span><span class="sxs-lookup"><span data-stu-id="88479-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="88479-224">Tous les types de diagnostics Azure sont au même format.</span><span class="sxs-lookup"><span data-stu-id="88479-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="88479-225">Pour utiliser les solutions mises à jour :</span><span class="sxs-lookup"><span data-stu-id="88479-225">To use the updated solutions:</span></span>

1. <span data-ttu-id="88479-226">[Configurez les diagnostics pour qu’ils soient directement envoyés à Log Analytics à partir d’Azure Application Gateways](#enable-azure-application-gateway-diagnostics-in-the-portal).</span><span class="sxs-lookup"><span data-stu-id="88479-226">[Configure diagnostics to be sent directly to Log Analytics from Azure Application Gateways](#enable-azure-application-gateway-diagnostics-in-the-portal)</span></span>
2. <span data-ttu-id="88479-227">[Configurez les diagnostics pour qu’ils soient directement envoyés à Log Analytics à partir d’Azure Network Security Groups](#enable-azure-network-security-group-diagnostics-in-the-portal).</span><span class="sxs-lookup"><span data-stu-id="88479-227">[Configure diagnostics to be sent directly to Log Analytics from Azure Network Security Groups](#enable-azure-network-security-group-diagnostics-in-the-portal)</span></span>
2. <span data-ttu-id="88479-228">Activez la solution *d’analytique Azure Application Gateway* et *d’analytique Azure Network Security Group* en procédant de la manière décrite dans [Ajouter des solutions Log Analytics à partir de la galerie de solutions](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="88479-228">Enable the *Azure Application Gateway Analytics* and the *Azure Network Security Group Analytics* solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="88479-229">Mettez à jour les requêtes, les tableaux de bord et les alertes enregistrés pour qu’ils utilisent le nouveau type de données.</span><span class="sxs-lookup"><span data-stu-id="88479-229">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="88479-230">Le type doit être AzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="88479-230">Type is to AzureDiagnostics.</span></span> <span data-ttu-id="88479-231">Vous pouvez utiliser ResourceType pour filtrer les journaux réseaux Azure.</span><span class="sxs-lookup"><span data-stu-id="88479-231">You can use the ResourceType to filter to Azure networking logs.</span></span>

    | <span data-ttu-id="88479-232">Au lieu du paramètre...</span><span class="sxs-lookup"><span data-stu-id="88479-232">Instead of:</span></span> | <span data-ttu-id="88479-233">Utilisez :</span><span class="sxs-lookup"><span data-stu-id="88479-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="88479-234">Pour tous les champs dont le suffixe est \_s, \_d ou \_g, remplacez le premier caractère du nom par une lettre minuscule.</span><span class="sxs-lookup"><span data-stu-id="88479-234">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
   + <span data-ttu-id="88479-235">Pour tous les champs dont le suffixe est \_o, les données sont réparties en plusieurs champs, selon les noms de champs imbriqués.</span><span class="sxs-lookup"><span data-stu-id="88479-235">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span>
4. <span data-ttu-id="88479-236">Supprimez la solution *Azure Networking Analytics (déconseillée)*.</span><span class="sxs-lookup"><span data-stu-id="88479-236">Remove the *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="88479-237">Si vous utilisez PowerShell, utilisez `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`.</span><span class="sxs-lookup"><span data-stu-id="88479-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="88479-238">Les données collectées avant la modification ne seront pas visibles dans la nouvelle solution.</span><span class="sxs-lookup"><span data-stu-id="88479-238">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="88479-239">Vous pouvez continuer à interroger ces données à l’aide de l’ancien type et des anciens noms de champs.</span><span class="sxs-lookup"><span data-stu-id="88479-239">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="88479-240">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="88479-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="88479-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="88479-241">Next steps</span></span>
* <span data-ttu-id="88479-242">Utilisez les [Recherches dans les journaux dans Log Analytics](log-analytics-log-searches.md) pour afficher les données détaillées de diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="88479-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure diagnostics data.</span></span>
