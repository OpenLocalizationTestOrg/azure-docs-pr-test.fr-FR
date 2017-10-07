---
title: "Lier un circuit ExpressRoute de tooan réseau virtuel : PowerShell : Azure | Documents Microsoft"
description: "Ce document fournit une vue d’ensemble du mode toolink virtuel réseaux (réseaux virtuels) tooExpressRoute circuits à l’aide de PowerShell et le modèle de déploiement du Gestionnaire de ressources hello."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="f4ced-103">Se connecter à un circuit ExpressRoute de tooan réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f4ced-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4ced-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f4ced-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="f4ced-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4ced-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="f4ced-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f4ced-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="f4ced-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="f4ced-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="f4ced-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="f4ced-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="f4ced-109">Cet article vous permet de lier des circuits ExpressRoute de tooAzure des réseaux virtuels (réseaux virtuels) à l’aide de PowerShell et le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f4ced-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="f4ced-110">Réseaux virtuels peuvent être dans hello même abonnement ou une partie d’un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="f4ced-110">Virtual networks can either be in hello same subscription or part of another subscription.</span></span> <span data-ttu-id="f4ced-111">Cet article vous montre également comment lier des tooupdate un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f4ced-111">This article also shows you how tooupdate a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f4ced-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f4ced-112">Before you begin</span></span>
* <span data-ttu-id="f4ced-113">Installez la version la plus récente des modules d’Azure PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="f4ced-113">Install hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="f4ced-114">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f4ced-114">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="f4ced-115">Hello de révision [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="f4ced-115">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="f4ced-116">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="f4ced-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="f4ced-117">Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et avoir des circuits hello activé par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="f4ced-117">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="f4ced-118">Vérifiez que l’homologation privée Azure est configurée pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="f4ced-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="f4ced-119">Consultez hello [configurer le routage](expressroute-howto-routing-arm.md) article pour obtenir des instructions de routage.</span><span class="sxs-lookup"><span data-stu-id="f4ced-119">See hello [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="f4ced-120">Assurez-vous que l’homologation privée Azure est configuré et est l’homologation BGP hello entre votre réseau et de Microsoft afin que vous pouvez activer la connectivité de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="f4ced-120">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="f4ced-121">Vérifiez qu’un réseau virtuel et une passerelle de réseau virtuel ont été créés et entièrement approvisionnés.</span><span class="sxs-lookup"><span data-stu-id="f4ced-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="f4ced-122">Suivez les instructions de hello trop[créer une passerelle de réseau virtuel pour ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f4ced-122">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="f4ced-123">Une passerelle de réseau virtuel pour ExpressRoute utilise hello « ExpressRoute », le type de passerelle VPN pas.</span><span class="sxs-lookup"><span data-stu-id="f4ced-123">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="f4ced-124">Vous pouvez lier de circuit de ExpressRoute standard too10 réseaux virtuels tooa.</span><span class="sxs-lookup"><span data-stu-id="f4ced-124">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="f4ced-125">Tous les réseaux virtuels doivent être Bonjour même région géopolitique lors de l’utilisation d’un circuit ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="f4ced-125">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="f4ced-126">Vous pouvez lier un réseau virtuel en dehors de la région de hello géopolitique de hello circuit ExpressRoute ou vous connecter à un plus grand nombre de réseaux virtuels tooyour circuit ExpressRoute si vous avez activé le module complémentaire de hello ExpressRoute premium.</span><span class="sxs-lookup"><span data-stu-id="f4ced-126">You can link a virtual networks outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="f4ced-127">Vérifiez hello [FAQ](expressroute-faqs.md) pour plus d’informations sur le module complémentaire de hello premium.</span><span class="sxs-lookup"><span data-stu-id="f4ced-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="f4ced-128">Connecter un réseau virtuel Bonjour même circuit de tooa d’abonnement</span><span class="sxs-lookup"><span data-stu-id="f4ced-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="f4ced-129">Vous pouvez vous connecter à un tooan de passerelle de réseau virtuel circuit ExpressRoute à l’aide de hello suivant l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f4ced-129">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="f4ced-130">Assurez-vous que cette passerelle de réseau virtuel hello est créée et est prête pour la liaison avant d’exécuter les applets de commande hello :</span><span class="sxs-lookup"><span data-stu-id="f4ced-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="f4ced-131">Connecter un réseau virtuel dans un circuit de tooa autre abonnement</span><span class="sxs-lookup"><span data-stu-id="f4ced-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="f4ced-132">Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="f4ced-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="f4ced-133">Hello figure suivante montre une simple principe de fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="f4ced-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="f4ced-134">Chaque hello petits clouds dans cloud volumineux de hello est utilisé toorepresent abonnements appartenant aux départements toodifferent au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="f4ced-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="f4ced-135">Chacun des services hello au sein de l’organisation de hello permettre utiliser leur propre abonnement pour le déploiement de leurs services, mais ils peuvent partager un réseau local ExpressRoute circuit tooconnect tooyour précédent.</span><span class="sxs-lookup"><span data-stu-id="f4ced-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="f4ced-136">Un seul département (dans cet exemple : informatique) peut posséder de circuit ExpressRoute de hello.</span><span class="sxs-lookup"><span data-stu-id="f4ced-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="f4ced-137">Autres abonnements au sein de l’organisation de hello peuvent utiliser le circuit ExpressRoute de hello.</span><span class="sxs-lookup"><span data-stu-id="f4ced-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="f4ced-138">Frais de connectivité et de bande passante pour le circuit ExpressRoute de hello sera appliqué toohello propriétaire de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="f4ced-138">Connectivity and bandwidth charges for hello ExpressRoute circuit will be applied toohello subscription owner.</span></span> <span data-ttu-id="f4ced-139">Tous les réseaux virtuels partagent hello même bande passante.</span><span class="sxs-lookup"><span data-stu-id="f4ced-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="f4ced-141">Administration - propriétaires de circuit et utilisateurs de circuit</span><span class="sxs-lookup"><span data-stu-id="f4ced-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="f4ced-142">Hello propriétaire du circuit est un utilisateur autorisé de la puissance de hello ressource de circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f4ced-142">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="f4ced-143">propriétaire du circuit Hello peut créer des autorisations qui peuvent être utilisées par les utilisateurs de circuit.</span><span class="sxs-lookup"><span data-stu-id="f4ced-143">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="f4ced-144">Les utilisateurs de circuit sont les propriétaires du réseau virtuel qui ne sont pas dans les passerelles hello même abonnement que hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f4ced-144">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="f4ced-145">Les utilisateurs du circuit peuvent échanger des autorisations (une seule autorisation par réseau virtuel).</span><span class="sxs-lookup"><span data-stu-id="f4ced-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="f4ced-146">propriétaire du circuit Hello possède les autorisations hello power toomodify et révoquer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="f4ced-146">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="f4ced-147">Révocation de des résultats d’autorisation dans toutes les connexions de la liaison en cours de suppression de l’abonnement hello dont l’accès a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="f4ced-147">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="f4ced-148">Opérations du propriétaire du circuit</span><span class="sxs-lookup"><span data-stu-id="f4ced-148">Circuit owner operations</span></span>

<span data-ttu-id="f4ced-149">**toocreate une autorisation**</span><span class="sxs-lookup"><span data-stu-id="f4ced-149">**toocreate an authorization**</span></span>

<span data-ttu-id="f4ced-150">propriétaire du circuit Hello crée une autorisation.</span><span class="sxs-lookup"><span data-stu-id="f4ced-150">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="f4ced-151">Cela entraîne la création de hello d’une clé d’autorisation qui peut être utilisé par un tooconnect utilisateur de circuit leur toohello de passerelles de réseau virtuel circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f4ced-151">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="f4ced-152">Une autorisation n’est valide que pour une seule connexion.</span><span class="sxs-lookup"><span data-stu-id="f4ced-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="f4ced-153">Hello suivant applet de commande extrait de code montre comment une autorisation de toocreate :</span><span class="sxs-lookup"><span data-stu-id="f4ced-153">hello following cmdlet snippet shows how toocreate an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="f4ced-154">Hello réponse toothis contiendra l’état et la clé d’autorisation de hello :</span><span class="sxs-lookup"><span data-stu-id="f4ced-154">hello response toothis will contain hello authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="f4ced-155">**autorisations tooreview**</span><span class="sxs-lookup"><span data-stu-id="f4ced-155">**tooreview authorizations**</span></span>

<span data-ttu-id="f4ced-156">propriétaire du circuit Hello peut consulter toutes les autorisations qui sont émises sur un circuit en particulier en exécutant hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="f4ced-156">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="f4ced-157">**autorisations tooadd**</span><span class="sxs-lookup"><span data-stu-id="f4ced-157">**tooadd authorizations**</span></span>

<span data-ttu-id="f4ced-158">propriétaire du circuit Hello peut ajouter des autorisations à l’aide de hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="f4ced-158">hello circuit owner can add authorizations by using hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="f4ced-159">**autorisations toodelete**</span><span class="sxs-lookup"><span data-stu-id="f4ced-159">**toodelete authorizations**</span></span>

<span data-ttu-id="f4ced-160">propriétaire du circuit Hello permettre révoquer/supprimer un autorisations toohello utilisateur en exécutant hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="f4ced-160">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="f4ced-161">Opérations de l’utilisateur du circuit</span><span class="sxs-lookup"><span data-stu-id="f4ced-161">Circuit user operations</span></span>

<span data-ttu-id="f4ced-162">utilisateur du circuit Hello doit hello homologue ID et une clé d’autorisation du propriétaire du circuit hello.</span><span class="sxs-lookup"><span data-stu-id="f4ced-162">hello circuit user needs hello peer ID and an authorization key from hello circuit owner.</span></span> <span data-ttu-id="f4ced-163">clé d’autorisation de Hello est un GUID.</span><span class="sxs-lookup"><span data-stu-id="f4ced-163">hello authorization key is a GUID.</span></span>

<span data-ttu-id="f4ced-164">ID de l’homologue peut être vérifiée à partir de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f4ced-164">Peer ID can be checked from hello following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="f4ced-165">**tooredeem une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="f4ced-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="f4ced-166">utilisateur du circuit Hello peut exécuter hello suivant l’applet de commande tooredeem une autorisation de lien :</span><span class="sxs-lookup"><span data-stu-id="f4ced-166">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="f4ced-167">**toorelease une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="f4ced-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="f4ced-168">Vous pouvez libérer une autorisation en supprimant la connexion hello qui établit un lien réseau virtuel du toohello circuit ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="f4ced-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="f4ced-169">Modifier une connexion de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f4ced-169">Modify a virtual network connection</span></span>
<span data-ttu-id="f4ced-170">Vous pouvez mettre à jour certaines propriétés d’une connexion de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f4ced-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="f4ced-171">**poids de connexion hello tooupdate**</span><span class="sxs-lookup"><span data-stu-id="f4ced-171">**tooupdate hello connection weight**</span></span>

<span data-ttu-id="f4ced-172">Votre réseau virtuel peut être connecté toomultiple des circuits ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f4ced-172">Your virtual network can be connected toomultiple ExpressRoute circuits.</span></span> <span data-ttu-id="f4ced-173">Vous pouvez recevoir le même préfixe de hello à partir de plusieurs circuits ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f4ced-173">You may receive hello same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="f4ced-174">toochoose le trafic toosend connexion destinés à ce préfixe, vous pouvez modifier *RoutingWeight* d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="f4ced-174">toochoose which connection toosend traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="f4ced-175">Le trafic sera envoyé sur connexion hello avec hello plus élevé *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="f4ced-175">Traffic will be sent on hello connection with hello highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="f4ced-176">Hello plage de *RoutingWeight* est too32000 0.</span><span class="sxs-lookup"><span data-stu-id="f4ced-176">hello range of *RoutingWeight* is 0 too32000.</span></span> <span data-ttu-id="f4ced-177">Hello par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="f4ced-177">hello default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4ced-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f4ced-178">Next steps</span></span>
<span data-ttu-id="f4ced-179">Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="f4ced-179">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
