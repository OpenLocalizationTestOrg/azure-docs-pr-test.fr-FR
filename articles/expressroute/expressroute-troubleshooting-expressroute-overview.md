---
title: "Vérification de la connectivité : Guide de dépannage Azure ExpressRoute | Microsoft Docs"
description: "Cette page fournit des instructions sur la résolution des problèmes et la validation de la connectivité de tooend de fin d’un circuit ExpressRoute."
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
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="7c23d-103">Vérification de la connectivité ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7c23d-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="7c23d-104">ExpressRoute, qui étend un réseau local en hello cloud de Microsoft via une connexion privée qui est facilitée par un fournisseur de connectivité, implique hello suivant trois zones de réseau distinctes :</span><span class="sxs-lookup"><span data-stu-id="7c23d-104">ExpressRoute, which extends an on-premises network into hello Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves hello following three distinct network zones:</span></span>

-   <span data-ttu-id="7c23d-105">Réseau de client</span><span class="sxs-lookup"><span data-stu-id="7c23d-105">Customer Network</span></span>
-   <span data-ttu-id="7c23d-106">Réseau de fournisseur</span><span class="sxs-lookup"><span data-stu-id="7c23d-106">Provider Network</span></span>
-   <span data-ttu-id="7c23d-107">Centre de données Microsoft</span><span class="sxs-lookup"><span data-stu-id="7c23d-107">Microsoft Datacenter</span></span>

<span data-ttu-id="7c23d-108">Hello ce document vise toohelp utilisateur tooidentify où (ou même si) il existe un problème de connectivité et dans la zone, tooseek contribuant à partir de problème de hello tooresolve équipe appropriée.</span><span class="sxs-lookup"><span data-stu-id="7c23d-108">hello purpose of this document is toohelp user tooidentify where (or even if) a connectivity issue exists and within which zone, thereby tooseek help from appropriate team tooresolve hello issue.</span></span> <span data-ttu-id="7c23d-109">Si la prise en charge de Microsoft est nécessaire tooresolve un problème, ouvrez un ticket de support avec [Support technique de Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="7c23d-109">If Microsoft support is needed tooresolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c23d-110">Ce document est prévue toohelp diagnostic et résolution des problèmes de simples.</span><span class="sxs-lookup"><span data-stu-id="7c23d-110">This document is intended toohelp diagnosing and fixing simple issues.</span></span> <span data-ttu-id="7c23d-111">Il n’est pas prévue toobe un remplacement pour le support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7c23d-111">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="7c23d-112">Ouvrez un ticket de support avec [Support technique de Microsoft] [ Support] en cas de problème de hello toosolve impossible à l’aide d’instructions hello fournies.</span><span class="sxs-lookup"><span data-stu-id="7c23d-112">Open a support ticket with [Microsoft Support][Support] if you are unable toosolve hello problem using hello guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="7c23d-113">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7c23d-113">Overview</span></span>
<span data-ttu-id="7c23d-114">Hello diagramme suivant montre connectivité logique de hello d’un client réseau tooMicrosoft réseau à l’aide d’ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7c23d-114">hello following diagram shows hello logical connectivity of a customer network tooMicrosoft network using ExpressRoute.</span></span>
<span data-ttu-id="7c23d-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="7c23d-115">[![1]][1]</span></span>

<span data-ttu-id="7c23d-116">Bonjour précédant le diagramme, les nombres de hello indiquent les points clés du réseau.</span><span class="sxs-lookup"><span data-stu-id="7c23d-116">In hello preceding diagram, hello numbers indicate key network points.</span></span> <span data-ttu-id="7c23d-117">points de réseau Hello sont souvent référencés dans cet article par leur numéro associé.</span><span class="sxs-lookup"><span data-stu-id="7c23d-117">hello network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="7c23d-118">En fonction de la connectivité d’ExpressRoute hello (modèle Cloud Exchange colocalisation, connexion Ethernet de point à point ou pour tout (IPVPN)) hello réseau points 3 et 4 peuvent être commutateurs (périphériques de couche 2).</span><span class="sxs-lookup"><span data-stu-id="7c23d-118">Depending on hello ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) hello network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="7c23d-119">les points de clé réseau Hello illustrées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c23d-119">hello key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="7c23d-120">Appareil de calcul du client (par exemple, un serveur ou un PC)</span><span class="sxs-lookup"><span data-stu-id="7c23d-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="7c23d-121">CE : routeurs de périphérie du client</span><span class="sxs-lookup"><span data-stu-id="7c23d-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="7c23d-122">PE (collaborant avec des CE) : routeurs / commutateurs de périphérie du fournisseur qui collaborent avec des routeurs de périphérie du client.</span><span class="sxs-lookup"><span data-stu-id="7c23d-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="7c23d-123">Appelle tooas PE-EC dans ce document.</span><span class="sxs-lookup"><span data-stu-id="7c23d-123">Referred tooas PE-CEs in this document.</span></span>
4.  <span data-ttu-id="7c23d-124">PE (collaborant avec des MSEE) : routeurs / commutateurs de périphérie du fournisseur qui collaborent avec des MSEE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="7c23d-125">Appelle tooas PE-MSEEs dans ce document.</span><span class="sxs-lookup"><span data-stu-id="7c23d-125">Referred tooas PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="7c23d-126">MSEE : routeurs ExpressRoute Microsoft Enterprise Edge (MSEE)</span><span class="sxs-lookup"><span data-stu-id="7c23d-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="7c23d-127">Passerelle de réseau virtuel (VNet)</span><span class="sxs-lookup"><span data-stu-id="7c23d-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="7c23d-128">Dispositif de hello réseau virtuel Azure de calcul</span><span class="sxs-lookup"><span data-stu-id="7c23d-128">Compute device on hello Azure VNet</span></span>

