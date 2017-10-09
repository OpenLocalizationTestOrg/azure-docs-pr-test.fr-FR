---
title: "Comment tooconfigure routage (homologation) pour un circuit ExpressRoute : Azure : classique | Documents Microsoft"
description: "Cet article vous guide tout au long des étapes hello pour la création et l’approvisionnement hello privés, publics et homologation Microsoft d’un circuit ExpressRoute. Cet article vous explique également comment toocheck état de hello, mettre à jour ou supprimer des homologations pour votre circuit."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="56b20-104">Créer et modifier l’homologation pour un circuit ExpressRoute (Classic)</span><span class="sxs-lookup"><span data-stu-id="56b20-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56b20-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="56b20-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="56b20-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56b20-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="56b20-107">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="56b20-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="56b20-108">Vidéo - Homologation privée</span><span class="sxs-lookup"><span data-stu-id="56b20-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="56b20-109">Vidéo - Homologation publique</span><span class="sxs-lookup"><span data-stu-id="56b20-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="56b20-110">Vidéo - Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="56b20-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="56b20-111">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="56b20-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="56b20-112">Cet article vous guide tout au long de hello étapes toocreate et gérer la configuration de routage pour un circuit ExpressRoute à l’aide du modèle de déploiement classique de PowerShell et hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="56b20-113">Hello étapes ci-dessous vous également montrent comment toocheck état de hello, mettre à jour, ou supprimez et annuler le déploiement homologations pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="56b20-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="56b20-114">**À propos des modèles de déploiement Azure**</span><span class="sxs-lookup"><span data-stu-id="56b20-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="56b20-115">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="56b20-115">Configuration prerequisites</span></span>
* <span data-ttu-id="56b20-116">Vous devez hello dernière version de hello applets de commande PowerShell de gestion de Service Azure (SM).</span><span class="sxs-lookup"><span data-stu-id="56b20-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="56b20-117">Pour en savoir plus, voir [Prise en main des applets de commande PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="56b20-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="56b20-118">Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md) page hello [exigences routage](expressroute-routing.md) page et hello [workflows](expressroute-workflows.md) page avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="56b20-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="56b20-119">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="56b20-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="56b20-120">Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="56b20-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="56b20-121">Hello circuit ExpressRoute doit être dans un état configuré et activé pour vous toobe toorun en mesure de hello applets de commande décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="56b20-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56b20-122">Ces instructions s’appliquent uniquement à toocircuits créé avec les fournisseurs de services offrant des services de connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="56b20-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="56b20-123">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement IPVPN, à l’image de MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="56b20-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="56b20-124">Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="56b20-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="56b20-125">Vous pouvez configurer les homologations dans l’ordre de votre choix.</span><span class="sxs-lookup"><span data-stu-id="56b20-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="56b20-126">Toutefois, il se peut que vous devez vous assurer que vous terminez configuration hello de chacun d’eux à la fois d’homologation.</span><span class="sxs-lookup"><span data-stu-id="56b20-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="56b20-127">Connectez-vous à tooyour compte Azure, puis sélectionnez un abonnement</span><span class="sxs-lookup"><span data-stu-id="56b20-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="56b20-128">Ouvrez la console PowerShell avec des droits élevés et tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="56b20-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="56b20-129">Utilisez hello suivant toohelp exemple que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="56b20-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="56b20-130">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="56b20-131">Si vous avez plusieurs abonnements, sélectionnez l’abonnement hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="56b20-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="56b20-132">Ensuite, utilisez hello suivant l’applet de commande tooadd tooPowerShell de votre abonnement Azure pour le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="56b20-133">Homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="56b20-133">Azure private peering</span></span>
<span data-ttu-id="56b20-134">Cette section fournit des instructions sur la façon dont toocreate, obtenir, mettre à jour et supprimer des hello Azure configuration d’homologation privée pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="56b20-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="56b20-135">toocreate l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="56b20-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="56b20-136">**Importez le module PowerShell de hello pour ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="56b20-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="56b20-137">Vous devez importer les modules Azure et ExpressRoute hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="56b20-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="56b20-138">Les commandes de suivantes de hello exécution tooimport hello Azure et ExpressRoute les modules dans la session de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="56b20-139">**Créez un circuit ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="56b20-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="56b20-140">Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-classic.md) et configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="56b20-141">Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous.</span><span class="sxs-lookup"><span data-stu-id="56b20-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="56b20-142">Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="56b20-143">Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, suivez les instructions hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="56b20-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="56b20-144">**Vérifiez tooensure de circuit ExpressRoute hello que s’il est configuré.**</span><span class="sxs-lookup"><span data-stu-id="56b20-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="56b20-145">Vous devez tout d’abord vérifier toosee si hello circuit ExpressRoute est configuré et également activé.</span><span class="sxs-lookup"><span data-stu-id="56b20-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="56b20-146">Consultez l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="56b20-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="56b20-147">Assurez-vous que le circuit de hello montre comme configuré et activé.</span><span class="sxs-lookup"><span data-stu-id="56b20-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="56b20-148">Si ce n’est pas le cas, fonctionne avec votre tooget de fournisseur de connectivité votre état toohello requis de circuit et l’état.</span><span class="sxs-lookup"><span data-stu-id="56b20-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="56b20-149">**Configurer une homologation privée Azure pour le circuit de hello.**</span><span class="sxs-lookup"><span data-stu-id="56b20-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="56b20-150">Assurez-vous que vous disposez des éléments suivants avant de passer aux étapes suivantes de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="56b20-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="56b20-151">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="56b20-152">Ce sous-réseau ne doit faire partie d’aucun espace d'adressage réservé aux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="56b20-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="56b20-153">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="56b20-154">Ce sous-réseau ne doit faire partie d’aucun espace d'adressage réservé aux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="56b20-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="56b20-155">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="56b20-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="56b20-156">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="56b20-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="56b20-157">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="56b20-157">AS number for peering.</span></span> <span data-ttu-id="56b20-158">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="56b20-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="56b20-159">Vous pouvez utiliser un numéro AS privé pour cette homologation.</span><span class="sxs-lookup"><span data-stu-id="56b20-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="56b20-160">Veillez à ne pas utiliser le numéro 65515.</span><span class="sxs-lookup"><span data-stu-id="56b20-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="56b20-161">Un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="56b20-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="56b20-162">**Cette étape est facultative**.</span><span class="sxs-lookup"><span data-stu-id="56b20-162">**This is optional**.</span></span>
     
    <span data-ttu-id="56b20-163">Vous pouvez exécuter hello suivant tooconfigure applet de commande d’homologation privée Azure pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="56b20-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="56b20-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="56b20-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="56b20-165">Vous pouvez utiliser la cmdlet hello ci-dessous si vous choisissez toouse un hachage MD5.</span><span class="sxs-lookup"><span data-stu-id="56b20-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="56b20-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="56b20-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="56b20-167">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="56b20-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="56b20-168">tooview Azure privé d’homologation détails</span><span class="sxs-lookup"><span data-stu-id="56b20-168">tooview Azure private peering details</span></span>
