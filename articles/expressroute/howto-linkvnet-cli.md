---
title: "Lier un circuit ExpressRoute de tooan réseau virtuel : CLI : Azure | Documents Microsoft"
description: "Ce document fournit une vue d’ensemble de la façon dont toolink virtuel réseaux des circuits tooExpressRoute (réseaux virtuels) en utilisant le modèle de déploiement du Gestionnaire de ressources hello et CLI."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a><span data-ttu-id="8b0ff-103">Se connecter à un circuit ExpressRoute de tooan de réseau virtuel à l’aide de CLI</span><span class="sxs-lookup"><span data-stu-id="8b0ff-103">Connect a virtual network tooan ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="8b0ff-104">Cet article vous permet de lier des circuits ExpressRoute de réseaux virtuels (réseaux virtuels) tooAzure à l’aide de CLI.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-104">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="8b0ff-105">toolink à l’aide de CLI d’Azure, les réseaux virtuels hello doivent être créés à l’aide du modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-105">toolink using Azure CLI, hello virtual networks must be created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="8b0ff-106">Ils peuvent être dans hello même abonnement, ou une partie d’un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-106">They can either be in hello same subscription, or part of another subscription.</span></span> <span data-ttu-id="8b0ff-107">Si vous souhaitez toouse une autre méthode de tooconnect votre circuit ExpressRoute de tooan réseau virtuel, vous pouvez sélectionner un article à partir de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="8b0ff-107">If you want toouse a different method tooconnect your VNet tooan ExpressRoute circuit, you can select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b0ff-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8b0ff-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="8b0ff-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b0ff-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="8b0ff-110">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="8b0ff-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="8b0ff-111">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="8b0ff-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="8b0ff-112">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="8b0ff-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="8b0ff-113">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="8b0ff-113">Configuration prerequisites</span></span>