<span data-ttu-id="7c23d-129">Si des modèles de connectivité Cloud Exchange colocalisation ou une connexion Ethernet de point à point hello sont utilisées, le routeur de périphérie client hello (2) serait établir BGP d’homologation avec MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="7c23d-129">If hello Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, hello customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="7c23d-130">Les points de réseau 3 et 4 existent toujours, mais sont quelque peu transparents en tant qu'appareils de couche 2.</span><span class="sxs-lookup"><span data-stu-id="7c23d-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="7c23d-131">Si le modèle de connectivité hello pour tout (IPVPN) est utilisé, hello PEs (accès MSEE) (4) établit BGP d’homologation avec MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="7c23d-131">If hello Any-to-any (IPVPN) connectivity model is used, hello PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="7c23d-132">Itinéraires puis propage réseau du client via le réseau de fournisseur de service de hello IPVPN toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="7c23d-132">Routes would then propagate back toohello customer network via hello IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="7c23d-133">Pour la haute disponibilité ExpressRoute, Microsoft nécessite une paire de sessions BGP redondante entre des MSEE (5) et des PE-MSEE (4).</span><span class="sxs-lookup"><span data-stu-id="7c23d-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="7c23d-134">Une paire redondante de chemins d’accès au réseau est également recommandée entre le réseau du client et les PE-CE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="7c23d-135">Toutefois, dans le modèle de connexion pour tout (IPVPN), un périphérique de CE seul (2) peut être connecté tooone ou plus PEs (3).</span><span class="sxs-lookup"><span data-stu-id="7c23d-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected tooone or more PEs (3).</span></span>
>
>