<span data-ttu-id="56b20-169">Vous pouvez obtenir les détails de configuration à l’aide de hello suivant l’applet de commande</span><span class="sxs-lookup"><span data-stu-id="56b20-169">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="56b20-170">tooupdate configuration d’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="56b20-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="56b20-171">Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello suivant l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="56b20-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="56b20-172">Dans l’exemple hello ci-dessous, hello ID de VLAN de circuit de hello est mise à jour à partir de 100 too500.</span><span class="sxs-lookup"><span data-stu-id="56b20-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="56b20-173">toodelete l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="56b20-173">toodelete Azure private peering</span></span>
<span data-ttu-id="56b20-174">Vous pouvez supprimer la configuration d’homologation par hello suivant l’applet de commande en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="56b20-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="56b20-175">Vous devez vous assurer que tous les réseaux virtuels sont dissocier hello circuit ExpressRoute avant d’exécuter cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="56b20-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="56b20-176">Homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="56b20-176">Azure public peering</span></span>
<span data-ttu-id="56b20-177">Cette section fournit des instructions sur la façon dont toocreate, obtenir, mettre à jour et supprimer des hello configuration d’homologation publique Azure pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="56b20-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="56b20-178">toocreate l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="56b20-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="56b20-179">**Importez le module PowerShell de hello pour ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="56b20-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="56b20-180">Vous devez importer les modules Azure et ExpressRoute hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="56b20-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="56b20-181">Les commandes de suivantes de hello exécution tooimport hello Azure et ExpressRoute les modules dans la session de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="56b20-182">**Création d’un circuit ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="56b20-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="56b20-183">Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-classic.md) et configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="56b20-184">Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure public d’homologation pour vous.</span><span class="sxs-lookup"><span data-stu-id="56b20-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="56b20-185">Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="56b20-186">Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, suivez les instructions hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="56b20-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="56b20-187">**Vérifiez tooensure de circuit ExpressRoute que s’il est configuré**</span><span class="sxs-lookup"><span data-stu-id="56b20-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="56b20-188">Vous devez tout d’abord vérifier toosee si hello circuit ExpressRoute est configuré et également activé.</span><span class="sxs-lookup"><span data-stu-id="56b20-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="56b20-189">Consultez l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="56b20-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="56b20-190">Assurez-vous que le circuit de hello montre comme configuré et activé.</span><span class="sxs-lookup"><span data-stu-id="56b20-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="56b20-191">Si ce n’est pas le cas, fonctionne avec votre tooget de fournisseur de connectivité votre état toohello requis de circuit et l’état.</span><span class="sxs-lookup"><span data-stu-id="56b20-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="56b20-192">**Configurer l’homologation publique Azure pour le circuit de hello**</span><span class="sxs-lookup"><span data-stu-id="56b20-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="56b20-193">Assurez-vous que vous disposez des informations suivantes avant de continuer davantage de hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="56b20-194">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="56b20-195">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="56b20-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="56b20-196">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="56b20-197">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="56b20-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="56b20-198">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="56b20-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="56b20-199">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="56b20-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="56b20-200">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="56b20-200">AS number for peering.</span></span> <span data-ttu-id="56b20-201">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="56b20-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="56b20-202">Un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="56b20-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="56b20-203">**Cette étape est facultative**.</span><span class="sxs-lookup"><span data-stu-id="56b20-203">**This is optional**.</span></span>
     
    <span data-ttu-id="56b20-204">Vous pouvez exécuter hello suivant tooconfigure applet de commande pour l’homologation publique Azure pour votre circuit</span><span class="sxs-lookup"><span data-stu-id="56b20-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="56b20-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="56b20-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="56b20-206">Vous pouvez utiliser la cmdlet hello ci-dessous si vous choisissez toouse un hachage MD5</span><span class="sxs-lookup"><span data-stu-id="56b20-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="56b20-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="56b20-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="56b20-208">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="56b20-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="56b20-209">tooview Azure public d’homologation détails</span><span class="sxs-lookup"><span data-stu-id="56b20-209">tooview Azure public peering details</span></span>
