---
title: "Comment tooconfigure routage (homologation) pour un circuit ExpressRoute : le Gestionnaire de ressources : PowerShell : Azure | Documents Microsoft"
description: "Cet article vous guide tout au long des étapes hello pour la création et l’approvisionnement hello privés, publics et homologation Microsoft d’un circuit ExpressRoute. Cet article vous explique également comment toocheck état de hello, mettre à jour ou supprimer des homologations pour votre circuit."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="94446-104">Créer et modifier l’homologation d’un circuit ExpressRoute à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="94446-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="94446-105">Cet article vous aide à créer et gérer la configuration de routage pour un circuit ExpressRoute dans le modèle de déploiement hello Gestionnaire de ressources à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94446-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="94446-106">Vous pouvez également vérifier l’état de hello, update ou delete et annuler le déploiement homologations pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="94446-107">Si vous souhaitez toouse une autre méthode de toowork avec votre circuit, sélectionnez un article à partir de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="94446-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="94446-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="94446-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="94446-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94446-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="94446-110">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="94446-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="94446-111">Vidéo - Homologation privée</span><span class="sxs-lookup"><span data-stu-id="94446-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="94446-112">Vidéo - Homologation publique</span><span class="sxs-lookup"><span data-stu-id="94446-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="94446-113">Vidéo - Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="94446-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="94446-114">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="94446-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="94446-115">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="94446-115">Configuration prerequisites</span></span>

* <span data-ttu-id="94446-116">Vous devez hello dernière version de hello applets de commande PowerShell de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="94446-116">You will need hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="94446-117">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="94446-117">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="94446-118">Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md) page hello [exigences routage](expressroute-routing.md) page et hello [workflows](expressroute-workflows.md) page avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="94446-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="94446-119">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="94446-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="94446-120">Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="94446-120">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="94446-121">Hello circuit ExpressRoute doit être dans un état configuré et activé pour vous toobe toorun en mesure des applets de commande hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="94446-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in this article.</span></span>

<span data-ttu-id="94446-122">Ces instructions s’appliquent uniquement à toocircuits créé avec les fournisseurs de services offrant des services de connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="94446-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="94446-123">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="94446-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94446-124">Nous n’effectuent pas homologations configurées par les fournisseurs de services via le portail de gestion des services hello.</span><span class="sxs-lookup"><span data-stu-id="94446-124">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="94446-125">Nous travaillons sur la prochaine activation de cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="94446-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="94446-126">Contactez votre fournisseur de services avant de configurer des homologations BGP.</span><span class="sxs-lookup"><span data-stu-id="94446-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="94446-127">Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="94446-128">Vous pouvez configurer les homologations dans l’ordre de votre choix.</span><span class="sxs-lookup"><span data-stu-id="94446-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="94446-129">Toutefois, il se peut que vous devez vous assurer que vous terminez configuration hello de chacun d’eux à la fois d’homologation.</span><span class="sxs-lookup"><span data-stu-id="94446-129">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="94446-130">Homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="94446-130">Azure private peering</span></span>

<span data-ttu-id="94446-131">Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello Azure configuration d’homologation privée pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-131">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="94446-132">toocreate l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="94446-132">toocreate Azure private peering</span></span>