<span data-ttu-id="7c23d-136">toovalidate un circuit ExpressRoute, hello suit sont traités (avec le point de réseau hello indiqué par nombre de hello associé) :</span><span class="sxs-lookup"><span data-stu-id="7c23d-136">toovalidate an ExpressRoute circuit, hello following steps are covered (with hello network point indicated by hello associated number):</span></span>
1. [<span data-ttu-id="7c23d-137">Validation de l'approvisionnement et l’état du circuit (5)</span><span class="sxs-lookup"><span data-stu-id="7c23d-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="7c23d-138">Valider qu'au moins une homologation ExpressRoute est configurée (5)</span><span class="sxs-lookup"><span data-stu-id="7c23d-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="7c23d-139">Valider ARP entre le fournisseur de services Microsoft et hello (lien entre 4 et 5)</span><span class="sxs-lookup"><span data-stu-id="7c23d-139">Validate ARP between Microsoft and hello service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="7c23d-140">Valider le protocole BGP et itinéraires hello MSEE (BGP entre too5 4 et 5 too6 si un réseau virtuel est connecté)</span><span class="sxs-lookup"><span data-stu-id="7c23d-140">Validate BGP and routes on hello MSEE (BGP between 4 too5, and 5 too6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="7c23d-141">Hello de vérification des statistiques de trafic (trafic passant par 5)</span><span class="sxs-lookup"><span data-stu-id="7c23d-141">Check hello Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="7c23d-142">Plusieurs validations et les vérifications seront ajoutées dans hello future, vérifier tous les mois !</span><span class="sxs-lookup"><span data-stu-id="7c23d-142">More validations and checks will be added in hello future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="7c23d-143">Validation de l'approvisionnement et l’état du circuit</span><span class="sxs-lookup"><span data-stu-id="7c23d-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="7c23d-144">Quel que soit le modèle de connectivité de hello, un circuit ExpressRoute a toobe créée et, par conséquent, un service de clé générée pour l’approvisionnement du circuit.</span><span class="sxs-lookup"><span data-stu-id="7c23d-144">Regardless of hello connectivity model, an ExpressRoute circuit has toobe created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="7c23d-145">L’approvisionnement d’un circuit ExpressRoute établit une connexion de couche 2 redondante entre les PE-MSEE (4) et les MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="7c23d-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="7c23d-146">Pour plus d’informations sur la façon dont toocreate, modifier, de configurer et vérifier un circuit ExpressRoute, consultez l’article de hello [créer et modifier un circuit ExpressRoute][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="7c23d-146">For more information on how toocreate, modify, provision, and verify an ExpressRoute circuit, see hello article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="7c23d-147">Une clé de service identifie un circuit ExpressRoute de façon unique.</span><span class="sxs-lookup"><span data-stu-id="7c23d-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="7c23d-148">Cette clé est requise pour la plupart des commandes powershell de hello mentionnés dans ce document.</span><span class="sxs-lookup"><span data-stu-id="7c23d-148">This key is required for most of hello powershell commands mentioned in this document.</span></span> <span data-ttu-id="7c23d-149">En outre, si vous avez besoin obtenir de l’aide de Microsoft ou d’un tootroubleshoot de partenaire ExpressRoute un problème d’ExpressRoute, servir hello tooreadily clé identifier circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner tootroubleshoot an ExpressRoute issue, provide hello service key tooreadily identify hello circuit.</span></span>
>
>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="7c23d-150">Vérification par hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7c23d-150">Verification via hello Azure portal</span></span>
<span data-ttu-id="7c23d-151">Bonjour portail Azure, état hello d’un circuit ExpressRoute peut être vérifiée en sélectionnant ![2][2] sur hello menu de barre de côté gauche, puis en sélectionnant hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7c23d-151">In hello Azure portal, hello status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="7c23d-152">En sélectionnant un ExpressRoute circuit sous « Toutes les ressources » ouvre le panneau de circuit ExpressRoute de hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-152">Selecting an ExpressRoute circuit listed under "All resources" opens hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="7c23d-153">Bonjour ![3][3] section du panneau hello, hello ExpressRoute essentials sont répertoriés comme indiqué dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="7c23d-153">In hello ![3][3] section of hello blade, hello ExpressRoute essentials are listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="7c23d-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="7c23d-154">![4][4]</span></span>    

<span data-ttu-id="7c23d-155">Bonjour ExpressRoute Essentials, *Circuit état* indique l’état hello du circuit hello sur hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7c23d-155">In hello ExpressRoute Essentials, *Circuit status* indicates hello status of hello circuit on hello Microsoft side.</span></span> <span data-ttu-id="7c23d-156">*État du fournisseur* indique si le circuit de hello a été *préparé non configuré* côté fournisseur de services de hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-156">*Provider status* indicates if hello circuit has been *Provisioned/Not provisioned* on hello service-provider side.</span></span> 

<span data-ttu-id="7c23d-157">Pour un toobe de circuit ExpressRoute opérationnel, hello *Circuit état* doit être *activé* et hello *état du fournisseur* doit être *configuré*.</span><span class="sxs-lookup"><span data-stu-id="7c23d-157">For an ExpressRoute circuit toobe operational, hello *Circuit status* must be *Enabled* and hello *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="7c23d-158">Si hello *Circuit état* est désactivée, contactez [Support technique de Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="7c23d-158">If hello *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="7c23d-159">Si hello *état du fournisseur* est ne pas configurée, contactez votre fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="7c23d-159">If hello *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="7c23d-160">Vérification par le biais de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c23d-160">Verification via PowerShell</span></span>
<span data-ttu-id="7c23d-161">toolist tous hello circuits ExpressRoute dans un groupe de ressources, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c23d-161">toolist all hello ExpressRoute circuits in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="7c23d-162">Vous pouvez obtenir le nom de votre groupe de ressources via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7c23d-162">You can get your resource group name through hello Azure portal.</span></span> <span data-ttu-id="7c23d-163">Consultez la sous-section précédente de hello de ce document et prenez note de que ce nom de groupe de ressources hello est répertorié dans la capture d’écran : exemple hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-163">See hello previous subsection of this document and note that hello resource group name is listed in hello example screen shot.</span></span>
>
>

<span data-ttu-id="7c23d-164">tooselect un circuit ExpressRoute particulier dans un groupe de ressources, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c23d-164">tooselect a particular ExpressRoute circuit in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="7c23d-165">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="7c23d-165">A sample response is:</span></span>

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

<span data-ttu-id="7c23d-166">tooconfirm si un circuit ExpressRoute est opérationnel, payer toohello une attention toute particulière champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="7c23d-166">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="7c23d-167">Si hello *état d’approvisionnement* est désactivée, contactez [Support technique de Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="7c23d-167">If hello *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="7c23d-168">Si hello *ServiceProviderProvisioningState* est ne pas configurée, contactez votre fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="7c23d-168">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="7c23d-169">Vérification par le biais de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="7c23d-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="7c23d-170">toolist tous hello circuits ExpressRoute sous un abonnement, utilisez hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c23d-170">toolist all hello ExpressRoute circuits under a subscription, use hello following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="7c23d-171">tooselect un circuit ExpressRoute particulier, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c23d-171">tooselect a particular ExpressRoute circuit, use hello following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="7c23d-172">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="7c23d-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="7c23d-173">tooconfirm si un circuit ExpressRoute est opérationnel, payer toohello une attention toute particulière suivant champs : ServiceProviderProvisioningState : état de mise en service : activé</span><span class="sxs-lookup"><span data-stu-id="7c23d-173">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="7c23d-174">Si hello *état* est désactivée, contactez [Support technique de Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="7c23d-174">If hello *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="7c23d-175">Si hello *ServiceProviderProvisioningState* est ne pas configurée, contactez votre fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="7c23d-175">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="7c23d-176">Validation de la configuration de l’homologation</span><span class="sxs-lookup"><span data-stu-id="7c23d-176">Validate Peering Configuration</span></span>
<span data-ttu-id="7c23d-177">Fournisseur de services hello après hello terminé approvisionnement du circuit ExpressRoute de hello, une configuration de routage peut être créée sur hello circuit ExpressRoute entre MSEE-réservations persistantes (4) et MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="7c23d-177">After hello service provider has completed hello provisioning hello ExpressRoute circuit, a routing configuration can be created over hello ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="7c23d-178">Chaque circuit ExpressRoute peut avoir une, deux ou trois contextes de routage activés : homologation privée Azure (trafic tooprivate réseaux virtuels dans Azure), homologation publique Azure (trafic toopublic adresses dans Azure) et (le trafic tooOffice 365 d’homologation Microsoft et Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="7c23d-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic tooprivate virtual networks in Azure), Azure public peering (traffic toopublic IP addresses in Azure), and Microsoft peering (traffic tooOffice 365 and Dynamics 365).</span></span> <span data-ttu-id="7c23d-179">Pour plus d’informations sur la façon de toocreate et modifier la configuration de routage, consultez l’article hello [créer et modifier le routage pour un circuit ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="7c23d-179">For more information on how toocreate and modify routing configuration, see hello article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="7c23d-180">Vérification par hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7c23d-180">Verification via hello Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="7c23d-181">Il existe un bogue connu dans hello portail Azure, dans laquelle les homologations ExpressRoute sont *pas* indiquées dans le portail hello si configuré par le fournisseur de services hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-181">There is a known bug in hello Azure portal wherein ExpressRoute peerings are *NOT* shown in hello portal if configured by hello service provider.</span></span> <span data-ttu-id="7c23d-182">Ajout des homologations ExpressRoute via le portail de hello ou PowerShell *remplace les paramètres du fournisseur de service hello*.</span><span class="sxs-lookup"><span data-stu-id="7c23d-182">Adding ExpressRoute peerings via hello portal or PowerShell *overwrites hello service provider settings*.</span></span> <span data-ttu-id="7c23d-183">Cette action interrompt hello routage sur le circuit ExpressRoute de hello et requiert la prise en charge de hello hello fournisseur toorestore hello de paramètres de service et rétablir le routage normal.</span><span class="sxs-lookup"><span data-stu-id="7c23d-183">This action breaks hello routing on hello ExpressRoute circuit and requires hello support of hello service provider toorestore hello settings and reestablish normal routing.</span></span> <span data-ttu-id="7c23d-184">Modifiez uniquement hello ExpressRoute homologations s’il est certain que ce fournisseur de service hello fournit uniquement les services de couche 2 !</span><span class="sxs-lookup"><span data-stu-id="7c23d-184">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="7c23d-185">Si la couche 3 est fournie par hello homologations de fournisseur et hello du service sont vides dans le portail de hello, PowerShell peut être utilisé toosee hello service fournisseur configuré paramètres.</span><span class="sxs-lookup"><span data-stu-id="7c23d-185">If layer 3 is provided by hello service provider and hello peerings are blank in hello portal, PowerShell can be used toosee hello service provider configured settings.</span></span>
>
>

<span data-ttu-id="7c23d-186">Bonjour portail Azure, l’état d’un circuit ExpressRoute peut être vérifiée en sélectionnant ![2][2] sur hello menu de barre de côté gauche, puis en sélectionnant hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7c23d-186">In hello Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="7c23d-187">En sélectionnant un ExpressRoute circuit sous « Toutes les ressources » pour ouvrir Panneau de circuit ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-187">Selecting an ExpressRoute circuit listed under "All resources" would open hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="7c23d-188">Bonjour ![3][3] section du panneau hello, hello ExpressRoute essentials sont répertoriés comme indiqué dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="7c23d-188">In hello ![3][3] section of hello blade, hello ExpressRoute essentials would be listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="7c23d-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="7c23d-189">![5][5]</span></span>

<span data-ttu-id="7c23d-190">Bonjour précédent exemple, Azure indiqués contexte de routage d’homologation privée est activée, alors que Azure public et les contextes de routage d’homologation Microsoft ne sont pas activés.</span><span class="sxs-lookup"><span data-stu-id="7c23d-190">In hello preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="7c23d-191">Un contexte d’homologation a été activé correctement aurait également les sous-réseaux de point à point principaux et secondaires (requis pour le protocole BGP) hello répertoriés.</span><span class="sxs-lookup"><span data-stu-id="7c23d-191">A successfully enabled peering context would also have hello primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="7c23d-192">les sous-réseaux Hello /30 sont utilisés pour l’adresse IP hello interface hello MSEEs et MSEEs-PE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-192">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="7c23d-193">Si une homologation n’est pas activée, vérifiez si sous-réseaux principaux et secondaires hello affectés correspond à configuration hello sur PE-MSEEs.</span><span class="sxs-lookup"><span data-stu-id="7c23d-193">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on PE-MSEEs.</span></span> <span data-ttu-id="7c23d-194">Si non, toochange à la configuration hello sur les routeurs MSEE, consultez trop[créer et modifier le routage pour un circuit ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="7c23d-194">If not, toochange hello configuration on MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="7c23d-195">Vérification par le biais de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c23d-195">Verification via PowerShell</span></span>
<span data-ttu-id="7c23d-196">tooget hello Azure privé d’homologation détails de configuration, utilisez hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="7c23d-196">tooget hello Azure private peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="7c23d-197">Voici un exemple de réponse pour une homologation privée correctement configurée :</span><span class="sxs-lookup"><span data-stu-id="7c23d-197">A sample response, for a successfully configured private peering, is:</span></span>

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

 <span data-ttu-id="7c23d-198">Un contexte d’homologation a été activé correctement aurait des préfixes d’adresse principale et secondaire hello répertoriés.</span><span class="sxs-lookup"><span data-stu-id="7c23d-198">A successfully enabled peering context would have hello primary and secondary address prefixes listed.</span></span> <span data-ttu-id="7c23d-199">les sous-réseaux Hello /30 sont utilisés pour l’adresse IP hello interface hello MSEEs et MSEEs-PE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-199">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="7c23d-200">tooget hello Azure public d’homologation détails de configuration, utilisez hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="7c23d-200">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="7c23d-201">tooget hello Microsoft d’homologation détails de configuration, utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="7c23d-201">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="7c23d-202">Si aucune homologation n’est configurée, un message d’erreur est généré.</span><span class="sxs-lookup"><span data-stu-id="7c23d-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="7c23d-203">Un exemple de réponse, lorsque hello indiquée d’homologation (Azure publics d’homologation dans cet exemple) n’est pas configuré dans le circuit de hello :</span><span class="sxs-lookup"><span data-stu-id="7c23d-203">A sample response, when hello stated peering (Azure Public peering in this example) is not configured within hello circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="7c23d-204">Si une homologation n’est pas activée, vérifiez si configuration hello sous-réseaux principaux et secondaires affectés correspondance hello hello lié PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-204">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="7c23d-205">Également vérifier si hello corriger *VlanId*, *AzureASN*, et *PeerASN* sont utilisés sur MSEEs et si ces valeurs est mappé toohello que ceux utilisés sur hello lié PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-205">Also check if hello correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="7c23d-206">Si le hachage MD5 est choisie, doit être les même sur MSEE et PE-MSEE paire clé partagée de hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-206">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="7c23d-207">configuration de hello toochange sur les routeurs MSEE hello, consultez trop [créer et modifier le routage pour un circuit ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="7c23d-207">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="7c23d-208">Vérification par le biais de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="7c23d-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="7c23d-209">tooget hello Azure privé d’homologation détails de configuration, utilisez hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c23d-209">tooget hello Azure private peering configuration details, use hello following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="7c23d-210">Voici un exemple de réponse pour une homologation privée correctement configurée :</span><span class="sxs-lookup"><span data-stu-id="7c23d-210">A sample response, for a successfully configured private peering is:</span></span>

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

<span data-ttu-id="7c23d-211">A été activée avec succès, contexte d’homologation aurait sous-réseaux homologue principal et secondaire de hello répertoriés.</span><span class="sxs-lookup"><span data-stu-id="7c23d-211">A successfully, enabled peering context would have hello primary and secondary peer subnets listed.</span></span> <span data-ttu-id="7c23d-212">les sous-réseaux Hello /30 sont utilisés pour l’adresse IP hello interface hello MSEEs et MSEEs-PE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-212">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="7c23d-213">tooget hello Azure public d’homologation détails de configuration, utilisez hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="7c23d-213">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="7c23d-214">tooget hello Microsoft d’homologation détails de configuration, utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="7c23d-214">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="7c23d-215">Si homologations de couche 3 ont été définies par le fournisseur de services hello, paramètre homologations de ExpressRoute hello via le portail de hello ou PowerShell remplace les paramètres du fournisseur de service hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-215">If layer 3 peerings were set by hello service provider, setting hello ExpressRoute peerings via hello portal or PowerShell overwrites hello service provider settings.</span></span> <span data-ttu-id="7c23d-216">La réinitialisation des paramètres d’homologation du côté fournisseur hello requiert la prise en charge de hello hello du fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="7c23d-216">Resetting hello provider side peering settings requires hello support of hello service provider.</span></span> <span data-ttu-id="7c23d-217">Modifiez uniquement hello ExpressRoute homologations s’il est certain que ce fournisseur de service hello fournit uniquement les services de couche 2 !</span><span class="sxs-lookup"><span data-stu-id="7c23d-217">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="7c23d-218">Si une homologation n’est pas activée, vérifiez si hello homologue principal et secondaire sous-réseaux affectés correspondance hello configuration sur hello lié PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-218">If a peering is not enabled, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="7c23d-219">Également vérifier si hello corriger *VlanId*, *AzureAsn*, et *PeerAsn* sont utilisés sur MSEEs et si ces valeurs est mappé toohello que ceux utilisés sur hello lié PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-219">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="7c23d-220">configuration de hello toochange sur les routeurs MSEE hello, consultez trop [créer et modifier le routage pour un circuit ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="7c23d-220">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a><span data-ttu-id="7c23d-221">Valider ARP entre le fournisseur de services Microsoft et hello</span><span class="sxs-lookup"><span data-stu-id="7c23d-221">Validate ARP between Microsoft and hello service provider</span></span>
<span data-ttu-id="7c23d-222">Cette section utilise les commandes PowerShell (classiques).</span><span class="sxs-lookup"><span data-stu-id="7c23d-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="7c23d-223">Si vous avez utilisé les commandes PowerShell Azure Resource Manager, assurez-vous que vous disposez d’abonnement de toohello d’accès d’administrateur/co-admin via [portail Azure classic][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="7c23d-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="7c23d-224">Pour le dépannage à l’aide du Gestionnaire de ressources Azure commandes reportez-vous toohello [tables ARP de mise en route dans le modèle de déploiement du Gestionnaire de ressources hello] [ ARP] document.</span><span class="sxs-lookup"><span data-stu-id="7c23d-224">For troubleshooting using Azure Resource Manager commands please refer toohello [Getting ARP tables in hello Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="7c23d-225">tooget ARP, hello portail Azure et commandes Azure PowerShell de gestionnaire de ressources peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="7c23d-225">tooget ARP, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="7c23d-226">Si vous rencontrez des erreurs avec les commandes du Gestionnaire de ressources PowerShell Azure hello, les commandes PowerShell classiques doivent fonctionner en tant que PowerShell classique, les commandes fonctionnent également avec des circuits ExpressRoute de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="7c23d-226">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="7c23d-227">tooget hello table ARP à partir du routeur MSEE principal hello pour l’homologation privée hello, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c23d-227">tooget hello ARP table from hello primary MSEE router for hello private peering, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="7c23d-228">Un exemple de réponse pour la commande hello, dans un scénario de réussite hello :</span><span class="sxs-lookup"><span data-stu-id="7c23d-228">An example response for hello command, in hello successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="7c23d-229">De même, vous pouvez vérifier hello table ARP de hello MSEE Bonjour *principal*/*secondaire* chemin d’accès, pour *privé* /  *Public*/*Microsoft* homologations.</span><span class="sxs-lookup"><span data-stu-id="7c23d-229">Similarly, you can check hello ARP table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="7c23d-230">Hello exemple suivant montre hello réponse de la commande hello pour une homologation n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="7c23d-230">hello following example shows hello response of hello command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="7c23d-231">Si hello table ARP ne dispose pas des adresses IP des interfaces de hello mappé tooMAC adresses, hello révision informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c23d-231">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
>1. <span data-ttu-id="7c23d-232">Si hello première adresse IP du sous-réseau de hello /30 affecté pour la liaison hello entre hello MSEE-PR et MSEE est utilisé sur l’interface hello de MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="7c23d-232">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="7c23d-233">Azure utilise toujours l’adresse IP de la deuxième hello pour MSEEs.</span><span class="sxs-lookup"><span data-stu-id="7c23d-233">Azure always uses hello second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="7c23d-234">Vérifiez si le client hello (C-Tag) et balises VLAN de service (S-Tag) correspondent à la fois sur la paire de MSEE-PR et MSEE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-234">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a><span data-ttu-id="7c23d-235">Valider BGP et itinéraires hello MSEE</span><span class="sxs-lookup"><span data-stu-id="7c23d-235">Validate BGP and routes on hello MSEE</span></span>
<span data-ttu-id="7c23d-236">Cette section utilise les commandes PowerShell (classiques).</span><span class="sxs-lookup"><span data-stu-id="7c23d-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="7c23d-237">Si vous avez utilisé les commandes PowerShell Azure Resource Manager, assurez-vous que vous disposez d’abonnement de toohello d’accès d’administrateur/co-admin via [portail Azure classic][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="7c23d-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="7c23d-238">tooget BGP plus d’informations, les deux hello portail Azure et les commandes PowerShell de gestionnaire de ressources Azure peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="7c23d-238">tooget BGP information, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="7c23d-239">Si vous rencontrez des erreurs avec les commandes du Gestionnaire de ressources PowerShell Azure hello, les commandes PowerShell classiques doivent fonctionner en tant que PowerShell classique, les commandes fonctionnent également avec des circuits ExpressRoute de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="7c23d-239">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="7c23d-240">tooget hello table de routage (voisin BGP) pour un contexte de routage spécifique, utilisez les hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c23d-240">tooget hello routing table (BGP neighbor) summary for a particular routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="7c23d-241">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="7c23d-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="7c23d-242">Comme indiqué dans le précédent exemple de hello, commande hello est toodetermine utile pour la durée pendant laquelle le contexte de routage hello a été établie.</span><span class="sxs-lookup"><span data-stu-id="7c23d-242">As shown in hello preceding example, hello command is useful toodetermine for how long hello routing context has been established.</span></span> <span data-ttu-id="7c23d-243">Il indique également le nombre de préfixes d’itinéraire publié par routeur d’homologation de hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-243">It also indicates number of route prefixes advertised by hello peering router.</span></span>

>[!NOTE]
><span data-ttu-id="7c23d-244">Si l’état du hello est actif ou inactif, vérifiez si hello homologue principal et secondaire sous-réseaux affectés correspondance hello configuration sur hello lié PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-244">If hello state is in Active or Idle, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="7c23d-245">Également vérifier si hello corriger *VlanId*, *AzureAsn*, et *PeerAsn* sont utilisés sur MSEEs et si ces valeurs est mappé toohello que ceux utilisés sur hello lié PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="7c23d-245">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="7c23d-246">Si le hachage MD5 est choisie, doit être les même sur MSEE et PE-MSEE paire clé partagée de hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-246">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="7c23d-247">configuration de hello toochange sur les routeurs MSEE hello, consultez trop[créer et modifier le routage pour un circuit ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="7c23d-247">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="7c23d-248">Si certaines destinations ne sont pas accessibles via une homologation particulier, vérifiez la table d’itinéraires hello de MSEEs hello appartenant toohello de contexte d’homologation particulier.</span><span class="sxs-lookup"><span data-stu-id="7c23d-248">If certain destinations are not reachable over a particular peering, check hello route table of hello MSEEs belonging toohello particular peering context.</span></span> <span data-ttu-id="7c23d-249">Si un préfixe correspondant (NATed IP possible) est présent dans la table de routage hello, vérifiez s’il existe des pare-feu/groupe de sécurité réseau/ACL sur le chemin d’accès hello et si elles autorisent le trafic de hello.</span><span class="sxs-lookup"><span data-stu-id="7c23d-249">If a matching prefix (could be NATed IP) is present in hello routing table, then check if there are firewalls/NSG/ACLs on hello path and if they permit hello traffic.</span></span>
>
>

<span data-ttu-id="7c23d-250">tooget hello table de routage complète à partir de MSEE sur hello *principal* chemin d’accès pour hello particulier *privé* contexte de routage, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c23d-250">tooget hello full routing table from MSEE on hello *Primary* path for hello particular *Private* routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="7c23d-251">Un résultat réussi exemple de commande hello est la suivante :</span><span class="sxs-lookup"><span data-stu-id="7c23d-251">An example successful outcome for hello command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="7c23d-252">De même, vous pouvez vérifier la table de routage hello de hello MSEE Bonjour *principal*/*secondaire* chemin d’accès, pour *privé* / *Public*/*Microsoft* un contexte d’homologation.</span><span class="sxs-lookup"><span data-stu-id="7c23d-252">Similarly, you can check hello routing table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="7c23d-253">Hello exemple suivant montre hello réponse de la commande hello pour une homologation n’existe pas :</span><span class="sxs-lookup"><span data-stu-id="7c23d-253">hello following example shows hello response of hello command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a><span data-ttu-id="7c23d-254">Vérifiez hello statistiques de trafic</span><span class="sxs-lookup"><span data-stu-id="7c23d-254">Check hello Traffic Statistics</span></span>
<span data-ttu-id="7c23d-255">tooget hello combiné des statistiques de trafic du chemin d’accès primaire et secondaire--octets et l’extraction--d’un contexte d’homologation, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c23d-255">tooget hello combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="7c23d-256">Un exemple de sortie de la commande hello est :</span><span class="sxs-lookup"><span data-stu-id="7c23d-256">A sample output of hello command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="7c23d-257">Un exemple de sortie de la commande hello pour une homologation inexistante est :</span><span class="sxs-lookup"><span data-stu-id="7c23d-257">A sample output of hello command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="7c23d-258">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c23d-258">Next Steps</span></span>
<span data-ttu-id="7c23d-259">Pour plus d’informations ou de l’aide, consultez hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="7c23d-259">For more information or help, check out hello following links:</span></span>

- <span data-ttu-id="7c23d-260">[Support Microsoft][Support]</span><span class="sxs-lookup"><span data-stu-id="7c23d-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="7c23d-261">[Création et modification d’un circuit ExpressRoute][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="7c23d-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="7c23d-262">[Créer et modifier le routage le routage pour un circuit ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="7c23d-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Connectivité logique Express Route"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Icône Toutes les ressources"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Icône Vue d’ensemble"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Capture d’écran : exemple pour ExpressRoute Essentials"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Capture d’écran : exemple pour ExpressRoute Essentials"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






