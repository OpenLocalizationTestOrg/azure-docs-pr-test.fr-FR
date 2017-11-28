---
title: "tooresource aaaIntroduction résolution des problèmes dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de capacités de dépannage de ressource hello Observateur réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="c7bd5-103">Tooresource présentation résolution des problèmes dans l’Observateur réseau de Azure</span><span class="sxs-lookup"><span data-stu-id="c7bd5-103">Introduction tooresource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="c7bd5-104">Les passerelles de réseau virtuel assurent une connectivité entre les ressources locales et d’autres réseaux virtuels dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="c7bd5-105">Les passerelles et les connexions d’analyse est critique tooensuring communication n’est pas interrompue.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-105">Monitoring these gateways and their Connections is critical tooensuring communication is not broken.</span></span> <span data-ttu-id="c7bd5-106">Observateur réseau fournit hello capacité tootroubleshoot les connexions et les passerelles de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-106">Network Watcher provides hello capability tootroubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="c7bd5-107">Il peut être appelé via le portail de hello, PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-107">This can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="c7bd5-108">Lorsqu’elle est appelée, Observateur réseau permet de diagnostiquer la santé de passerelle de réseau virtuel hello ou de connexion et les résultats appropriés hello retour hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-108">When called, Network Watcher diagnoses hello health of hello virtual network gateway or connection and return hello appropriate results.</span></span> <span data-ttu-id="c7bd5-109">Cette demande est une transaction longue, hello résultats une fois le diagnostic de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-109">This request is a long running transaction, hello results are returned once hello diagnosis is complete.</span></span>

![portail][2]

## <a name="results"></a><span data-ttu-id="c7bd5-111">Résultats</span><span class="sxs-lookup"><span data-stu-id="c7bd5-111">Results</span></span>

<span data-ttu-id="c7bd5-112">Hello préliminaire résultats donnent une vue d’ensemble de la santé de ressource de hello hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-112">hello preliminary results returned give an overall picture of hello health of hello resource.</span></span> <span data-ttu-id="c7bd5-113">Informations plus approfondies peuvent être fournies pour les ressources comme indiqué dans hello suivant la section :</span><span class="sxs-lookup"><span data-stu-id="c7bd5-113">Deeper information can be provided for resources as shown in hello following section:</span></span>

<span data-ttu-id="c7bd5-114">Hello Voici les valeurs hello retournées par hello résoudre les problèmes d’API :</span><span class="sxs-lookup"><span data-stu-id="c7bd5-114">hello following list is hello values returned with hello troubleshoot API:</span></span>

* <span data-ttu-id="c7bd5-115">**startTime** -cette valeur est le temps hello hello résoudre les problèmes d’appel de l’API a démarré.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-115">**startTime** - This value is hello time hello troubleshoot API call started.</span></span>
* <span data-ttu-id="c7bd5-116">**heure de fin** -cette valeur est l’heure de hello hello dépannage fin.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-116">**endTime** - This value is hello time when hello troubleshooting ended.</span></span>
* <span data-ttu-id="c7bd5-117">**code** : la valeur est définie sur UnHealthy en cas d’échec du diagnostic.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="c7bd5-118">**résultats** -résultats est une collection de résultats retournés sur la passerelle de réseau virtuel de connexion ou hello hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-118">**results** - Results is a collection of results returned on hello Connection or hello virtual network gateway.</span></span>
    * <span data-ttu-id="c7bd5-119">**ID** -cette valeur est le type d’erreur hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-119">**id** - This value is hello fault type.</span></span>
    * <span data-ttu-id="c7bd5-120">**Résumé** -cette valeur est un résumé des pannes de hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-120">**summary** - This value is a summary of hello fault.</span></span>
    * <span data-ttu-id="c7bd5-121">**détaillées** -cette valeur fournit une description détaillée de l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-121">**detailed** - This value provides a detailed description of hello fault.</span></span>
    * <span data-ttu-id="c7bd5-122">**recommendedActions** -cette propriété est une collection d’actions recommandées tootake.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-122">**recommendedActions** - This property is a collection of recommended actions tootake.</span></span>
      * <span data-ttu-id="c7bd5-123">**actionText** -cette valeur contient le texte hello décrivant le tootake action.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-123">**actionText** - This value contains hello text describing what action tootake.</span></span>
      * <span data-ttu-id="c7bd5-124">**actionUri** -cette valeur fournit des hello URI toodocumentation tooact.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-124">**actionUri** - This value provides hello URI toodocumentation on how tooact.</span></span>
      * <span data-ttu-id="c7bd5-125">**actionUriText** -cette valeur est une brève description de texte d’action hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-125">**actionUriText** - This value is a short description of hello action text.</span></span>