1. <span data-ttu-id="94446-133">Importez le module PowerShell de hello pour ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-133">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="94446-134">Vous devez installer hello dernière PowerShell installer à partir de [PowerShell Gallery](http://www.powershellgallery.com/) et importer des modules du Gestionnaire de ressources Azure hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-134">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="94446-135">Vous devez toorun PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="94446-135">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="94446-136">Importer tous les modules de AzureRM.* hello dans hello connu de plage de version sémantique.</span><span class="sxs-lookup"><span data-stu-id="94446-136">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="94446-137">Vous pouvez également importer un module sélectionnez hello connu de plage de version sémantique.</span><span class="sxs-lookup"><span data-stu-id="94446-137">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="94446-138">Tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="94446-138">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="94446-139">Sélectionnez l’abonnement hello circuit ExpressRoute de toocreate.</span><span class="sxs-lookup"><span data-stu-id="94446-139">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="94446-140">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="94446-141">Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-arm.md) et configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="94446-141">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="94446-142">Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous.</span><span class="sxs-lookup"><span data-stu-id="94446-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="94446-143">Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="94446-143">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="94446-144">Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.</span><span class="sxs-lookup"><span data-stu-id="94446-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="94446-145">Vérifiez hello ExpressRoute circuit toomake qu’il est configuré et activé également.</span><span class="sxs-lookup"><span data-stu-id="94446-145">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="94446-146">Utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-146">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="94446-147">réponse de Hello est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-147">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="94446-148">Configurer une homologation privée Azure pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-148">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="94446-149">Assurez-vous que vous disposez des éléments suivants avant de passer aux étapes suivantes de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="94446-149">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="94446-150">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-150">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="94446-151">sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="94446-151">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="94446-152">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-152">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="94446-153">sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="94446-153">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="94446-154">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="94446-154">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="94446-155">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="94446-155">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="94446-156">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="94446-156">AS number for peering.</span></span> <span data-ttu-id="94446-157">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="94446-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="94446-158">Vous pouvez utiliser un numéro AS privé pour cette homologation.</span><span class="sxs-lookup"><span data-stu-id="94446-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="94446-159">Veillez à ne pas utiliser le numéro 65515.</span><span class="sxs-lookup"><span data-stu-id="94446-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="94446-160">**Facultatif :** un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="94446-160">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="94446-161">Utilisez hello suivant exemple tooconfigure Azure privé d’homologation pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="94446-161">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="94446-162">Si vous choisissez toouse un hachage MD5, utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-162">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="94446-163">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="94446-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="94446-164">tooview Azure privé d’homologation détails</span><span class="sxs-lookup"><span data-stu-id="94446-164">tooview Azure private peering details</span></span>

<span data-ttu-id="94446-165">Vous pouvez obtenir les détails de configuration à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-165">You can get configuration details by using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="94446-166">tooupdate configuration d’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="94446-166">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="94446-167">Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="94446-167">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="94446-168">Dans cet exemple, hello ID de VLAN de circuit de hello est mise à jour à partir de 100 too500.</span><span class="sxs-lookup"><span data-stu-id="94446-168">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="94446-169">toodelete l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="94446-169">toodelete Azure private peering</span></span>

<span data-ttu-id="94446-170">Vous pouvez supprimer votre configuration d’homologation en exécutant hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-170">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="94446-171">Vous devez vous assurer que tous les réseaux virtuels sont dissocier hello circuit ExpressRoute avant d’exécuter cet exemple.</span><span class="sxs-lookup"><span data-stu-id="94446-171">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="94446-172">Homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="94446-172">Azure public peering</span></span>

<span data-ttu-id="94446-173">Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello configuration d’homologation publique Azure pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-173">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="94446-174">toocreate l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="94446-174">toocreate Azure public peering</span></span>

