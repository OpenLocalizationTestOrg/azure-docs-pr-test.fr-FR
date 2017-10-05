---
title: "Lier un réseau virtuel à un circuit ExpressRoute avec l’interface Azure CLI | Microsoft Docs"
description: "Ce document explique comment lier des réseaux virtuels à des circuits ExpressRoute à l’aide du modèle de déploiement Resource Manager et de l’interface CLI."
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
ms.openlocfilehash: 0ea696e796ec3a943bc028f56da417978b728b82
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-cli"></a><span data-ttu-id="9b656-103">Connecter un réseau virtuel à un circuit ExpressRoute à l’aide de l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="9b656-103">Connect a virtual network to an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="9b656-104">Cet article est conçu pour vous aider à lier des réseaux virtuels à des circuits ExpressRoute de Azure à l’aide de l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="9b656-104">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="9b656-105">Pour pouvoir être liés avec l’interface Azure CLI, les réseaux virtuels doivent être créés à l’aide du modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b656-105">To link using Azure CLI, the virtual networks must be created using the Resource Manager deployment model.</span></span> <span data-ttu-id="9b656-106">Ils peuvent appartenir au même abonnement ou faire partie d’un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9b656-106">They can either be in the same subscription, or part of another subscription.</span></span> <span data-ttu-id="9b656-107">Si vous souhaitez utiliser une autre méthode pour connecter votre réseau virtuel à un circuit ExpressRoute, vous pouvez sélectionner un article dans la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="9b656-107">If you want to use a different method to connect your VNet to an ExpressRoute circuit, you can select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b656-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="9b656-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="9b656-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b656-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="9b656-110">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="9b656-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="9b656-111">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="9b656-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="9b656-112">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="9b656-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="9b656-113">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="9b656-113">Configuration prerequisites</span></span>