<span data-ttu-id="c7bd5-126">Hello suivant tables afficher hello différents types d’erreurs (id de sous les résultats à partir de hello précédant la liste) qui sont disponibles et si les pannes hello créent des journaux.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-126">hello following tables show hello different fault types (id under results from hello preceding list) that are available and if hello fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="c7bd5-127">Passerelle</span><span class="sxs-lookup"><span data-stu-id="c7bd5-127">Gateway</span></span>

| <span data-ttu-id="c7bd5-128">Type d’erreur</span><span class="sxs-lookup"><span data-stu-id="c7bd5-128">Fault Type</span></span> | <span data-ttu-id="c7bd5-129">Motif</span><span class="sxs-lookup"><span data-stu-id="c7bd5-129">Reason</span></span> | <span data-ttu-id="c7bd5-130">Journal</span><span class="sxs-lookup"><span data-stu-id="c7bd5-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="c7bd5-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="c7bd5-131">NoFault</span></span> | <span data-ttu-id="c7bd5-132">Quand aucune erreur n’est détectée.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-132">When no error is detected.</span></span> |<span data-ttu-id="c7bd5-133">Oui</span><span class="sxs-lookup"><span data-stu-id="c7bd5-133">Yes</span></span>|
| <span data-ttu-id="c7bd5-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="c7bd5-134">GatewayNotFound</span></span> | <span data-ttu-id="c7bd5-135">Passerelle introuvable ou non approvisionnée.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="c7bd5-136">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-136">No</span></span>|
| <span data-ttu-id="c7bd5-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="c7bd5-137">PlannedMaintenance</span></span> |  <span data-ttu-id="c7bd5-138">Instance de passerelle en maintenance.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="c7bd5-139">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-139">No</span></span>|
| <span data-ttu-id="c7bd5-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="c7bd5-140">UserDrivenUpdate</span></span> | <span data-ttu-id="c7bd5-141">Quand une mise à jour utilisateur est en cours.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-141">When a user update is in progress.</span></span> <span data-ttu-id="c7bd5-142">Il peut s’agir d’une opération de redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-142">This could be a resize operation.</span></span> | <span data-ttu-id="c7bd5-143">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-143">No</span></span> |
| <span data-ttu-id="c7bd5-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="c7bd5-144">VipUnResponsive</span></span> | <span data-ttu-id="c7bd5-145">Impossible d’atteindre instance principale hello hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-145">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="c7bd5-146">Cela se produit en cas d’échec de la sonde d’intégrité hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-146">This happens when hello health probe fails.</span></span> | <span data-ttu-id="c7bd5-147">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-147">No</span></span> |
| <span data-ttu-id="c7bd5-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="c7bd5-148">PlatformInActive</span></span> | <span data-ttu-id="c7bd5-149">Il existe un problème avec la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-149">There is an issue with hello platform.</span></span> | <span data-ttu-id="c7bd5-150">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-150">No</span></span>|
| <span data-ttu-id="c7bd5-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="c7bd5-151">ServiceNotRunning</span></span> | <span data-ttu-id="c7bd5-152">service sous-jacent de Hello ne fonctionne pas.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-152">hello underlying service is not running.</span></span> | <span data-ttu-id="c7bd5-153">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-153">No</span></span>|
| <span data-ttu-id="c7bd5-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="c7bd5-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="c7bd5-155">Aucune connexion n’existe sur la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-155">No Connections exists on hello gateway.</span></span> <span data-ttu-id="c7bd5-156">Il s’agit simplement d’un avertissement.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-156">This is only a warning.</span></span>| <span data-ttu-id="c7bd5-157">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-157">No</span></span>|
| <span data-ttu-id="c7bd5-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="c7bd5-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="c7bd5-159">Aucune connexion n’est établie.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-159">Connections are not connected.</span></span> <span data-ttu-id="c7bd5-160">Il s’agit simplement d’un avertissement.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-160">This is only a warning.</span></span>| <span data-ttu-id="c7bd5-161">Oui</span><span class="sxs-lookup"><span data-stu-id="c7bd5-161">Yes</span></span>|
| <span data-ttu-id="c7bd5-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="c7bd5-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="c7bd5-163">utilisation du processeur de passerelle Hello est > 95 %.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-163">hello current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="c7bd5-164">Oui</span><span class="sxs-lookup"><span data-stu-id="c7bd5-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="c7bd5-165">Connexion</span><span class="sxs-lookup"><span data-stu-id="c7bd5-165">Connection</span></span>

