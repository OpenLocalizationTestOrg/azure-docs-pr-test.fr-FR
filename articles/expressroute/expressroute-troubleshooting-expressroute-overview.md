---
title: "Vérification de la connectivité : Guide de dépannage Azure ExpressRoute | Microsoft Docs"
description: "Cette page fournit des instructions sur le dépannage et la validation de la connectivité de bout en bout d’un circuit ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 5a6360b56963d219ab576fb3e2636b6c51dd72ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="ea2bd-103">Vérification de la connectivité ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ea2bd-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="ea2bd-104">ExpressRoute, qui étend un réseau local dans le cloud Microsoft par le biais d’une connexion privée qui est facilitée par un fournisseur de connectivité, implique les trois zones de réseau distinctes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-104">ExpressRoute, which extends an on-premises network into the Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves the following three distinct network zones:</span></span>

-   <span data-ttu-id="ea2bd-105">Réseau de client</span><span class="sxs-lookup"><span data-stu-id="ea2bd-105">Customer Network</span></span>
-   <span data-ttu-id="ea2bd-106">Réseau de fournisseur</span><span class="sxs-lookup"><span data-stu-id="ea2bd-106">Provider Network</span></span>
-   <span data-ttu-id="ea2bd-107">Centre de données Microsoft</span><span class="sxs-lookup"><span data-stu-id="ea2bd-107">Microsoft Datacenter</span></span>

<span data-ttu-id="ea2bd-108">L’objectif de ce document est d’aider l’utilisateur à identifier où (ou même si) un problème de connectivité existe et dans quelle zone, afin de demander l’aide d’une équipe appropriée pour le résoudre.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-108">The purpose of this document is to help user to identify where (or even if) a connectivity issue exists and within which zone, thereby to seek help from appropriate team to resolve the issue.</span></span> <span data-ttu-id="ea2bd-109">Si le support technique de Microsoft est nécessaire pour résoudre un problème, ouvrez un ticket de support auprès du [support Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-109">If Microsoft support is needed to resolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea2bd-110">Ce document a pour but de vous aider à diagnostiquer et à résoudre des problèmes simples.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-110">This document is intended to help diagnosing and fixing simple issues.</span></span> <span data-ttu-id="ea2bd-111">Il n’a pas pour objet de remplacer le support de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-111">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="ea2bd-112">Si vous ne parvenez pas à résoudre le problème en suivant les conseils donnés, ouvrez un ticket de support auprès du [support Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-112">Open a support ticket with [Microsoft Support][Support] if you are unable to solve the problem using the guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="ea2bd-113">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ea2bd-113">Overview</span></span>
<span data-ttu-id="ea2bd-114">Le diagramme suivant illustre la connectivité logique d’un réseau de client vers un réseau Microsoft à l’aide d’ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-114">The following diagram shows the logical connectivity of a customer network to Microsoft network using ExpressRoute.</span></span>
<span data-ttu-id="ea2bd-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="ea2bd-115">[![1]][1]</span></span>