* <span data-ttu-id="8b0ff-114">Vous devez hello dernière version de hello interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="8b0ff-114">You need hello latest version of hello command-line interface (CLI).</span></span> <span data-ttu-id="8b0ff-115">Pour plus d’informations, consultez [Installer Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8b0ff-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="8b0ff-116">Vous devez tooreview hello [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="8b0ff-117">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="8b0ff-118">Suivez les instructions de hello trop[créer un circuit ExpressRoute](howto-circuit-cli.md) et avoir des circuits hello activé par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-118">Follow hello instructions too[create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="8b0ff-119">Vérifiez que l’homologation privée Azure est configurée pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="8b0ff-120">Consultez hello [configurer le routage](howto-routing-cli.md) article pour obtenir des instructions de routage.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-120">See hello [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="8b0ff-121">Assurez-vous que l’homologation privée Azure est configurée.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="8b0ff-122">l’homologation BGP Hello entre votre réseau et de Microsoft doit être des afin que vous pouvez activer la connectivité de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-122">hello BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="8b0ff-123">Vérifiez qu’un réseau virtuel et une passerelle de réseau virtuel ont été créés et entièrement approvisionnés.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="8b0ff-124">Suivez les instructions de hello trop[configurer une passerelle de réseau virtuel pour ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="8b0ff-124">Follow hello instructions too[Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="8b0ff-125">Être toouse vraiment `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-125">Be sure toouse `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="8b0ff-126">Vous pouvez lier de circuit de ExpressRoute standard too10 réseaux virtuels tooa.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-126">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="8b0ff-127">Tous les réseaux virtuels doivent être Bonjour même région géopolitique lors de l’utilisation d’un circuit ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-127">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="8b0ff-128">Si vous activez le module complémentaire de hello ExpressRoute premium, vous pouvez lier un réseau virtuel en dehors de la région de hello géopolitique de hello circuit ExpressRoute, ou vous connecter à un plus grand nombre de réseaux virtuels tooyour circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-128">If you enable hello ExpressRoute premium add-on, you can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="8b0ff-129">Pour plus d’informations sur le module complémentaire de hello premium, consultez hello [FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="8b0ff-129">For more information about hello premium add-on, see hello [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="8b0ff-130">Connecter un réseau virtuel Bonjour même circuit de tooa d’abonnement</span><span class="sxs-lookup"><span data-stu-id="8b0ff-130">Connect a virtual network in hello same subscription tooa circuit</span></span>

<span data-ttu-id="8b0ff-131">Vous pouvez vous connecter à un circuit ExpressRoute de réseau virtuel passerelle tooan à l’aide de hello exemple.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-131">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello example.</span></span> <span data-ttu-id="8b0ff-132">Assurez-vous que cette passerelle de réseau virtuel hello est créée et est prête pour la liaison avant d’exécuter les commandes hello.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-132">Make sure that hello virtual network gateway is created and is ready for linking before you run hello command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="8b0ff-133">Connecter un réseau virtuel dans un circuit de tooa autre abonnement</span><span class="sxs-lookup"><span data-stu-id="8b0ff-133">Connect a virtual network in a different subscription tooa circuit</span></span>

<span data-ttu-id="8b0ff-134">Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="8b0ff-135">la figure ci-dessous Hello schématique simple de fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-135">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="8b0ff-136">Chaque hello petits clouds dans cloud volumineux de hello est utilisé toorepresent abonnements appartenant aux départements toodifferent au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-136">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="8b0ff-137">Chacun des services hello au sein de l’organisation de hello permettre utiliser leur propre abonnement pour le déploiement de leurs services, mais ils peuvent partager un réseau local ExpressRoute circuit tooconnect tooyour précédent.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-137">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="8b0ff-138">Un seul département (dans cet exemple : informatique) peut posséder de circuit ExpressRoute de hello.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-138">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="8b0ff-139">Autres abonnements au sein de l’organisation de hello peuvent utiliser le circuit ExpressRoute de hello.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-139">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="8b0ff-140">Frais de connectivité et de bande passante pour le circuit de hello dédié sera appliqué toohello propriétaire du Circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-140">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="8b0ff-141">Tous les réseaux virtuels partagent hello même bande passante.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-141">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="8b0ff-143">Administration : propriétaires de circuit et utilisateurs du circuit</span><span class="sxs-lookup"><span data-stu-id="8b0ff-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="8b0ff-144">Hello propriétaire du Circuit est un utilisateur autorisé de la puissance de hello ressource de circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-144">hello 'Circuit Owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="8b0ff-145">Hello propriétaire du Circuit peut créer des autorisations qui peuvent être utilisées par les utilisateurs de Circuit.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-145">hello Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="8b0ff-146">Les utilisateurs de circuit sont les propriétaires du réseau virtuel qui ne sont pas dans les passerelles hello même abonnement que hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-146">Circuit Users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="8b0ff-147">Les utilisateurs du circuit peuvent utiliser des autorisations (une seule autorisation par réseau virtuel).</span><span class="sxs-lookup"><span data-stu-id="8b0ff-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="8b0ff-148">Hello propriétaire du Circuit a les autorisations hello power toomodify et révoquer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-148">hello Circuit Owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="8b0ff-149">Lorsqu’une autorisation est révoquée, toutes les connexions de lien sont supprimées de l’abonnement hello dont l’accès a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-149">When an authorization is revoked, all link connections are deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="8b0ff-150">Opérations du propriétaire du circuit</span><span class="sxs-lookup"><span data-stu-id="8b0ff-150">Circuit Owner operations</span></span>

<span data-ttu-id="8b0ff-151">**toocreate une autorisation**</span><span class="sxs-lookup"><span data-stu-id="8b0ff-151">**toocreate an authorization**</span></span>

<span data-ttu-id="8b0ff-152">Hello propriétaire du Circuit crée une autorisation, ce qui crée une clé d’autorisation qui peut être utilisé par un utilisateur du Circuit de tooconnect leur toohello de passerelles de réseau virtuel circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-152">hello Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="8b0ff-153">Une autorisation n’est valide que pour une seule connexion.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="8b0ff-154">Hello suivant montre l’exemple de comment toocreate une autorisation :</span><span class="sxs-lookup"><span data-stu-id="8b0ff-154">hello following example shows how toocreate an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="8b0ff-155">réponse de Hello contient l’état et la clé d’autorisation de hello :</span><span class="sxs-lookup"><span data-stu-id="8b0ff-155">hello response contains hello authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="8b0ff-156">**autorisations tooreview**</span><span class="sxs-lookup"><span data-stu-id="8b0ff-156">**tooreview authorizations**</span></span>

<span data-ttu-id="8b0ff-157">Hello propriétaire du Circuit peut consulter toutes les autorisations qui sont émises sur un circuit en particulier en exécutant hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8b0ff-157">hello Circuit Owner can review all authorizations that are issued on a particular circuit by running hello following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="8b0ff-158">**autorisations tooadd**</span><span class="sxs-lookup"><span data-stu-id="8b0ff-158">**tooadd authorizations**</span></span>

<span data-ttu-id="8b0ff-159">Hello propriétaire du Circuit peut ajouter des autorisations à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8b0ff-159">hello Circuit Owner can add authorizations by using hello following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="8b0ff-160">**autorisations toodelete**</span><span class="sxs-lookup"><span data-stu-id="8b0ff-160">**toodelete authorizations**</span></span>

<span data-ttu-id="8b0ff-161">Hello propriétaire du Circuit peut révoquer/supprimer un autorisations toohello utilisateur en exécutant hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8b0ff-161">hello Circuit Owner can revoke/delete authorizations toohello user by running hello following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="8b0ff-162">Opérations de l’utilisateur du circuit</span><span class="sxs-lookup"><span data-stu-id="8b0ff-162">Circuit User operations</span></span>

<span data-ttu-id="8b0ff-163">Hello Circuit utilisateur a besoin d’ID de l’homologue hello et une clé d’autorisation à partir de hello propriétaire du Circuit.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-163">hello Circuit User needs hello peer ID and an authorization key from hello Circuit Owner.</span></span> <span data-ttu-id="8b0ff-164">clé d’autorisation de Hello est un GUID.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-164">hello authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="8b0ff-165">**tooredeem une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="8b0ff-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="8b0ff-166">Hello utilisateur du Circuit peut exécuter hello suivant exemple tooredeem une autorisation de lien :</span><span class="sxs-lookup"><span data-stu-id="8b0ff-166">hello Circuit User can run hello following example tooredeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="8b0ff-167">**toorelease une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="8b0ff-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="8b0ff-168">Vous pouvez libérer une autorisation en supprimant la connexion hello qui établit un lien réseau virtuel du toohello circuit ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="8b0ff-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b0ff-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8b0ff-169">Next steps</span></span>

<span data-ttu-id="8b0ff-170">Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="8b0ff-170">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