* <span data-ttu-id="9b656-114">Vous avez besoin de la dernière version de l’interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="9b656-114">You need the latest version of the command-line interface (CLI).</span></span> <span data-ttu-id="9b656-115">Pour plus d’informations, consultez [Installer Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9b656-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="9b656-116">Avant de commencer la configuration, vous devez examiner les [conditions préalables](expressroute-prerequisites.md), la [configuration requise pour le routage](expressroute-routing.md) et les [flux de travail](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="9b656-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="9b656-117">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="9b656-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="9b656-118">Suivez les instructions permettant de [créer un circuit ExpressRoute](howto-circuit-cli.md) et faites-le activer par votre fournisseur de service de connectivité.</span><span class="sxs-lookup"><span data-stu-id="9b656-118">Follow the instructions to [create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="9b656-119">Vérifiez que l’homologation privée Azure est configurée pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="9b656-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="9b656-120">Pour obtenir des instructions de routage, consultez l'article sur la [configuration du routage](howto-routing-cli.md) .</span><span class="sxs-lookup"><span data-stu-id="9b656-120">See the [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="9b656-121">Assurez-vous que l’homologation privée Azure est configurée.</span><span class="sxs-lookup"><span data-stu-id="9b656-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="9b656-122">L’homologation BGP entre votre réseau et Microsoft doit être opérationnelle pour que vous puissiez activer la connectivité de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="9b656-122">The BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="9b656-123">Vérifiez qu’un réseau virtuel et une passerelle de réseau virtuel ont été créés et entièrement approvisionnés.</span><span class="sxs-lookup"><span data-stu-id="9b656-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="9b656-124">Suivez les instructions fournies dans l’article [Configurer une passerelle de réseau virtuel pour ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="9b656-124">Follow the instructions to [Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="9b656-125">Veillez à utiliser `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="9b656-125">Be sure to use `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="9b656-126">Vous pouvez lier jusqu’à 10 réseaux virtuels à un circuit ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="9b656-126">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="9b656-127">Tous les réseaux virtuels doivent figurer dans la même région géopolitique lors de l’utilisation d’un circuit ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="9b656-127">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="9b656-128">Si vous avez activé le module complémentaire ExpressRoute Premium, vous pouvez lier un réseau virtuel à l’extérieur de la zone géopolitique du circuit ExpressRoute ou connecter un plus grand nombre de réseaux virtuels à votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b656-128">If you enable the ExpressRoute premium add-on, you can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="9b656-129">Pour plus d’informations sur le module complémentaire Premium, consultez le [FAQ ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="9b656-129">For more information about the premium add-on, see the [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="9b656-130">Connecter un réseau virtuel du même abonnement à un circuit</span><span class="sxs-lookup"><span data-stu-id="9b656-130">Connect a virtual network in the same subscription to a circuit</span></span>

<span data-ttu-id="9b656-131">Vous pouvez connecter une passerelle de réseau virtuel à un circuit ExpressRoute à l’aide de l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="9b656-131">You can connect a virtual network gateway to an ExpressRoute circuit by using the example.</span></span> <span data-ttu-id="9b656-132">Assurez-vous que la passerelle de réseau virtuel est créée et prête pour la liaison avant d’exécuter la commande.</span><span class="sxs-lookup"><span data-stu-id="9b656-132">Make sure that the virtual network gateway is created and is ready for linking before you run the command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="9b656-133">Connecter un réseau virtuel d’un autre abonnement à un circuit</span><span class="sxs-lookup"><span data-stu-id="9b656-133">Connect a virtual network in a different subscription to a circuit</span></span>

<span data-ttu-id="9b656-134">Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="9b656-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="9b656-135">La figure suivante montre un schéma simple sur le fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="9b656-135">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="9b656-136">Chacun des petits clouds dans le cloud principal est utilisé pour représenter les abonnements appartenant à différents services au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="9b656-136">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="9b656-137">Chacun des services au sein de l’organisation peut utiliser son propre abonnement pour déployer ses services, mais ils peuvent partager un même circuit ExpressRoute pour se connecter à votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="9b656-137">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="9b656-138">Un seul service (dans cet exemple, le service informatique) peut posséder le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b656-138">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="9b656-139">D’autres abonnements au sein de l’organisation peuvent utiliser le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b656-139">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="9b656-140">Les frais de connectivité et de bande passante pour le circuit dédié s’appliquent au propriétaire du circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b656-140">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="9b656-141">Tous les réseaux virtuels partagent la même bande passante.</span><span class="sxs-lookup"><span data-stu-id="9b656-141">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="9b656-143">Administration : propriétaires de circuit et utilisateurs du circuit</span><span class="sxs-lookup"><span data-stu-id="9b656-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="9b656-144">Le « propriétaire du circuit » est un utilisateur avancé autorisé de la ressource de circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b656-144">The 'Circuit Owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="9b656-145">Le propriétaire du circuit peut créer des autorisations utilisables par les « utilisateurs du circuit ».</span><span class="sxs-lookup"><span data-stu-id="9b656-145">The Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="9b656-146">Les utilisateurs du circuit sont les propriétaires des passerelles de réseau virtuel qui ne figurent pas dans le même abonnement que le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b656-146">Circuit Users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="9b656-147">Les utilisateurs du circuit peuvent utiliser des autorisations (une seule autorisation par réseau virtuel).</span><span class="sxs-lookup"><span data-stu-id="9b656-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="9b656-148">Le propriétaire du circuit a le pouvoir de modifier et de révoquer les autorisations à tout moment.</span><span class="sxs-lookup"><span data-stu-id="9b656-148">The Circuit Owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="9b656-149">Lorsqu’une autorisation est révoquée, toutes les connexions sont supprimées de l’abonnement dont l’accès a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="9b656-149">When an authorization is revoked, all link connections are deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="9b656-150">Opérations du propriétaire du circuit</span><span class="sxs-lookup"><span data-stu-id="9b656-150">Circuit Owner operations</span></span>

<span data-ttu-id="9b656-151">**Création d’une autorisation**</span><span class="sxs-lookup"><span data-stu-id="9b656-151">**To create an authorization**</span></span>

<span data-ttu-id="9b656-152">Le propriétaire du circuit crée une autorisation, ce qui entraîne la création d’une clé d’autorisation qui peut être utilisée par un utilisateur du circuit pour connecter ses passerelles de réseau virtuel à un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9b656-152">The Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="9b656-153">Une autorisation n’est valide que pour une seule connexion.</span><span class="sxs-lookup"><span data-stu-id="9b656-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="9b656-154">L’exemple suivant montre comment créer une autorisation :</span><span class="sxs-lookup"><span data-stu-id="9b656-154">The following example shows how to create an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="9b656-155">La réponse contient la clé et l’état d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="9b656-155">The response contains the authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="9b656-156">**Vérification des autorisations**</span><span class="sxs-lookup"><span data-stu-id="9b656-156">**To review authorizations**</span></span>

<span data-ttu-id="9b656-157">Le propriétaire du circuit peut vérifier toutes les autorisations émises pour un circuit donné en exécutant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9b656-157">The Circuit Owner can review all authorizations that are issued on a particular circuit by running the following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="9b656-158">**Ajout d’autorisations**</span><span class="sxs-lookup"><span data-stu-id="9b656-158">**To add authorizations**</span></span>

<span data-ttu-id="9b656-159">Le propriétaire du circuit peut ajouter des autorisations à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9b656-159">The Circuit Owner can add authorizations by using the following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="9b656-160">**Suppression d’autorisations**</span><span class="sxs-lookup"><span data-stu-id="9b656-160">**To delete authorizations**</span></span>

<span data-ttu-id="9b656-161">Le propriétaire du circuit peut révoquer/supprimer les autorisations accordées à l’utilisateur en exécutant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9b656-161">The Circuit Owner can revoke/delete authorizations to the user by running the following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="9b656-162">Opérations de l’utilisateur du circuit</span><span class="sxs-lookup"><span data-stu-id="9b656-162">Circuit User operations</span></span>

<span data-ttu-id="9b656-163">L’utilisateur du circuit a besoin de l’ID de pair et d’une clé d’autorisation de la part du propriétaire du circuit.</span><span class="sxs-lookup"><span data-stu-id="9b656-163">The Circuit User needs the peer ID and an authorization key from the Circuit Owner.</span></span> <span data-ttu-id="9b656-164">La clé d'autorisation est un GUID.</span><span class="sxs-lookup"><span data-stu-id="9b656-164">The authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="9b656-165">**Réclamation d’une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="9b656-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="9b656-166">L’utilisateur du circuit peut exécuter l’applet de commande suivante pour utiliser une autorisation de liaison :</span><span class="sxs-lookup"><span data-stu-id="9b656-166">The Circuit User can run the following example to redeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="9b656-167">**Libération d’une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="9b656-167">**To release a connection authorization**</span></span>

<span data-ttu-id="9b656-168">Vous pouvez libérer une autorisation en supprimant la connexion qui lie le circuit ExpressRoute et le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9b656-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b656-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b656-169">Next steps</span></span>

<span data-ttu-id="9b656-170">Pour plus d'informations sur ExpressRoute, consultez le [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="9b656-170">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>