| <span data-ttu-id="c7bd5-166">Type d’erreur</span><span class="sxs-lookup"><span data-stu-id="c7bd5-166">Fault Type</span></span> | <span data-ttu-id="c7bd5-167">Motif</span><span class="sxs-lookup"><span data-stu-id="c7bd5-167">Reason</span></span> | <span data-ttu-id="c7bd5-168">Journal</span><span class="sxs-lookup"><span data-stu-id="c7bd5-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="c7bd5-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="c7bd5-169">NoFault</span></span> | <span data-ttu-id="c7bd5-170">Quand aucune erreur n’est détectée.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-170">When no error is detected.</span></span> |<span data-ttu-id="c7bd5-171">Oui</span><span class="sxs-lookup"><span data-stu-id="c7bd5-171">Yes</span></span>|
| <span data-ttu-id="c7bd5-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="c7bd5-172">GatewayNotFound</span></span> | <span data-ttu-id="c7bd5-173">Passerelle introuvable ou non approvisionnée.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="c7bd5-174">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-174">No</span></span>|
| <span data-ttu-id="c7bd5-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="c7bd5-175">PlannedMaintenance</span></span> | <span data-ttu-id="c7bd5-176">Instance de passerelle en maintenance.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="c7bd5-177">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-177">No</span></span>|
| <span data-ttu-id="c7bd5-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="c7bd5-178">UserDrivenUpdate</span></span> | <span data-ttu-id="c7bd5-179">Quand une mise à jour utilisateur est en cours.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-179">When a user update is in progress.</span></span> <span data-ttu-id="c7bd5-180">Il peut s’agir d’une opération de redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-180">This could be a resize operation.</span></span>  | <span data-ttu-id="c7bd5-181">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-181">No</span></span> |
| <span data-ttu-id="c7bd5-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="c7bd5-182">VipUnResponsive</span></span> | <span data-ttu-id="c7bd5-183">Impossible d’atteindre instance principale hello hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-183">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="c7bd5-184">Il se produit en cas d’échec de la sonde d’intégrité hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-184">It happens when hello health probe fails.</span></span> | <span data-ttu-id="c7bd5-185">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-185">No</span></span> |
| <span data-ttu-id="c7bd5-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="c7bd5-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="c7bd5-187">La configuration de la connexion est manquante.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-187">Connection configuration is missing.</span></span> | <span data-ttu-id="c7bd5-188">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-188">No</span></span> |
| <span data-ttu-id="c7bd5-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="c7bd5-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="c7bd5-190">Hello connexion est marquée comme « déconnecté ».</span><span class="sxs-lookup"><span data-stu-id="c7bd5-190">hello Connection is marked "disconnected".</span></span> |<span data-ttu-id="c7bd5-191">Non</span><span class="sxs-lookup"><span data-stu-id="c7bd5-191">No</span></span>|
| <span data-ttu-id="c7bd5-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="c7bd5-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="c7bd5-193">service d’Hello sous-jacent n’a pas de hello que connexion configurée.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-193">hello underlying service does not have hello Connection configured.</span></span> | <span data-ttu-id="c7bd5-194">Oui</span><span class="sxs-lookup"><span data-stu-id="c7bd5-194">Yes</span></span> |
| <span data-ttu-id="c7bd5-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="c7bd5-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="c7bd5-196">Hello service sous-jacent est marqué en état de secours.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-196">hello underlying service is marked as standby.</span></span>| <span data-ttu-id="c7bd5-197">Oui</span><span class="sxs-lookup"><span data-stu-id="c7bd5-197">Yes</span></span>|
| <span data-ttu-id="c7bd5-198">Authentification</span><span class="sxs-lookup"><span data-stu-id="c7bd5-198">Authentication</span></span> | <span data-ttu-id="c7bd5-199">Non-concordance des clés prépartagées.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="c7bd5-200">Oui</span><span class="sxs-lookup"><span data-stu-id="c7bd5-200">Yes</span></span>|
| <span data-ttu-id="c7bd5-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="c7bd5-201">PeerReachability</span></span> | <span data-ttu-id="c7bd5-202">passerelle de homologue Hello n’est pas accessible.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-202">hello peer gateway is not reachable.</span></span> | <span data-ttu-id="c7bd5-203">Oui</span><span class="sxs-lookup"><span data-stu-id="c7bd5-203">Yes</span></span>|
| <span data-ttu-id="c7bd5-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="c7bd5-204">IkePolicyMismatch</span></span> | <span data-ttu-id="c7bd5-205">passerelle de homologue Hello comporte des stratégies IKE qui ne sont pas pris en charge par Azure.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-205">hello peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="c7bd5-206">Oui</span><span class="sxs-lookup"><span data-stu-id="c7bd5-206">Yes</span></span>|
| <span data-ttu-id="c7bd5-207">WfpParse Error</span><span class="sxs-lookup"><span data-stu-id="c7bd5-207">WfpParse Error</span></span> | <span data-ttu-id="c7bd5-208">Une erreur s’est produite lors de l’analyse journal de protection de fichiers Windows hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-208">An error occurred parsing hello WFP log.</span></span> |<span data-ttu-id="c7bd5-209">Oui</span><span class="sxs-lookup"><span data-stu-id="c7bd5-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="c7bd5-210">Types de passerelles pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-210">Supported Gateway types</span></span>

