---
title: "Lier un réseau virtuel à un circuit ExpressRoute avec PowerShell et Azure | Microsoft Docs"
description: "Ce document explique comment lier des réseaux virtuels à des circuits ExpressRoute à l’aide du modèle de déploiement Resource Manager et de PowerShell."
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
ms.openlocfilehash: 8c2f3036f754a98090ab860f95900416690ebf83
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="5f93a-103">Connecter un réseau virtuel à un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5f93a-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f93a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="5f93a-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="5f93a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f93a-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="5f93a-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="5f93a-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="5f93a-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="5f93a-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="5f93a-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="5f93a-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="5f93a-109">Cet article vous aide à lier des réseaux virtuels à des circuits Azure ExpressRoute en utilisant le modèle de déploiement Resource Manager et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f93a-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="5f93a-110">Les réseaux virtuels peuvent appartenir au même abonnement ou faire partie d’un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f93a-110">Virtual networks can either be in the same subscription or part of another subscription.</span></span> <span data-ttu-id="5f93a-111">Cet article vous montre également comment mettre à jour une liaison de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5f93a-111">This article also shows you how to update a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="5f93a-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="5f93a-112">Before you begin</span></span>
* <span data-ttu-id="5f93a-113">Installez la dernière version des modules Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f93a-113">Install the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="5f93a-114">Pour plus d’informations, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f93a-114">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="5f93a-115">Avant de commencer la configuration, examinez les [conditions préalables](expressroute-prerequisites.md), la [configuration requise pour le routage](expressroute-routing.md) et les [flux de travail](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="5f93a-115">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="5f93a-116">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="5f93a-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="5f93a-117">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et faites-le activer par votre fournisseur de service de connectivité.</span><span class="sxs-lookup"><span data-stu-id="5f93a-117">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="5f93a-118">Vérifiez que l’homologation privée Azure est configurée pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="5f93a-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="5f93a-119">Pour obtenir des instructions de routage, consultez l'article sur la [configuration du routage](expressroute-howto-routing-arm.md) .</span><span class="sxs-lookup"><span data-stu-id="5f93a-119">See the [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="5f93a-120">Vérifiez que l’homologation privée Azure est être configurée, et que l’homologation BGP entre votre réseau et Microsoft est être opérationnelle pour pouvoir activer la connectivité de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="5f93a-120">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="5f93a-121">Vérifiez qu’un réseau virtuel et une passerelle de réseau virtuel ont été créés et entièrement approvisionnés.</span><span class="sxs-lookup"><span data-stu-id="5f93a-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="5f93a-122">Suivez les instructions pour [créer une passerelle de réseau virtuel pour ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5f93a-122">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="5f93a-123">Une passerelle de réseau virtuel pour ExpressRoute utilise le type de passerelle « ExpressRoute », pas de VPN.</span><span class="sxs-lookup"><span data-stu-id="5f93a-123">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="5f93a-124">Vous pouvez lier jusqu’à 10 réseaux virtuels à un circuit ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="5f93a-124">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="5f93a-125">Tous les réseaux virtuels doivent figurer dans la même région géopolitique lors de l’utilisation d’un circuit ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="5f93a-125">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="5f93a-126">Vous pouvez lier des réseaux virtuels à l'extérieur de la zone géopolitique du circuit ExpressRoute ou lier un plus grand nombre de réseaux virtuels à votre circuit ExpressRoute si vous avez activé le module complémentaire Premium d’ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5f93a-126">You can link a virtual networks outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="5f93a-127">Pour plus d’informations sur le module complémentaire Premium, consultez le [FAQ](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="5f93a-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="5f93a-128">Connecter un réseau virtuel du même abonnement à un circuit</span><span class="sxs-lookup"><span data-stu-id="5f93a-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="5f93a-129">Vous pouvez connecter une passerelle de réseau virtuel à un circuit ExpressRoute à l’aide de l’applet de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="5f93a-129">You can connect a virtual network gateway to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="5f93a-130">Vérifiez que la passerelle de réseau virtuel est créée et prête pour la liaison avant d’exécuter l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="5f93a-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="5f93a-131">Connecter un réseau virtuel d’un autre abonnement à un circuit</span><span class="sxs-lookup"><span data-stu-id="5f93a-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="5f93a-132">Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="5f93a-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="5f93a-133">La figure suivante montre un schéma simple sur le fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="5f93a-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="5f93a-134">Chacun des petits clouds dans le cloud principal est utilisé pour représenter les abonnements appartenant à différents services au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="5f93a-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="5f93a-135">Chacun des services au sein de l’organisation peut utiliser son propre abonnement pour déployer ses services, mais ils peuvent partager un même circuit ExpressRoute pour se connecter à votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="5f93a-135">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="5f93a-136">Un seul service (dans cet exemple, le service informatique) peut posséder le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5f93a-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="5f93a-137">D’autres abonnements au sein de l’organisation peuvent utiliser le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5f93a-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="5f93a-138">Les frais de connectivité et de bande passante pour le circuit ExpressRoute s’appliquent au propriétaire de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f93a-138">Connectivity and bandwidth charges for the ExpressRoute circuit will be applied to the subscription owner.</span></span> <span data-ttu-id="5f93a-139">Tous les réseaux virtuels partagent la même bande passante.</span><span class="sxs-lookup"><span data-stu-id="5f93a-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="5f93a-141">Administration - propriétaires de circuit et utilisateurs de circuit</span><span class="sxs-lookup"><span data-stu-id="5f93a-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="5f93a-142">Le « propriétaire du circuit » est l’utilisateur avec pouvoir autorisé de la ressource de circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5f93a-142">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="5f93a-143">Le propriétaire du circuit peut créer des autorisations utilisables par les « utilisateurs du circuit ».</span><span class="sxs-lookup"><span data-stu-id="5f93a-143">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="5f93a-144">Les utilisateurs du circuit sont les propriétaires des passerelles de réseau virtuel qui ne figurent pas dans le même abonnement que le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5f93a-144">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="5f93a-145">Les utilisateurs du circuit peuvent échanger des autorisations (une seule autorisation par réseau virtuel).</span><span class="sxs-lookup"><span data-stu-id="5f93a-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="5f93a-146">Le propriétaire du circuit a le pouvoir de modifier et de révoquer les autorisations à tout moment.</span><span class="sxs-lookup"><span data-stu-id="5f93a-146">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="5f93a-147">La révocation d’une autorisation entraîne la suppression de toutes les connexions de l’abonnement dont l’accès a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="5f93a-147">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="5f93a-148">Opérations du propriétaire du circuit</span><span class="sxs-lookup"><span data-stu-id="5f93a-148">Circuit owner operations</span></span>

<span data-ttu-id="5f93a-149">**Création d’une autorisation**</span><span class="sxs-lookup"><span data-stu-id="5f93a-149">**To create an authorization**</span></span>

<span data-ttu-id="5f93a-150">Le propriétaire du circuit crée une autorisation.</span><span class="sxs-lookup"><span data-stu-id="5f93a-150">The circuit owner creates an authorization.</span></span> <span data-ttu-id="5f93a-151">Cela entraîne la création d'une clé d'autorisation qui peut être utilisée par un utilisateur du circuit pour se connecter à ses passerelles de réseau virtuel vers un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5f93a-151">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="5f93a-152">Une autorisation n’est valide que pour une seule connexion.</span><span class="sxs-lookup"><span data-stu-id="5f93a-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="5f93a-153">L’extrait de code d’applet de commande ci-dessous montre comment créer une autorisation :</span><span class="sxs-lookup"><span data-stu-id="5f93a-153">The following cmdlet snippet shows how to create an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="5f93a-154">La réponse contient la clé d’autorisation et le statut :</span><span class="sxs-lookup"><span data-stu-id="5f93a-154">The response to this will contain the authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="5f93a-155">**Vérification des autorisations**</span><span class="sxs-lookup"><span data-stu-id="5f93a-155">**To review authorizations**</span></span>

<span data-ttu-id="5f93a-156">Le propriétaire du circuit peut vérifier toutes les autorisations émises sur un circuit donné en exécutant l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5f93a-156">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="5f93a-157">**Ajout d’autorisations**</span><span class="sxs-lookup"><span data-stu-id="5f93a-157">**To add authorizations**</span></span>

<span data-ttu-id="5f93a-158">Le propriétaire du circuit peut ajouter des autorisations à l’aide de l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5f93a-158">The circuit owner can add authorizations by using the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="5f93a-159">**Suppression d’autorisations**</span><span class="sxs-lookup"><span data-stu-id="5f93a-159">**To delete authorizations**</span></span>

<span data-ttu-id="5f93a-160">Le propriétaire du circuit peut révoquer/supprimer les autorisations accordées à l’utilisateur en exécutant l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5f93a-160">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="5f93a-161">Opérations de l’utilisateur du circuit</span><span class="sxs-lookup"><span data-stu-id="5f93a-161">Circuit user operations</span></span>

<span data-ttu-id="5f93a-162">L'utilisateur du circuit a besoin de l'ID de l'homologue et une clé d'autorisation du propriétaire du circuit.</span><span class="sxs-lookup"><span data-stu-id="5f93a-162">The circuit user needs the peer ID and an authorization key from the circuit owner.</span></span> <span data-ttu-id="5f93a-163">La clé d'autorisation est un GUID.</span><span class="sxs-lookup"><span data-stu-id="5f93a-163">The authorization key is a GUID.</span></span>

<span data-ttu-id="5f93a-164">L’ID de l’homologue peut être consulté avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5f93a-164">Peer ID can be checked from the following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="5f93a-165">**Réclamation d’une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="5f93a-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="5f93a-166">L’utilisateur du circuit peut exécuter l’applet de commande suivante pour échanger une autorisation de lien :</span><span class="sxs-lookup"><span data-stu-id="5f93a-166">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="5f93a-167">**Libération d’une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="5f93a-167">**To release a connection authorization**</span></span>

<span data-ttu-id="5f93a-168">Vous pouvez libérer une autorisation en supprimant la connexion qui lie le circuit ExpressRoute et le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5f93a-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="5f93a-169">Modifier une connexion de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="5f93a-169">Modify a virtual network connection</span></span>
<span data-ttu-id="5f93a-170">Vous pouvez mettre à jour certaines propriétés d’une connexion de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5f93a-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="5f93a-171">**Mise à jour du poids attribué à la connexion**</span><span class="sxs-lookup"><span data-stu-id="5f93a-171">**To update the connection weight**</span></span>

<span data-ttu-id="5f93a-172">Votre réseau virtuel peut être connecté à plusieurs circuits ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5f93a-172">Your virtual network can be connected to multiple ExpressRoute circuits.</span></span> <span data-ttu-id="5f93a-173">Vous pouvez recevoir le même préfixe à partir de plusieurs circuits ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5f93a-173">You may receive the same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="5f93a-174">Pour choisir la connexion pour envoyer le trafic destiné à ce préfixe, vous pouvez modifier le *RoutingWeight* d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="5f93a-174">To choose which connection to send traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="5f93a-175">Le trafic est envoyé sur la connexion avec le *RoutingWeight*.le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="5f93a-175">Traffic will be sent on the connection with the highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="5f93a-176">La plage de *RoutingWeight* est de 0 à 32000.</span><span class="sxs-lookup"><span data-stu-id="5f93a-176">The range of *RoutingWeight* is 0 to 32000.</span></span> <span data-ttu-id="5f93a-177">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="5f93a-177">The default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f93a-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5f93a-178">Next steps</span></span>
<span data-ttu-id="5f93a-179">Pour plus d'informations sur ExpressRoute, consultez le [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="5f93a-179">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
