---
title: "aaaAzure solution Analytique de mise en réseau dans le journal Analytique | Documents Microsoft"
description: "Vous pouvez utiliser hello solution Analytique de mise en réseau Azure dans les journaux du groupe de sécurité Analytique de journal tooreview réseau Azure et les journaux de la passerelle d’Application Azure."
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
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="8af1c-103">Solutions d’analyse réseaux Azure dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8af1c-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="8af1c-104">Analytique de journal offre hello suivant des solutions pour l’analyse de vos réseaux :</span><span class="sxs-lookup"><span data-stu-id="8af1c-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="8af1c-105">Analyseur de performances réseau (NPM) pour</span><span class="sxs-lookup"><span data-stu-id="8af1c-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="8af1c-106">Surveiller la santé de votre réseau hello</span><span class="sxs-lookup"><span data-stu-id="8af1c-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="8af1c-107">Azure tooreview analytique de passerelle d’Application</span><span class="sxs-lookup"><span data-stu-id="8af1c-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="8af1c-108">Journaux Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8af1c-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="8af1c-109">Mesures Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8af1c-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="8af1c-110">Groupe de sécurité réseau Azure analytique tooreview</span><span class="sxs-lookup"><span data-stu-id="8af1c-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="8af1c-111">Journaux Azure Network Security Group</span><span class="sxs-lookup"><span data-stu-id="8af1c-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="8af1c-112">Analyseur de performances réseau (NPM)</span><span class="sxs-lookup"><span data-stu-id="8af1c-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="8af1c-113">Hello [analyse des performances réseau](log-analytics-network-performance-monitor.md) solution de gestion est un solution, qui surveille l’intégrité de hello, la disponibilité et l’accessibilité des réseaux d’analyse de réseau.</span><span class="sxs-lookup"><span data-stu-id="8af1c-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="8af1c-114">Il existe une connectivité toomonitor utilisé entre :</span><span class="sxs-lookup"><span data-stu-id="8af1c-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="8af1c-115">le cloud public et le site local ;</span><span class="sxs-lookup"><span data-stu-id="8af1c-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="8af1c-116">les centres de données et les emplacements des utilisateurs (filiales) ;</span><span class="sxs-lookup"><span data-stu-id="8af1c-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="8af1c-117">les sous-réseaux hébergeant différents niveaux d’une application multiniveau.</span><span class="sxs-lookup"><span data-stu-id="8af1c-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="8af1c-118">Pour plus d’informations, consultez l’[Analyseur de performances réseau](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="8af1c-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="8af1c-119">Azure Application Gateway et Network Security Group Analytics</span><span class="sxs-lookup"><span data-stu-id="8af1c-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="8af1c-120">solutions de hello toouse :</span><span class="sxs-lookup"><span data-stu-id="8af1c-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="8af1c-121">Ajouter tooLog de solution de gestion hello Analytique, et</span><span class="sxs-lookup"><span data-stu-id="8af1c-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="8af1c-122">Activer les diagnostics toodirect hello diagnostics tooa Analytique de journal espace de travail.</span><span class="sxs-lookup"><span data-stu-id="8af1c-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="8af1c-123">Il n’est pas le stockage Blob tooAzure toowrite nécessaire hello journaux.</span><span class="sxs-lookup"><span data-stu-id="8af1c-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="8af1c-124">Vous pouvez activer les diagnostics et les solutions correspondantes hello pour un ou deux de la passerelle d’Application et les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8af1c-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="8af1c-125">Si vous n’activez pas la journalisation des diagnostics pour un type particulier, mais que vous installez hello solution, panneaux de tableau de bord hello pour cette ressource est vides et affiche un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="8af1c-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="8af1c-126">En janvier 2017, hello pris en charge la façon d’envoi de journaux à partir des passerelles d’Application et les groupes de sécurité réseau tooLog que Analytique modifié.</span><span class="sxs-lookup"><span data-stu-id="8af1c-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="8af1c-127">Si vous voyez hello **Analytique de mise en réseau Azure (déconseillée)** solution, consultez trop[migration à partir de l’ancienne solution de mise en réseau d’Analytique hello](#migrating-from-the-old-networking-analytics-solution) pour connaître les étapes, vous devez toofollow.</span><span class="sxs-lookup"><span data-stu-id="8af1c-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="8af1c-128">Consulter les détails de la collecte de données réseaux Azure</span><span class="sxs-lookup"><span data-stu-id="8af1c-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="8af1c-129">analytique de passerelle d’Application Azure Hello et solutions de gestion d’analytique de groupe de sécurité réseau hello collecter les journaux de diagnostics directement à partir des passerelles d’Application Azure et les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8af1c-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="8af1c-130">Il n’est pas nécessaire de toowrite hello journaux tooAzure stockage d’objets Blob et aucun agent n’est requise pour la collection de données.</span><span class="sxs-lookup"><span data-stu-id="8af1c-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="8af1c-131">Hello tableau suivant présente les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour l’analytique de la passerelle d’Application Azure et analytique de groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="8af1c-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="8af1c-132">Plateforme</span><span class="sxs-lookup"><span data-stu-id="8af1c-132">Platform</span></span> | <span data-ttu-id="8af1c-133">Agent direct</span><span class="sxs-lookup"><span data-stu-id="8af1c-133">Direct agent</span></span> | <span data-ttu-id="8af1c-134">Agent Systems Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="8af1c-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="8af1c-135">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8af1c-135">Azure</span></span> | <span data-ttu-id="8af1c-136">Operations Manager requis ?</span><span class="sxs-lookup"><span data-stu-id="8af1c-136">Operations Manager required?</span></span> | <span data-ttu-id="8af1c-137">Données de l’agent Operations Manager envoyées via un groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="8af1c-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="8af1c-138">Fréquence de collecte</span><span class="sxs-lookup"><span data-stu-id="8af1c-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8af1c-139">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8af1c-139">Azure</span></span> |  |  |<span data-ttu-id="8af1c-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="8af1c-140">&#8226;</span></span> |  |  |<span data-ttu-id="8af1c-141">si connecté</span><span class="sxs-lookup"><span data-stu-id="8af1c-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="8af1c-142">Solution d’analytique Azure Application Gateway dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8af1c-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Symbole d’Azure Application Gateway Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="8af1c-144">Hello suivant les journaux est pris en charge pour les passerelles d’Application :</span><span class="sxs-lookup"><span data-stu-id="8af1c-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="8af1c-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="8af1c-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="8af1c-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="8af1c-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="8af1c-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="8af1c-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="8af1c-148">Hello suit les mesures est prises en charge pour les passerelles d’Application :</span><span class="sxs-lookup"><span data-stu-id="8af1c-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="8af1c-149">Débit de 5 minutes</span><span class="sxs-lookup"><span data-stu-id="8af1c-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="8af1c-150">Installer et configurer une solution de hello</span><span class="sxs-lookup"><span data-stu-id="8af1c-150">Install and configure hello solution</span></span>
<span data-ttu-id="8af1c-151">Utilisez hello suivant les instructions tooinstall et configurer une solution d’analytique hello passerelle d’Application Azure :</span><span class="sxs-lookup"><span data-stu-id="8af1c-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="8af1c-152">Activer la solution d’analytique de passerelle d’Application Azure hello à partir de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="8af1c-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="8af1c-153">Activer la journalisation des diagnostics pour hello [passerelles d’Application](../application-gateway/application-gateway-diagnostics.md) vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="8af1c-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="8af1c-154">Activer les diagnostics de passerelle d’Application Azure dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="8af1c-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="8af1c-155">Bonjour portail Azure, accédez à toomonitor de ressources toohello Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8af1c-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="8af1c-156">Sélectionnez *les journaux de diagnostic* hello tooopen suivant page</span><span class="sxs-lookup"><span data-stu-id="8af1c-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Image de la ressource Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="8af1c-158">Cliquez sur *activer les diagnostics* hello tooopen suivant page</span><span class="sxs-lookup"><span data-stu-id="8af1c-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Image de la ressource Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="8af1c-160">tooturn des diagnostics, cliquez sur *sur* sous *état*</span><span class="sxs-lookup"><span data-stu-id="8af1c-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="8af1c-161">Cliquez sur la case à cocher hello *envoyer tooLog Analytique*</span><span class="sxs-lookup"><span data-stu-id="8af1c-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="8af1c-162">Sélectionnez un espace de travail Log Analytics existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="8af1c-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="8af1c-163">Cliquez sur la case à cocher hello sous **journal** pour chacun des toocollect de types hello journal</span><span class="sxs-lookup"><span data-stu-id="8af1c-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="8af1c-164">Cliquez sur *enregistrer* tooenable la journalisation hello de diagnostics tooLog Analytique</span><span class="sxs-lookup"><span data-stu-id="8af1c-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="8af1c-165">Activez les diagnostics de réseau Azure avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="8af1c-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="8af1c-166">Hello PowerShell script suivant fournit un exemple de procédure tooenable journalisation des diagnostics pour les passerelles d’application.</span><span class="sxs-lookup"><span data-stu-id="8af1c-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="8af1c-167">Utiliser l’analytique Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8af1c-167">Use Azure Application Gateway analytics</span></span>
![Image de la mosaïque d’analytique Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="8af1c-169">Après avoir cliqué sur hello **analytique de la passerelle d’Application Azure** vignette sur hello vue d’ensemble, vous pouvez afficher des synthèses de vos journaux et procéder dans toodetails pour hello suivant des catégories :</span><span class="sxs-lookup"><span data-stu-id="8af1c-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="8af1c-170">Journaux d’accès à la passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="8af1c-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="8af1c-171">Erreurs client et serveur pour les journaux d’accès à la passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="8af1c-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="8af1c-172">Nombre de demandes par heure pour chaque passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="8af1c-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="8af1c-173">Nombre d’échecs de demande par heure pour chaque passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="8af1c-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="8af1c-174">Erreurs de l’agent utilisateur pour les passerelles d’application</span><span class="sxs-lookup"><span data-stu-id="8af1c-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="8af1c-175">Performances de la passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="8af1c-175">Application Gateway performance</span></span>
  * <span data-ttu-id="8af1c-176">Intégrité de l’hôte pour la passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="8af1c-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="8af1c-177">Nombre maximal et 95e centile pour les échecs de demande de passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="8af1c-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![Image du tableau de bord d’analytique Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Image du tableau de bord d’analytique Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="8af1c-180">Sur hello **analytique de la passerelle d’Application Azure** tableau de bord, passez en revue les informations de résumé hello dans un des panneaux de hello, puis cliquez sur une tooview des informations détaillées sur page de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="8af1c-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="8af1c-181">Sur les pages de recherche de journal hello, vous pouvez afficher les résultats par heure, les résultats détaillés et votre historique de recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="8af1c-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="8af1c-182">Vous pouvez également filtrer selon les résultats de facettes toonarrow hello.</span><span class="sxs-lookup"><span data-stu-id="8af1c-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="8af1c-183">Solution d’analytique Azure Network Security Group dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8af1c-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Symbole d’Azure Network Security Group Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="8af1c-185">Hello suivant des journaux est pris en charge pour les groupes de sécurité réseau :</span><span class="sxs-lookup"><span data-stu-id="8af1c-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="8af1c-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="8af1c-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="8af1c-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="8af1c-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="8af1c-188">Installer et configurer une solution de hello</span><span class="sxs-lookup"><span data-stu-id="8af1c-188">Install and configure hello solution</span></span>
<span data-ttu-id="8af1c-189">Utilisez hello suivant les instructions tooinstall et configurer une solution d’Analytique de mise en réseau Azure hello :</span><span class="sxs-lookup"><span data-stu-id="8af1c-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="8af1c-190">Activer la solution d’analytique de groupe de sécurité réseau Azure hello à partir de [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="8af1c-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="8af1c-191">Activer la journalisation des diagnostics pour hello [groupe de sécurité réseau](../virtual-network/virtual-network-nsg-manage-log.md) ressources toomonitor.</span><span class="sxs-lookup"><span data-stu-id="8af1c-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="8af1c-192">Activer les diagnostics de groupe de sécurité réseau Azure dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="8af1c-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="8af1c-193">Bonjour portail Azure, accédez à toomonitor de ressource de groupe de sécurité réseau toohello</span><span class="sxs-lookup"><span data-stu-id="8af1c-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="8af1c-194">Sélectionnez *les journaux de diagnostic* hello tooopen suivant page</span><span class="sxs-lookup"><span data-stu-id="8af1c-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Image de la ressource Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="8af1c-196">Cliquez sur *activer les diagnostics* hello tooopen suivant page</span><span class="sxs-lookup"><span data-stu-id="8af1c-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Image de la ressource Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="8af1c-198">tooturn des diagnostics, cliquez sur *sur* sous *état*</span><span class="sxs-lookup"><span data-stu-id="8af1c-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="8af1c-199">Cliquez sur la case à cocher hello *envoyer tooLog Analytique*</span><span class="sxs-lookup"><span data-stu-id="8af1c-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="8af1c-200">Sélectionnez un espace de travail Log Analytics existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="8af1c-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="8af1c-201">Cliquez sur la case à cocher hello sous **journal** pour chacun des toocollect de types hello journal</span><span class="sxs-lookup"><span data-stu-id="8af1c-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="8af1c-202">Cliquez sur *enregistrer* tooenable la journalisation hello de diagnostics tooLog Analytique</span><span class="sxs-lookup"><span data-stu-id="8af1c-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="8af1c-203">Activez les diagnostics de réseau Azure avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="8af1c-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="8af1c-204">Hello PowerShell script suivant fournit un exemple de procédure tooenable journalisation des diagnostics pour les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="8af1c-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="8af1c-205">Utiliser l’analytique Azure Network Security Group</span><span class="sxs-lookup"><span data-stu-id="8af1c-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="8af1c-206">Après avoir cliqué sur hello **analytique de groupe de sécurité réseau Azure** vignette sur hello vue d’ensemble, vous pouvez afficher des synthèses de vos journaux et procéder dans toodetails pour hello suivant des catégories :</span><span class="sxs-lookup"><span data-stu-id="8af1c-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="8af1c-207">Flux bloqués de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="8af1c-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="8af1c-208">Règles de groupe de sécurité réseau avec flux bloqués</span><span class="sxs-lookup"><span data-stu-id="8af1c-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="8af1c-209">Adresses MAC avec flux bloqués</span><span class="sxs-lookup"><span data-stu-id="8af1c-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="8af1c-210">Flux autorisés de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="8af1c-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="8af1c-211">Règles de groupe de sécurité réseau avec flux autorisés</span><span class="sxs-lookup"><span data-stu-id="8af1c-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="8af1c-212">Adresses MAC avec flux autorisés</span><span class="sxs-lookup"><span data-stu-id="8af1c-212">MAC addresses with allowed flows</span></span>

![Image du tableau de bord d’analytique Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Image du tableau de bord d’analytique Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="8af1c-215">Sur hello **analytique de groupe de sécurité réseau Azure** tableau de bord, passez en revue les informations de résumé hello dans un des panneaux de hello, puis cliquez sur une tooview des informations détaillées sur page de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="8af1c-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="8af1c-216">Sur les pages de recherche de journal hello, vous pouvez afficher les résultats par heure, les résultats détaillés et votre historique de recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="8af1c-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="8af1c-217">Vous pouvez également filtrer selon les résultats de facettes toonarrow hello.</span><span class="sxs-lookup"><span data-stu-id="8af1c-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="8af1c-218">Migration à partir de l’ancienne solution de mise en réseau d’Analytique hello</span><span class="sxs-lookup"><span data-stu-id="8af1c-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="8af1c-219">En janvier 2017, hello pris en charge la façon d’envoi de journaux à partir des passerelles d’Application Azure et les groupes de sécurité de réseau Azure tooLog que Analytique modifié.</span><span class="sxs-lookup"><span data-stu-id="8af1c-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="8af1c-220">Ces modifications permettent de hello suivant avantages :</span><span class="sxs-lookup"><span data-stu-id="8af1c-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="8af1c-221">Les journaux sont écrits directement tooLog Analytique sans hello devez toouse un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="8af1c-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="8af1c-222">Latence est faible à partir de l’heure hello lorsque les journaux sont générés toothem soient disponibles dans le journal Analytique</span><span class="sxs-lookup"><span data-stu-id="8af1c-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="8af1c-223">Le nombre d’étapes de configuration est réduit.</span><span class="sxs-lookup"><span data-stu-id="8af1c-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="8af1c-224">Tous les types de diagnostics Azure sont au même format.</span><span class="sxs-lookup"><span data-stu-id="8af1c-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="8af1c-225">solutions toouse hello mis à jour :</span><span class="sxs-lookup"><span data-stu-id="8af1c-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="8af1c-226">Configurer toobe diagnostics provenant directement tooLog Analytique passerelles d’Application Azure</span><span class="sxs-lookup"><span data-stu-id="8af1c-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="8af1c-227">Configurer toobe diagnostics envoyé des tooLog Analytique directement à partir de groupes de sécurité réseau Azure</span><span class="sxs-lookup"><span data-stu-id="8af1c-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="8af1c-228">Activer hello *Analytique de passerelle d’Application Azure* et hello *Analytique de groupe de sécurité de réseau Azure* solution à l’aide du processus de hello décrit dans [solutions Analytique de journal ajouter à partir de Hello galerie de Solutions](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="8af1c-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="8af1c-229">Mettre à jour toutes les requêtes enregistrées, les tableaux de bord ou les alertes toouse hello nouveau type de données</span><span class="sxs-lookup"><span data-stu-id="8af1c-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="8af1c-230">Le type est tooAzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="8af1c-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="8af1c-231">Vous pouvez utiliser hello ResourceType toofilter tooAzure mise en réseau des journaux.</span><span class="sxs-lookup"><span data-stu-id="8af1c-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="8af1c-232">Au lieu du paramètre...</span><span class="sxs-lookup"><span data-stu-id="8af1c-232">Instead of:</span></span> | <span data-ttu-id="8af1c-233">Utilisez :</span><span class="sxs-lookup"><span data-stu-id="8af1c-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="8af1c-234">Pour un champ qui comporte un suffixe de \_s, \_d, ou \_g dans nom hello, modification hello premier caractère toolower cas</span><span class="sxs-lookup"><span data-stu-id="8af1c-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="8af1c-235">Pour un champ qui comporte un suffixe de \_o dans nom, les données de salutation est divisé en champs individuels en fonction du nom de champ hello imbriqué.</span><span class="sxs-lookup"><span data-stu-id="8af1c-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="8af1c-236">Supprimer hello *Analytique de mise en réseau Azure (obsolète)* solution.</span><span class="sxs-lookup"><span data-stu-id="8af1c-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="8af1c-237">Avec PowerShell, utilisez `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`.</span><span class="sxs-lookup"><span data-stu-id="8af1c-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="8af1c-238">Les données collectées avant la modification de hello n’est pas visible dans une nouvelle solution hello.</span><span class="sxs-lookup"><span data-stu-id="8af1c-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="8af1c-239">Vous pouvez continuer tooquery pour cette à l’aide de données hello ancien Type et les noms de champs.</span><span class="sxs-lookup"><span data-stu-id="8af1c-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8af1c-240">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="8af1c-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="8af1c-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8af1c-241">Next steps</span></span>
* <span data-ttu-id="8af1c-242">Utilisez [connecter recherche Analytique de journal](log-analytics-log-searches.md) tooview détaillées des données de diagnostic Azure.</span><span class="sxs-lookup"><span data-stu-id="8af1c-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