<span data-ttu-id="c7bd5-211">Hello liste suivante montre la prise en charge de hello les passerelles et les connexions sont pris en charge avec la résolution des problèmes de l’Observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-211">hello following list shows hello support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="c7bd5-212">**Types de passerelles**</span><span class="sxs-lookup"><span data-stu-id="c7bd5-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="c7bd5-213">VPN</span><span class="sxs-lookup"><span data-stu-id="c7bd5-213">VPN</span></span>      | <span data-ttu-id="c7bd5-214">Pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-214">Supported</span></span>        |
|<span data-ttu-id="c7bd5-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c7bd5-215">ExpressRoute</span></span> | <span data-ttu-id="c7bd5-216">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-216">Not Supported</span></span> |
|<span data-ttu-id="c7bd5-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="c7bd5-217">Hypernet</span></span> | <span data-ttu-id="c7bd5-218">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-218">Not Supported</span></span>|
|<span data-ttu-id="c7bd5-219">**Types de VPN**</span><span class="sxs-lookup"><span data-stu-id="c7bd5-219">**VPN types**</span></span> | |
|<span data-ttu-id="c7bd5-220">Route-based</span><span class="sxs-lookup"><span data-stu-id="c7bd5-220">Route Based</span></span> | <span data-ttu-id="c7bd5-221">Pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-221">Supported</span></span>|
|<span data-ttu-id="c7bd5-222">Policy-based</span><span class="sxs-lookup"><span data-stu-id="c7bd5-222">Policy Based</span></span> | <span data-ttu-id="c7bd5-223">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-223">Not Supported</span></span>|
|<span data-ttu-id="c7bd5-224">**Types de connexions**</span><span class="sxs-lookup"><span data-stu-id="c7bd5-224">**Connection types**</span></span>||
|<span data-ttu-id="c7bd5-225">IPsec</span><span class="sxs-lookup"><span data-stu-id="c7bd5-225">IPSec</span></span>| <span data-ttu-id="c7bd5-226">Pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-226">Supported</span></span>|
|<span data-ttu-id="c7bd5-227">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="c7bd5-227">VNet2Vnet</span></span>| <span data-ttu-id="c7bd5-228">Pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-228">Supported</span></span>|
|<span data-ttu-id="c7bd5-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c7bd5-229">ExpressRoute</span></span>| <span data-ttu-id="c7bd5-230">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-230">Not Supported</span></span>|
|<span data-ttu-id="c7bd5-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="c7bd5-231">Hypernet</span></span>| <span data-ttu-id="c7bd5-232">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-232">Not Supported</span></span>|
|<span data-ttu-id="c7bd5-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="c7bd5-233">VPNClient</span></span>| <span data-ttu-id="c7bd5-234">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="c7bd5-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="c7bd5-235">Fichiers journaux</span><span class="sxs-lookup"><span data-stu-id="c7bd5-235">Log files</span></span>

<span data-ttu-id="c7bd5-236">fichiers de journaux dépannage Hello ressource sont stockés dans un compte de stockage après que la résolution des problèmes de ressource sont terminée.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-236">hello resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="c7bd5-237">Hello image suivante montre contenu d’exemple hello d’un appel qui a généré une erreur.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-237">hello following image shows hello example contents of a call that resulted in an error.</span></span>

![fichier zip][1]