<span data-ttu-id="ea2bd-116">Dans le diagramme précédent, les nombres indiquent les points clés de réseau.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-116">In the preceding diagram, the numbers indicate key network points.</span></span> <span data-ttu-id="ea2bd-117">Les points de réseau sont souvent référencés dans cet article par le numéro qui leur est associé.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-117">The network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="ea2bd-118">Selon le modèle de connectivité ExpressRoute (colocalisation Cloud Exchange, connexion Ethernet point à point ou universelle (IPVPN)), les points de réseau 3 et 4 peuvent être commutateurs (appareils de couche 2).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-118">Depending on the ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) the network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="ea2bd-119">Les points clés de réseau illustrés sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-119">The key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="ea2bd-120">Appareil de calcul du client (par exemple, un serveur ou un PC)</span><span class="sxs-lookup"><span data-stu-id="ea2bd-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="ea2bd-121">CE : routeurs de périphérie du client</span><span class="sxs-lookup"><span data-stu-id="ea2bd-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="ea2bd-122">PE (collaborant avec des CE) : routeurs / commutateurs de périphérie du fournisseur qui collaborent avec des routeurs de périphérie du client.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="ea2bd-123">Appelé PE-CE dans ce document.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-123">Referred to as PE-CEs in this document.</span></span>
4.  <span data-ttu-id="ea2bd-124">PE (collaborant avec des MSEE) : routeurs / commutateurs de périphérie du fournisseur qui collaborent avec des MSEE.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="ea2bd-125">Appelé PE-MSEE dans ce document.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-125">Referred to as PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="ea2bd-126">MSEE : routeurs ExpressRoute Microsoft Enterprise Edge (MSEE)</span><span class="sxs-lookup"><span data-stu-id="ea2bd-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="ea2bd-127">Passerelle de réseau virtuel (VNet)</span><span class="sxs-lookup"><span data-stu-id="ea2bd-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="ea2bd-128">Appareil de calcul sur le réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="ea2bd-128">Compute device on the Azure VNet</span></span>

<span data-ttu-id="ea2bd-129">Si les modèles de connectivité Colocalisation Cloud Exchange ou Connexion Ethernet point à point sont utilisés, le routeur de périphérie du client (2) établit l’homologation BGP avec des MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-129">If the Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, the customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="ea2bd-130">Les points de réseau 3 et 4 existent toujours, mais sont quelque peu transparents en tant qu'appareils de couche 2.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="ea2bd-131">Si le modèle de connectivité universelle (IPVPN) est utilisé, les PE (collaborant avec des MSEE) (4) établissent une homologation BGP avec des MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-131">If the Any-to-any (IPVPN) connectivity model is used, the PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="ea2bd-132">Les itinéraires sont ensuite propagés sur le réseau du client par le biais du réseau de fournisseur de service IPVPN.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-132">Routes would then propagate back to the customer network via the IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="ea2bd-133">Pour la haute disponibilité ExpressRoute, Microsoft nécessite une paire de sessions BGP redondante entre des MSEE (5) et des PE-MSEE (4).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="ea2bd-134">Une paire redondante de chemins d’accès au réseau est également recommandée entre le réseau du client et les PE-CE.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="ea2bd-135">Cependant, dans le modèle de connexion universelle (IPVPN), un seul appareil CE (2) peut-être connecté à un ou plusieurs PE (3).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected to one or more PEs (3).</span></span>
>
>