<span data-ttu-id="56b20-210">Vous pouvez obtenir les détails de configuration à l’aide de hello suivant l’applet de commande</span><span class="sxs-lookup"><span data-stu-id="56b20-210">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="56b20-211">tooupdate configuration d’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="56b20-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="56b20-212">Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello suivant l’applet de commande</span><span class="sxs-lookup"><span data-stu-id="56b20-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="56b20-213">Hello, ID de VLAN de circuit de hello est mise à jour à partir de 200 too600 Bonjour à l’exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="56b20-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="56b20-214">toodelete l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="56b20-214">toodelete Azure public peering</span></span>
<span data-ttu-id="56b20-215">Vous pouvez supprimer votre configuration d’homologation par hello suivant l’applet de commande en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="56b20-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="56b20-216">Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="56b20-216">Microsoft peering</span></span>
<span data-ttu-id="56b20-217">Cette section fournit des instructions sur la façon dont toocreate, obtenir, mettre à jour et supprimer la configuration d’homologation Microsoft hello pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="56b20-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="56b20-218">l’homologation de Microsoft toocreate</span><span class="sxs-lookup"><span data-stu-id="56b20-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="56b20-219">**Importez le module PowerShell de hello pour ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="56b20-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="56b20-220">Vous devez importer les modules Azure et ExpressRoute hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="56b20-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="56b20-221">Les commandes de suivantes de hello exécution tooimport hello Azure et ExpressRoute les modules dans la session de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="56b20-222">**Création d’un circuit ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="56b20-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="56b20-223">Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-classic.md) et configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="56b20-224">Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous.</span><span class="sxs-lookup"><span data-stu-id="56b20-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="56b20-225">Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="56b20-226">Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, suivez les instructions hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="56b20-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="56b20-227">**Vérifiez tooensure de circuit ExpressRoute que s’il est configuré**</span><span class="sxs-lookup"><span data-stu-id="56b20-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="56b20-228">Vous devez tout d’abord vérifier toosee si hello circuit ExpressRoute est en état préparé et activé.</span><span class="sxs-lookup"><span data-stu-id="56b20-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="56b20-229">Assurez-vous que le circuit de hello montre comme configuré et activé.</span><span class="sxs-lookup"><span data-stu-id="56b20-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="56b20-230">Si ce n’est pas le cas, fonctionne avec votre tooget de fournisseur de connectivité votre état toohello requis de circuit et l’état.</span><span class="sxs-lookup"><span data-stu-id="56b20-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="56b20-231">**Configuration de Microsoft d’homologation pour le circuit de hello**</span><span class="sxs-lookup"><span data-stu-id="56b20-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="56b20-232">Assurez-vous que vous avez hello suivant informations avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="56b20-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="56b20-233">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="56b20-234">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="56b20-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="56b20-235">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="56b20-236">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="56b20-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="56b20-237">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="56b20-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="56b20-238">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="56b20-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="56b20-239">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="56b20-239">AS number for peering.</span></span> <span data-ttu-id="56b20-240">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="56b20-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="56b20-241">Publié préfixes : vous devez fournir une liste de tous les préfixes que vous prévoyez tooadvertise sur la session BGP de hello.</span><span class="sxs-lookup"><span data-stu-id="56b20-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="56b20-242">Seuls les préfixes d'adresses IP publiques sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="56b20-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="56b20-243">Vous pouvez envoyer une liste séparée par des virgules si vous envisagez de toosend un jeu de préfixes.</span><span class="sxs-lookup"><span data-stu-id="56b20-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="56b20-244">Ces préfixes doivent être inscrit tooyou dans un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="56b20-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="56b20-245">Client ASN : Si vous publiez des préfixes qui ne sont pas inscrit toohello d’homologation en tant que nombre, vous pouvez spécifier hello en tant que nombre toowhich qu'ils sont inscrits.</span><span class="sxs-lookup"><span data-stu-id="56b20-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="56b20-246">**Cette étape est facultative**.</span><span class="sxs-lookup"><span data-stu-id="56b20-246">**This is optional**.</span></span>
   * <span data-ttu-id="56b20-247">Nom de Registre de routage : Vous pouvez spécifier hello RIR / IRR contre le hello comme nombre et les préfixes sont inscrits.</span><span class="sxs-lookup"><span data-stu-id="56b20-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="56b20-248">Un hachage MD5, si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="56b20-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="56b20-249">**Cette étape est facultative.**</span><span class="sxs-lookup"><span data-stu-id="56b20-249">**This is optional.**</span></span>
     
    <span data-ttu-id="56b20-250">Vous pouvez exécuter hello suivant pering de Microsoft tooconfigure applet de commande pour votre circuit</span><span class="sxs-lookup"><span data-stu-id="56b20-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="56b20-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="56b20-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="56b20-252">informations d’homologation de tooview Microsoft</span><span class="sxs-lookup"><span data-stu-id="56b20-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="56b20-253">Vous pouvez obtenir les détails de configuration à l’aide de hello suivant l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="56b20-253">You can get configuration details using hello following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="56b20-254">configuration d’homologation de tooupdate Microsoft</span><span class="sxs-lookup"><span data-stu-id="56b20-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="56b20-255">Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello suivant l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="56b20-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="56b20-256">l’homologation de Microsoft toodelete</span><span class="sxs-lookup"><span data-stu-id="56b20-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="56b20-257">Vous pouvez supprimer la configuration d’homologation par hello suivant l’applet de commande en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="56b20-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="56b20-258">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56b20-258">Next steps</span></span>
<span data-ttu-id="56b20-259">Ensuite, [lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="56b20-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="56b20-260">Pour plus d'informations sur les workflows, consultez [Workflows ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="56b20-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="56b20-261">Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="56b20-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