> [!NOTE]
> <span data-ttu-id="c7bd5-239">Dans certains cas, seul un sous-ensemble des fichiers de journaux hello est écrit toostorage.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-239">In some cases, only a subset of hello logs files is written toostorage.</span></span>

<span data-ttu-id="c7bd5-240">Pour obtenir des instructions sur le téléchargement de fichiers à partir des comptes de stockage azure, consultez trop[prise en main le stockage Blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c7bd5-240">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="c7bd5-241">L’explorateur de stockage peut aussi être utilisé.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="c7bd5-242">Plus d’informations sur l’Explorateur de stockage trouverez ici hello lien : [Explorateur de stockage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="c7bd5-242">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="c7bd5-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="c7bd5-243">ConnectionStats.txt</span></span>

<span data-ttu-id="c7bd5-244">Hello **ConnectionStats.txt** fichier contient des statistiques globales de hello connexion, y compris les octets d’entrée et de sortie, l’état de connexion et hello de temps hello connexion a été établie.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-244">hello **ConnectionStats.txt** file contains overall stats of hello Connection, including ingress and egress bytes, Connection status, and hello time hello Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="c7bd5-245">Si toohello d’appel hello dépannage API renvoie sain, seul hello retournée dans le fichier zip de hello est un **ConnectionStats.txt** fichier.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-245">If hello call toohello troubleshooting API returns healthy, hello only thing returned in hello zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="c7bd5-246">contenu Hello de ce fichier est similaires toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c7bd5-246">hello contents of this file are similar toohello following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="c7bd5-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="c7bd5-247">CPUStats.txt</span></span>

<span data-ttu-id="c7bd5-248">Hello **CPUStats.txt** fichier contient l’utilisation du processeur et mémoire disponible au moment de hello du test.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-248">hello **CPUStats.txt** file contains CPU usage and memory available at hello time of testing.</span></span>  <span data-ttu-id="c7bd5-249">contenu Hello de ce fichier est semblable toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c7bd5-249">hello contents of this file is similar toohello following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="c7bd5-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="c7bd5-250">IKEErrors.txt</span></span>

<span data-ttu-id="c7bd5-251">Hello **IKEErrors.txt** fichier contient toutes les erreurs de IKE qui ont été détectées pendant l’analyse.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-251">hello **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="c7bd5-252">Hello suivant montre contenu hello d’un fichier IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-252">hello following example shows hello contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="c7bd5-253">Votre erreurs peuvent être différentes en fonction du problème de hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-253">Your errors may be different depending on hello issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="c7bd5-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="c7bd5-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="c7bd5-255">Hello **Scrubbed-wfpdiag.txt** fichier journal contient le journal de protection de fichiers Windows hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-255">hello **Scrubbed-wfpdiag.txt** log file contains hello wfp log.</span></span> <span data-ttu-id="c7bd5-256">Ce journal contient la journalisation des rejets de paquets et des échecs IKE/AuthIP.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="c7bd5-257">Hello suivant montre contenu hello du fichier de Scrubbed-wfpdiag.txt hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-257">hello following example shows hello contents of hello Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="c7bd5-258">Dans cet exemple, la clé partagée de hello d’une connexion n’était pas correcte comme peuvent être consultés à partir de la ligne en bas de hello 3e hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-258">In this example, hello shared key of a Connection was not correct as can be seen from hello 3rd line from hello bottom.</span></span> <span data-ttu-id="c7bd5-259">Hello l’exemple suivant est simplement un extrait de journal complet de hello, comme le journal de hello peut être longue, en fonction du problème de hello.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-259">hello following example is just a snippet of hello entire log, as hello log can be lengthy depending on hello issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="c7bd5-260">wfpdiag.txt.Sum</span><span class="sxs-lookup"><span data-stu-id="c7bd5-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="c7bd5-261">Hello **wfpdiag.txt.sum** fichier est un journal présentant les mémoires tampons de hello et les événements traités.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-261">hello **wfpdiag.txt.sum** file is a log showing hello buffers and events processed.</span></span>

<span data-ttu-id="c7bd5-262">Hello exemple suivant est contenu hello d’un fichier wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="c7bd5-262">hello following example is hello contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="c7bd5-263">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7bd5-263">Next steps</span></span>

<span data-ttu-id="c7bd5-264">Découvrez comment toodiagnose les passerelles VPN et les connexions via hello portail en vous rendant sur [dépannage de la passerelle - portail Azure](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c7bd5-264">Learn how toodiagnose VPN Gateways and Connections through hello portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