<span data-ttu-id="ea2bd-136">Les étapes suivantes permettent de valider un circuit ExpressRoute (avec le point de réseau indiqué par le nombre associé) :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-136">To validate an ExpressRoute circuit, the following steps are covered (with the network point indicated by the associated number):</span></span>
1. [<span data-ttu-id="ea2bd-137">Validation de l'approvisionnement et l’état du circuit (5)</span><span class="sxs-lookup"><span data-stu-id="ea2bd-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="ea2bd-138">Valider qu'au moins une homologation ExpressRoute est configurée (5)</span><span class="sxs-lookup"><span data-stu-id="ea2bd-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="ea2bd-139">Validation de l'ARP entre Microsoft et le fournisseur de service (lien entre 4 et 5)</span><span class="sxs-lookup"><span data-stu-id="ea2bd-139">Validate ARP between Microsoft and the service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="ea2bd-140">Valider les BGP et les itinéraires sur les MSEE (BGP entre 4 et 5 et 5 et 6 si un réseau virtuel est connecté)</span><span class="sxs-lookup"><span data-stu-id="ea2bd-140">Validate BGP and routes on the MSEE (BGP between 4 to 5, and 5 to 6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="ea2bd-141">Vérifier les statistiques de trafic (trafic passant par 5)</span><span class="sxs-lookup"><span data-stu-id="ea2bd-141">Check the Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="ea2bd-142">Des validations et des vérifications complémentaires seront ajoutées prochainement, vérifiez tous les mois !</span><span class="sxs-lookup"><span data-stu-id="ea2bd-142">More validations and checks will be added in the future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="ea2bd-143">Validation de l'approvisionnement et l’état du circuit</span><span class="sxs-lookup"><span data-stu-id="ea2bd-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="ea2bd-144">Quel que soit le modèle de connectivité, un circuit ExpressRoute doit être créé et une clé de service générée pour l’approvisionnement du circuit.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-144">Regardless of the connectivity model, an ExpressRoute circuit has to be created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="ea2bd-145">L’approvisionnement d’un circuit ExpressRoute établit une connexion de couche 2 redondante entre les PE-MSEE (4) et les MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="ea2bd-146">Pour plus d’informations sur la manière de créer, de modifier, d'approvisionner et de vérifier un circuit ExpressRoute, consultez l’article [Création et modification d’un circuit ExpressRoute][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-146">For more information on how to create, modify, provision, and verify an ExpressRoute circuit, see the article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="ea2bd-147">Une clé de service identifie un circuit ExpressRoute de façon unique.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="ea2bd-148">Cette clé est exigée pour la plupart des commandes powershell mentionnées dans ce document.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-148">This key is required for most of the powershell commands mentioned in this document.</span></span> <span data-ttu-id="ea2bd-149">Si vous avez également besoin d'assistance de la part de Microsoft ou d’un partenaire ExpressRoute pour résoudre un problème lié à ExpressRoute, entrez la clé de service afin d’identifier facilement le circuit.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner to troubleshoot an ExpressRoute issue, provide the service key to readily identify the circuit.</span></span>
>
>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="ea2bd-150">Vérification par le biais du portail Azure</span><span class="sxs-lookup"><span data-stu-id="ea2bd-150">Verification via the Azure portal</span></span>
<span data-ttu-id="ea2bd-151">Dans le portail Azure, l’état d’un circuit ExpressRoute peut être vérifié en sélectionnant ![2][2] dans la barre de menu de gauche, puis en sélectionnant le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-151">In the Azure portal, the status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="ea2bd-152">Sélectionner un circuit ExpressRoute répertorié sous « Toutes les ressources » ouvre le panneau de circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-152">Selecting an ExpressRoute circuit listed under "All resources" opens the ExpressRoute circuit blade.</span></span> <span data-ttu-id="ea2bd-153">Dans la section ![3][3] du panneau, les informations essentielles d'ExpressRoute sont indiquées comme illustré dans la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-153">In the ![3][3] section of the blade, the ExpressRoute essentials are listed as shown in the following screen shot:</span></span>

<span data-ttu-id="ea2bd-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="ea2bd-154">![4][4]</span></span>    

<span data-ttu-id="ea2bd-155">Dans ExpressRoute Essentials, *l'état du circuit* indique l’état du circuit côté Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-155">In the ExpressRoute Essentials, *Circuit status* indicates the status of the circuit on the Microsoft side.</span></span> <span data-ttu-id="ea2bd-156">*L'état du fournisseur* indique si le circuit a été *approvisionné/non approvisionné* côté fournisseur de service.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-156">*Provider status* indicates if the circuit has been *Provisioned/Not provisioned* on the service-provider side.</span></span> 

<span data-ttu-id="ea2bd-157">Pour qu'un circuit ExpressRoute soit opérationnel, *l'état du Circuit* doit être *activé* et *l'état du fournisseur* doit être *approvisionné*.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-157">For an ExpressRoute circuit to be operational, the *Circuit status* must be *Enabled* and the *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="ea2bd-158">Si *l'état du circuit* est désactivé, contactez le [support Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-158">If the *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="ea2bd-159">Si *l'état du fournisseur* n'est pas approvisionné, contactez votre fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-159">If the *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="ea2bd-160">Vérification par le biais de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea2bd-160">Verification via PowerShell</span></span>
<span data-ttu-id="ea2bd-161">Pour répertorier tous les circuits ExpressRoute dans un groupe de ressources, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-161">To list all the ExpressRoute circuits in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="ea2bd-162">Vous pouvez obtenir le nom de votre groupe de ressources par le biais du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-162">You can get your resource group name through the Azure portal.</span></span> <span data-ttu-id="ea2bd-163">Consultez la section précédente de ce document et notez que le nom de groupe de ressources est répertorié dans l'exemple de capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-163">See the previous subsection of this document and note that the resource group name is listed in the example screen shot.</span></span>
>
>

<span data-ttu-id="ea2bd-164">Pour sélectionner un circuit ExpressRoute spécifique dans un groupe de ressources, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-164">To select a particular ExpressRoute circuit in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="ea2bd-165">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="ea2bd-166">Pour vérifier si un circuit ExpressRoute est opérationnel, portez une attention particulière aux champs suivants :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-166">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="ea2bd-167">Si *CircuitProvisioningState* est désactivé, contactez le [support Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-167">If the *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="ea2bd-168">Si *ServiceProviderProvisioningState* n'est pas approvisionné, contactez votre fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-168">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="ea2bd-169">Vérification par le biais de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="ea2bd-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="ea2bd-170">Pour répertorier tous les circuits ExpressRoute dans un abonnement, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-170">To list all the ExpressRoute circuits under a subscription, use the following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="ea2bd-171">Pour sélectionner un circuit ExpressRoute spécifique, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-171">To select a particular ExpressRoute circuit, use the following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="ea2bd-172">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="ea2bd-173">Pour vérifier si un circuit ExpressRoute est opérationnel, portez une attention particulière aux champs suivants : ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span><span class="sxs-lookup"><span data-stu-id="ea2bd-173">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="ea2bd-174">Si *l'état* est désactivé, contactez le [support Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-174">If the *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="ea2bd-175">Si *ServiceProviderProvisioningState* n'est pas approvisionné, contactez votre fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-175">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="ea2bd-176">Validation de la configuration de l’homologation</span><span class="sxs-lookup"><span data-stu-id="ea2bd-176">Validate Peering Configuration</span></span>
<span data-ttu-id="ea2bd-177">Une fois que le fournisseur de services a terminé l'approvisionnement du circuit ExpressRoute, une configuration de routage peut être créée à travers le circuit ExpressRoute entre des MSEE-PR (4) et des MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-177">After the service provider has completed the provisioning the ExpressRoute circuit, a routing configuration can be created over the ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="ea2bd-178">Chaque circuit ExpressRoute peut avoir un, deux ou trois contextes de routage activés : l'homologation privée Azure (trafic vers des réseaux virtuels privés dans Azure), l'homologation publique Azure (le trafic vers des adresses IP publiques dans Azure) et l'homologation Microsoft (Office 365 et Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic to private virtual networks in Azure), Azure public peering (traffic to public IP addresses in Azure), and Microsoft peering (traffic to Office 365 and Dynamics 365).</span></span> <span data-ttu-id="ea2bd-179">Pour plus d’informations sur la création et la modification de la configuration de routage, consultez l’article [Créer et modifier le routage le routage pour un circuit ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-179">For more information on how to create and modify routing configuration, see the article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="ea2bd-180">Vérification par le biais du portail Azure</span><span class="sxs-lookup"><span data-stu-id="ea2bd-180">Verification via the Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="ea2bd-181">Il existe un bogue connu dans le portail Azure : certaines homologations ExpressRoute ne sont *PAS* affichées dans le portail si elles sont configurées par le fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-181">There is a known bug in the Azure portal wherein ExpressRoute peerings are *NOT* shown in the portal if configured by the service provider.</span></span> <span data-ttu-id="ea2bd-182">L'ajout d'homologations ExpressRoute par le biais du portail ou PowerShell *remplace les paramètres du fournisseur de service*.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-182">Adding ExpressRoute peerings via the portal or PowerShell *overwrites the service provider settings*.</span></span> <span data-ttu-id="ea2bd-183">Cette action interrompt le routage sur le circuit ExpressRoute et nécessite le support du fournisseur de services pour restaurer les paramètres et rétablir le routage normal.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-183">This action breaks the routing on the ExpressRoute circuit and requires the support of the service provider to restore the settings and reestablish normal routing.</span></span> <span data-ttu-id="ea2bd-184">Modifiez uniquement les homologations ExpressRoute si vous êtes certain que le fournisseur de services fournit uniquement des services de couche 2 !</span><span class="sxs-lookup"><span data-stu-id="ea2bd-184">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="ea2bd-185">Si la couche 3 est fournie par le fournisseur de services et si les homologations sont vides dans le portail, vous pouvez utiliser PowerShell pour voir les paramètres configurés du fournisseur du service.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-185">If layer 3 is provided by the service provider and the peerings are blank in the portal, PowerShell can be used to see the service provider configured settings.</span></span>
>
>

<span data-ttu-id="ea2bd-186">Dans le portail Azure, l’état d’un circuit ExpressRoute peut être vérifié en sélectionnant ![2][2] dans la barre de menu de gauche, puis en sélectionnant le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-186">In the Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="ea2bd-187">Sélectionner un circuit ExpressRoute répertorié sous « Toutes les ressources » permet d'ouvrir le panneau de circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-187">Selecting an ExpressRoute circuit listed under "All resources" would open the ExpressRoute circuit blade.</span></span> <span data-ttu-id="ea2bd-188">Dans la section ![3][3] du panneau, les informations essentielles d'ExpressRoute sont indiquées comme illustré dans la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-188">In the ![3][3] section of the blade, the ExpressRoute essentials would be listed as shown in the following screen shot:</span></span>

<span data-ttu-id="ea2bd-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="ea2bd-189">![5][5]</span></span>

<span data-ttu-id="ea2bd-190">Dans l’exemple précédent, nous avons noté que le contexte de routage Homologation privée Azure est activé, tandis que les contextes de routage Homologation publique Azure et Microsoft ne sont pas activés.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-190">In the preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="ea2bd-191">Un contexte d’homologation correctement activé doit également répertorier les sous-réseaux de point à point principaux et secondaires (nécessaires pour BGP).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-191">A successfully enabled peering context would also have the primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="ea2bd-192">Les sous-réseaux /30 sont utilisés pour l’adresse IP d’interface des MSEE et PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-192">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="ea2bd-193">Si aucune homologation n’est activée, vérifiez si les sous-réseaux principaux et secondaires attribués correspondent à la configuration sur les PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-193">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on PE-MSEEs.</span></span> <span data-ttu-id="ea2bd-194">Dans le cas contraire, pour modifier la configuration sur les routeurs MSEE, reportez-vous à la rubrique [Créer et modifier le routage le routage pour un circuit ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="ea2bd-194">If not, to change the configuration on MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="ea2bd-195">Vérification par le biais de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea2bd-195">Verification via PowerShell</span></span>
<span data-ttu-id="ea2bd-196">Pour obtenir les détails sur la configuration de l'homologation privée Azure, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-196">To get the Azure private peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="ea2bd-197">Voici un exemple de réponse pour une homologation privée correctement configurée :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="ea2bd-198">Un contexte d’homologation correctement activé répertorie les préfixes d’adresses principales et secondaires.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-198">A successfully enabled peering context would have the primary and secondary address prefixes listed.</span></span> <span data-ttu-id="ea2bd-199">Les sous-réseaux /30 sont utilisés pour l’adresse IP d’interface des MSEE et PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-199">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="ea2bd-200">Pour obtenir les détails sur la configuration de l'homologation publique Azure, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-200">To get the Azure public peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="ea2bd-201">Pour obtenir les détails sur la configuration de l'homologation Microsoft, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-201">To get the Microsoft peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="ea2bd-202">Si aucune homologation n’est configurée, un message d’erreur est généré.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="ea2bd-203">Voici un exemple de réponse si les homologations mentionnées (l'homologation publique Azure dans cet exemple) ne sont pas configurées dans le circuit :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-203">A sample response, when the stated peering (Azure Public peering in this example) is not configured within the circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="ea2bd-204">Si aucune homologation n’est activée, vérifiez si les sous-réseaux principaux et secondaires attribués correspondent à la configuration sur le PE-MSEE lié.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-204">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="ea2bd-205">Vérifiez également si les *VlanId*, *AzureASN* et *PeerASN* sont utilisés sur des MSEE et si ces valeurs correspondent à celles utilisées sur le PE-MSEE lié.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-205">Also check if the correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="ea2bd-206">Si le hachage MD5 est choisi, la clé partagée doit être la même sur la paire MSEE et PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-206">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="ea2bd-207">Pour modifier la configuration sur les routeurs MSEE, reportez-vous à la rubrique [Créer et modifier le routage le routage pour un circuit ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-207">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="ea2bd-208">Vérification par le biais de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="ea2bd-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="ea2bd-209">Pour obtenir les détails sur la configuration de l'homologation privée Azure, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-209">To get the Azure private peering configuration details, use the following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="ea2bd-210">Voici un exemple de réponse pour une homologation privée correctement configurée :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="ea2bd-211">Un contexte d’homologation correctement activé répertorie les sous-réseaux d'homologation principaux et secondaires.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-211">A successfully, enabled peering context would have the primary and secondary peer subnets listed.</span></span> <span data-ttu-id="ea2bd-212">Les sous-réseaux /30 sont utilisés pour l’adresse IP d’interface des MSEE et PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-212">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="ea2bd-213">Pour obtenir les détails sur la configuration de l'homologation publique Azure, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-213">To get the Azure public peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="ea2bd-214">Pour obtenir les détails sur la configuration de l'homologation Microsoft, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-214">To get the Microsoft peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="ea2bd-215">Si les homologations de couche 3 ont été définies par le fournisseur de services, la définition d'homologations ExpressRoute par le biais du portail ou de PowerShell remplace les paramètres du fournisseur de service.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-215">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span></span> <span data-ttu-id="ea2bd-216">La réinitialisation des paramètres d’homologation côté fournisseur nécessite le support du fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-216">Resetting the provider side peering settings requires the support of the service provider.</span></span> <span data-ttu-id="ea2bd-217">Modifiez uniquement les homologations ExpressRoute si vous êtes certain que le fournisseur de services fournit uniquement des services de couche 2 !</span><span class="sxs-lookup"><span data-stu-id="ea2bd-217">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="ea2bd-218">Si une homologation n’est pas activée, vérifiez si les sous-réseaux d’homologation principaux et secondaires attribués correspondent à la configuration sur le PE-MSEE lié.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-218">If a peering is not enabled, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="ea2bd-219">Vérifiez également si les *VlanId*, *AzureAsn* et *PeerAsn* sont utilisés sur des MSEE et si ces valeurs correspondent à celles utilisées sur le PE-MSEE lié.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-219">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="ea2bd-220">Pour modifier la configuration sur les routeurs MSEE, reportez-vous à la rubrique [Créer et modifier le routage le routage pour un circuit ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-220">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-the-service-provider"></a><span data-ttu-id="ea2bd-221">Validation de l'ARP entre Microsoft et le fournisseur de service</span><span class="sxs-lookup"><span data-stu-id="ea2bd-221">Validate ARP between Microsoft and the service provider</span></span>
<span data-ttu-id="ea2bd-222">Cette section utilise les commandes PowerShell (classiques).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="ea2bd-223">Si vous avez utilisé des commandes PowerShell Azure Resource Manager, assurez-vous d’avoir un accès administrateur / coadministrateur à l’abonnement par le biais du [portail Azure Classic][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="ea2bd-224">Pour le dépannage à l’aide des commandes Azure Resource Manager, veuillez vous reporter au document [Obtention de tables ARP dans le modèle de déploiement Resource Manager][ARP].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-224">For troubleshooting using Azure Resource Manager commands please refer to the [Getting ARP tables in the Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="ea2bd-225">Vous pouvez utiliser le portail Azure et les commandes Azure Resource Manager PowerShell pour obtenir l’ARP.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-225">To get ARP, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="ea2bd-226">Si vous rencontrez des erreurs avec les commandes PowerShell Azure Resource Manager, les commandes PowerShell classiques peuvent fonctionner comme commandes PowerShell classiques et avec des circuits ExpressRoute Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-226">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="ea2bd-227">Pour obtenir la table ARP depuis le routeur MSEE principal pour l’homologation privée, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-227">To get the ARP table from the primary MSEE router for the private peering, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="ea2bd-228">Voici un exemple de réponse pour la commande si le scénario réussit :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-228">An example response for the command, in the successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="ea2bd-229">De même, vous pouvez vérifier la table ARP à partir des MSEE dans le chemin d'accès *principal*/*secondaire* pour les homologations *privée*/*publique*/*Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-229">Similarly, you can check the ARP table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="ea2bd-230">L’exemple suivant montre la réponse de la commande pour une homologation inexistante.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-230">The following example shows the response of the command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="ea2bd-231">Si la table ARP ne comprend pas les adresses IP des interfaces mappées sur des adresses MAC, passez en revue les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-231">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
>1. <span data-ttu-id="ea2bd-232">Si la première adresse IP du sous-réseau /30 affecté pour la liaison entre les MSEE-PR et MSEE est utilisée dans l’interface de MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-232">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="ea2bd-233">Azure utilise toujours la deuxième adresse IP pour les MSEE.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-233">Azure always uses the second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="ea2bd-234">Vérifiez si les balises VLAN du client (C-Tag) et du service (S-Tag) correspondent à la paire MSEE-PR et MSEE.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-234">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-the-msee"></a><span data-ttu-id="ea2bd-235">Validation de BGP et des itinéraires sur les MSEE</span><span class="sxs-lookup"><span data-stu-id="ea2bd-235">Validate BGP and routes on the MSEE</span></span>
<span data-ttu-id="ea2bd-236">Cette section utilise les commandes PowerShell (classiques).</span><span class="sxs-lookup"><span data-stu-id="ea2bd-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="ea2bd-237">Si vous avez utilisé des commandes PowerShell Azure Resource Manager, assurez-vous que vous avez un accès administrateur/coadministrateur à l’abonnement par le biais du [portail Azure classique][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="ea2bd-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="ea2bd-238">Vous pouvez utiliser le portail Azure et les commandes Azure Resource Manager PowerShell pour obtenir des informations BGP.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-238">To get BGP information, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="ea2bd-239">Si vous rencontrez des erreurs avec les commandes PowerShell Azure Resource Manager, les commandes PowerShell classiques peuvent fonctionner comme commandes PowerShell classiques et avec des circuits ExpressRoute Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-239">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="ea2bd-240">Pour obtenir le résumé de la table de routage (voisin BGP) d’un contexte de routage spécifique, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-240">To get the routing table (BGP neighbor) summary for a particular routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="ea2bd-241">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="ea2bd-242">Comme indiqué dans l’exemple précédent, la commande est utile pour déterminer pour la durée de mise en place du contexte de routage.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-242">As shown in the preceding example, the command is useful to determine for how long the routing context has been established.</span></span> <span data-ttu-id="ea2bd-243">Il indique également le nombre de préfixes d’itinéraire annoncés par le routeur d'homologation.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-243">It also indicates number of route prefixes advertised by the peering router.</span></span>

>[!NOTE]
><span data-ttu-id="ea2bd-244">Si l’état est Activé ou Inactif, vérifiez si les sous-réseaux d’homologation principaux et secondaires attribués correspondent à la configuration sur le PE-MSEE lié.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-244">If the state is in Active or Idle, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="ea2bd-245">Vérifiez également si les *VlanId*, *AzureAsn* et *PeerAsn* sont utilisés sur des MSEE et si ces valeurs correspondent à celles utilisées sur le PE-MSEE lié.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-245">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="ea2bd-246">Si le hachage MD5 est choisi, la clé partagée doit être la même sur la paire MSEE et PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-246">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="ea2bd-247">Pour modifier la configuration sur les routeurs MSEE, reportez-vous à la rubrique [Créer et modifier le routage le routage pour un circuit ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="ea2bd-247">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="ea2bd-248">Si certaines destinations ne sont pas accessibles par le biais d’une homologation particulière, vérifiez la table d’itinéraires des MSEE appartenant au contexte d’homologation spécifique.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-248">If certain destinations are not reachable over a particular peering, check the route table of the MSEEs belonging to the particular peering context.</span></span> <span data-ttu-id="ea2bd-249">Si aucun préfixe correspondant (éventuellement NATed IP) n'est présent dans la table de routage, vérifiez s’il existe des pare-feu/NSG/ACL sur le chemin d’accès et si elles autorisent le trafic.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-249">If a matching prefix (could be NATed IP) is present in the routing table, then check if there are firewalls/NSG/ACLs on the path and if they permit the traffic.</span></span>
>
>

<span data-ttu-id="ea2bd-250">Pour obtenir la table de routage complète à partir du MSEE sur le chemin d’accès *principal* pour le contexte de routage *privé* spécifique, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-250">To get the full routing table from MSEE on the *Primary* path for the particular *Private* routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="ea2bd-251">Voici un exemple de sortie réussie de la commande :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-251">An example successful outcome for the command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="ea2bd-252">De même, vous pouvez vérifier la table de routage à partir des MSEE dans le chemin d'accès *principal*/*secondaire* pour le contexte d'homologation *privé*/*public*/*Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="ea2bd-252">Similarly, you can check the routing table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="ea2bd-253">L’exemple suivant montre la réponse de la commande pour une homologation inexistante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-253">The following example shows the response of the command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-the-traffic-statistics"></a><span data-ttu-id="ea2bd-254">Vérification des statistiques de trafic</span><span class="sxs-lookup"><span data-stu-id="ea2bd-254">Check the Traffic Statistics</span></span>
<span data-ttu-id="ea2bd-255">Pour obtenir les statistiques combinées du trafic de chemin d’accès primaire et secondaire (octets en entrée et en sortie) d’un contexte d’homologation, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-255">To get the combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use the following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="ea2bd-256">Voici un exemple de sortie de la commande :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-256">A sample output of the command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="ea2bd-257">Voici un exemple de sortie de la commande pour une homologation inexistante :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-257">A sample output of the command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="ea2bd-258">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ea2bd-258">Next Steps</span></span>
<span data-ttu-id="ea2bd-259">Pour plus d’informations ou d'aide, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="ea2bd-259">For more information or help, check out the following links:</span></span>

- <span data-ttu-id="ea2bd-260">[Support Microsoft][Support]</span><span class="sxs-lookup"><span data-stu-id="ea2bd-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="ea2bd-261">[Création et modification d’un circuit ExpressRoute][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="ea2bd-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="ea2bd-262">[Créer et modifier le routage le routage pour un circuit ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="ea2bd-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
<span data-ttu-id="ea2bd-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Connectivité logique Express Route"</span><span class="sxs-lookup"><span data-stu-id="ea2bd-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity"</span></span>
<span data-ttu-id="ea2bd-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Icône Toutes les ressources"</span><span class="sxs-lookup"><span data-stu-id="ea2bd-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "All resources icon"</span></span>
<span data-ttu-id="ea2bd-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Icône Vue d’ensemble"</span><span class="sxs-lookup"><span data-stu-id="ea2bd-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overview icon"</span></span>
<span data-ttu-id="ea2bd-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Capture d’écran : exemple pour ExpressRoute Essentials"</span><span class="sxs-lookup"><span data-stu-id="ea2bd-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials sample screenshot"</span></span>
<span data-ttu-id="ea2bd-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Capture d’écran : exemple pour ExpressRoute Essentials"</span><span class="sxs-lookup"><span data-stu-id="ea2bd-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials sample screenshot"</span></span>

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