1. <span data-ttu-id="94446-175">Importez le module PowerShell de hello pour ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-175">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="94446-176">Vous devez installer hello dernière PowerShell installer à partir de [PowerShell Gallery](http://www.powershellgallery.com/) et importer des modules du Gestionnaire de ressources Azure hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-176">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="94446-177">Vous devez toorun PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="94446-177">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="94446-178">Importer tous les modules de AzureRM.* hello dans hello connu de plage de version sémantique.</span><span class="sxs-lookup"><span data-stu-id="94446-178">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="94446-179">Vous pouvez également importer un module sélectionnez hello connu de plage de version sémantique.</span><span class="sxs-lookup"><span data-stu-id="94446-179">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="94446-180">Tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="94446-180">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="94446-181">Sélectionnez l’abonnement hello circuit ExpressRoute de toocreate.</span><span class="sxs-lookup"><span data-stu-id="94446-181">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="94446-182">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="94446-183">Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-arm.md) et configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="94446-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="94446-184">Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous.</span><span class="sxs-lookup"><span data-stu-id="94446-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="94446-185">Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="94446-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="94446-186">Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.</span><span class="sxs-lookup"><span data-stu-id="94446-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="94446-187">Vérifiez tooensure de circuit ExpressRoute hello il est configuré et activé également.</span><span class="sxs-lookup"><span data-stu-id="94446-187">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="94446-188">Utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-188">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="94446-189">réponse de Hello est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-189">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="94446-190">Configurer l’homologation publique Azure pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-190">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="94446-191">Assurez-vous que vous disposez des informations suivantes avant de continuer davantage de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-191">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="94446-192">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-192">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="94446-193">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="94446-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="94446-194">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-194">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="94446-195">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="94446-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="94446-196">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="94446-196">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="94446-197">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="94446-197">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="94446-198">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="94446-198">AS number for peering.</span></span> <span data-ttu-id="94446-199">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="94446-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="94446-200">**Facultatif :** un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="94446-200">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="94446-201">Exécutez hello suivant exemple tooconfigure Azure public d’homologation pour votre circuit</span><span class="sxs-lookup"><span data-stu-id="94446-201">Run hello following example tooconfigure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="94446-202">Si vous choisissez toouse un hachage MD5, utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-202">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="94446-203">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="94446-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="94446-204">tooview Azure public d’homologation détails</span><span class="sxs-lookup"><span data-stu-id="94446-204">tooview Azure public peering details</span></span>

<span data-ttu-id="94446-205">Vous pouvez obtenir les détails de configuration à l’aide de hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="94446-205">You can get configuration details using hello following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="94446-206">tooupdate configuration d’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="94446-206">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="94446-207">Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="94446-207">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="94446-208">Dans cet exemple, hello ID de VLAN de circuit de hello est mise à jour à partir de too600 200.</span><span class="sxs-lookup"><span data-stu-id="94446-208">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="94446-209">toodelete l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="94446-209">toodelete Azure public peering</span></span>

<span data-ttu-id="94446-210">Vous pouvez supprimer votre configuration d’homologation en exécutant hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-210">You can remove your peering configuration by running hello following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="94446-211">Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="94446-211">Microsoft peering</span></span>

<span data-ttu-id="94446-212">Cette section vous permet de créer, obtenir, mettre à jour et supprimer la configuration d’homologation Microsoft hello pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-212">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94446-213">Homologation Microsoft des circuits ExpressRoute qui ont été configurés préalable tooAugust 1, 2017 aura tous les préfixes de service publiés par le biais d’homologation de Microsoft hello, même si les filtres de routage ne sont pas définis.</span><span class="sxs-lookup"><span data-stu-id="94446-213">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="94446-214">Homologation Microsoft des circuits ExpressRoute qui sont configurés sur ou après le 1er août 2017 n’aura pas de préfixes publiés jusqu'à ce qu’un filtre de routage est attaché toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="94446-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="94446-215">Pour plus d’informations, consultez [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurer un filtre d’itinéraire pour l’homologation Microsoft).</span><span class="sxs-lookup"><span data-stu-id="94446-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="94446-216">l’homologation de Microsoft toocreate</span><span class="sxs-lookup"><span data-stu-id="94446-216">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="94446-217">Importez le module PowerShell de hello pour ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-217">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="94446-218">Vous devez installer hello dernière PowerShell installer à partir de [PowerShell Gallery](http://www.powershellgallery.com/) et importer des modules du Gestionnaire de ressources Azure hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-218">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="94446-219">Vous devez toorun PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="94446-219">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="94446-220">Importer tous les modules de AzureRM.* hello dans hello connu de plage de version sémantique.</span><span class="sxs-lookup"><span data-stu-id="94446-220">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="94446-221">Vous pouvez également importer un module sélectionnez hello connu de plage de version sémantique.</span><span class="sxs-lookup"><span data-stu-id="94446-221">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="94446-222">Tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="94446-222">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="94446-223">Sélectionnez l’abonnement hello circuit ExpressRoute de toocreate.</span><span class="sxs-lookup"><span data-stu-id="94446-223">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="94446-224">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="94446-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="94446-225">Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-arm.md) et configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="94446-225">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="94446-226">Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous.</span><span class="sxs-lookup"><span data-stu-id="94446-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="94446-227">Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="94446-227">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="94446-228">Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.</span><span class="sxs-lookup"><span data-stu-id="94446-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="94446-229">Vérifiez hello ExpressRoute circuit toomake qu’il est configuré et activé également.</span><span class="sxs-lookup"><span data-stu-id="94446-229">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="94446-230">Utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-230">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="94446-231">réponse de Hello est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-231">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="94446-232">Configurez Microsoft d’homologation pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-232">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="94446-233">Assurez-vous que vous avez hello suivant informations avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="94446-233">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="94446-234">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-234">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="94446-235">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="94446-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="94446-236">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-236">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="94446-237">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="94446-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="94446-238">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="94446-238">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="94446-239">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="94446-239">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="94446-240">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="94446-240">AS number for peering.</span></span> <span data-ttu-id="94446-241">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="94446-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="94446-242">Publié préfixes : vous devez fournir une liste de tous les préfixes que vous prévoyez tooadvertise sur la session BGP de hello.</span><span class="sxs-lookup"><span data-stu-id="94446-242">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="94446-243">Seuls les préfixes d'adresses IP publiques sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="94446-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="94446-244">Si vous envisagez un jeu de préfixes de toosend, vous pouvez envoyer une liste séparée par des virgules.</span><span class="sxs-lookup"><span data-stu-id="94446-244">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="94446-245">Ces préfixes doivent être inscrit tooyou dans un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="94446-245">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="94446-246">**Facultatif :** client ASN : Si vous ne les préfixes de publicité qui ne sont pas inscrit toohello d’homologation en tant que nombre, vous pouvez spécifier hello en tant que nombre toowhich ils sont inscrits.</span><span class="sxs-lookup"><span data-stu-id="94446-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="94446-247">Nom de Registre de routage : Vous pouvez spécifier hello RIR / IRR contre le hello comme nombre et les préfixes sont inscrits.</span><span class="sxs-lookup"><span data-stu-id="94446-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="94446-248">**Facultatif :** un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="94446-248">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="94446-249">Utilisez hello suivant exemple tooconfigure Microsoft homologation pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="94446-249">Use hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="94446-250">informations d’homologation de tooget Microsoft</span><span class="sxs-lookup"><span data-stu-id="94446-250">tooget Microsoft peering details</span></span>

<span data-ttu-id="94446-251">Vous pouvez obtenir les détails de configuration à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-251">You can get configuration details using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="94446-252">configuration d’homologation de tooupdate Microsoft</span><span class="sxs-lookup"><span data-stu-id="94446-252">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="94446-253">Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="94446-253">You can update any part of hello configuration using hello following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="94446-254">l’homologation de Microsoft toodelete</span><span class="sxs-lookup"><span data-stu-id="94446-254">toodelete Microsoft peering</span></span>

<span data-ttu-id="94446-255">Vous pouvez supprimer votre configuration d’homologation par hello suivant l’applet de commande en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="94446-255">You can remove your peering configuration by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="94446-256">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94446-256">Next steps</span></span>

<span data-ttu-id="94446-257">Étape suivante, [lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="94446-257">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="94446-258">Pour plus d'informations sur les workflows ExpressRoute, consultez [Workflows ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="94446-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="94446-259">Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="94446-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="94446-260">Pour plus d’informations sur l’utilisation des réseaux virtuels, consultez la page [Présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94446-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
