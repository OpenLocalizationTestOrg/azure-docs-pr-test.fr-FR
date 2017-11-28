---
title: "Lier un réseau virtuel à un circuit ExpressRoute à l’aide du portail Azure | Microsoft Docs"
description: "Ce document fournit une vue d’ensemble de la façon de lier des réseaux virtuels à des circuits ExpressRoute."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 595c30ab5d9adc6061ad753d952adf894ba80b2f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="21e4f-103">Connecter un réseau virtuel à un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="21e4f-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21e4f-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="21e4f-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="21e4f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21e4f-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="21e4f-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="21e4f-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="21e4f-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="21e4f-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="21e4f-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="21e4f-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="21e4f-109">Cet article vous aide à lier des réseaux virtuels à des circuits Azure ExpressRoute en utilisant le modèle de déploiement Resource Manager et le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21e4f-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and the Azure portal.</span></span> <span data-ttu-id="21e4f-110">Les réseaux virtuels peuvent appartenir au même abonnement ou faire partie d’un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="21e4f-110">Virtual networks can either be in the same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="21e4f-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="21e4f-111">Before you begin</span></span>
* <span data-ttu-id="21e4f-112">Avant de commencer la configuration, examinez les [conditions préalables](expressroute-prerequisites.md), la [configuration requise pour le routage](expressroute-routing.md) et les [flux de travail](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="21e4f-112">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="21e4f-113">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="21e4f-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="21e4f-114">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) et faites-le activer par votre fournisseur de service de connectivité.</span><span class="sxs-lookup"><span data-stu-id="21e4f-114">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="21e4f-115">Vérifiez que l’homologation privée Azure est configurée pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="21e4f-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="21e4f-116">Pour obtenir des instructions sur le routage, consultez l’article [Configurer le routage](expressroute-howto-routing-portal-resource-manager.md) .</span><span class="sxs-lookup"><span data-stu-id="21e4f-116">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="21e4f-117">Vérifiez que l’homologation privée Azure est être configurée, et que l’homologation BGP entre votre réseau et Microsoft est être opérationnelle pour pouvoir activer la connectivité de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="21e4f-117">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="21e4f-118">Vérifiez qu’un réseau virtuel et une passerelle de réseau virtuel ont été créés et entièrement approvisionnés.</span><span class="sxs-lookup"><span data-stu-id="21e4f-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="21e4f-119">Suivez les instructions pour [créer une passerelle de réseau virtuel pour ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="21e4f-119">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="21e4f-120">Une passerelle de réseau virtuel pour ExpressRoute utilise le type de passerelle « ExpressRoute », pas de VPN.</span><span class="sxs-lookup"><span data-stu-id="21e4f-120">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="21e4f-121">Vous pouvez lier jusqu’à 10 réseaux virtuels à un circuit ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="21e4f-121">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="21e4f-122">Tous les réseaux virtuels doivent figurer dans la même région géopolitique lors de l’utilisation d’un circuit ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="21e4f-122">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="21e4f-123">Vous pouvez lier un réseau virtuel à l’extérieur de la zone géopolitique du circuit ExpressRoute ou lier un plus grand nombre de réseaux virtuels à votre circuit ExpressRoute si vous avez activé le module complémentaire Premium d’ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="21e4f-123">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="21e4f-124">Pour plus d’informations sur le module complémentaire Premium, consultez le [FAQ](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="21e4f-124">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>
* <span data-ttu-id="21e4f-125">Vous pouvez [visualiser une vidéo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) avant de commencer afin de mieux comprendre les étapes.</span><span class="sxs-lookup"><span data-stu-id="21e4f-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="21e4f-126">Connecter un réseau virtuel du même abonnement à un circuit</span><span class="sxs-lookup"><span data-stu-id="21e4f-126">Connect a virtual network in the same subscription to a circuit</span></span>

### <a name="to-create-a-connection"></a><span data-ttu-id="21e4f-127">Pour créer une connexion</span><span class="sxs-lookup"><span data-stu-id="21e4f-127">To create a connection</span></span>

> [!NOTE]
> <span data-ttu-id="21e4f-128">Les informations de configuration BGP ne s’affichent pas si vos homologations ont été configurées par le fournisseur de la couche 3.</span><span class="sxs-lookup"><span data-stu-id="21e4f-128">BGP configuration information will not show up if the layer 3 provider configured your peerings.</span></span> <span data-ttu-id="21e4f-129">Si votre circuit est dans l’état Approvisionné, vous pouvez créer des connexions.</span><span class="sxs-lookup"><span data-stu-id="21e4f-129">If your circuit is in a provisioned state, you should be able to create connections.</span></span>
>

1. <span data-ttu-id="21e4f-130">Assurez-vous que votre circuit ExpressRoute et l'homologation privée Azure ont été correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="21e4f-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="21e4f-131">Suivez les instructions dans [Créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et [Configurer le routage](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="21e4f-131">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="21e4f-132">Votre circuit ExpressRoute doit être similaire à l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="21e4f-132">Your ExpressRoute circuit should look like the following image:</span></span>

    ![Capture d’écran Circuit ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="21e4f-134">Vous pouvez maintenant commencer à approvisionner une connexion pour lier votre passerelle de réseau virtuel à votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="21e4f-134">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span></span> <span data-ttu-id="21e4f-135">Cliquez sur **Connexion** > **Ajouter** pour ouvrir le panneau **Ajouter une connexion**, puis configurez les valeurs.</span><span class="sxs-lookup"><span data-stu-id="21e4f-135">Click **Connection** > **Add** to open the **Add connection** blade, and then configure the values.</span></span>

    ![Capture d’écran Ajouter une connexion](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="21e4f-137">Une fois votre connexion correctement configurée, votre objet de connexion affiche les informations de la connexion.</span><span class="sxs-lookup"><span data-stu-id="21e4f-137">After your connection has been successfully configured, your connection object will show the information for the connection.</span></span>

     ![Capture d’écran Objet de connexion](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="to-delete-a-connection"></a><span data-ttu-id="21e4f-139">Suppression d'une connexion</span><span class="sxs-lookup"><span data-stu-id="21e4f-139">To delete a connection</span></span>
<span data-ttu-id="21e4f-140">Vous pouvez supprimer une connexion en sélectionnant l’icône **Supprimer** dans le panneau de votre connexion.</span><span class="sxs-lookup"><span data-stu-id="21e4f-140">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="21e4f-141">Connecter un réseau virtuel d’un autre abonnement à un circuit</span><span class="sxs-lookup"><span data-stu-id="21e4f-141">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="21e4f-142">Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="21e4f-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="21e4f-143">La figure suivante montre un schéma simple sur le fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="21e4f-143">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="21e4f-145">Chacun des petits clouds dans le cloud principal est utilisé pour représenter les abonnements appartenant à différents services au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="21e4f-145">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span>
- <span data-ttu-id="21e4f-146">Chacun des services au sein de l’organisation peut utiliser son propre abonnement pour déployer ses services, mais ils peuvent partager un même circuit ExpressRoute pour se connecter à votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="21e4f-146">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span>
- <span data-ttu-id="21e4f-147">Un seul service (dans cet exemple, le service informatique) peut posséder le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="21e4f-147">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="21e4f-148">D’autres abonnements au sein de l’organisation peuvent utiliser le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="21e4f-148">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="21e4f-149">Les frais de connectivité et de bande passante pour le circuit dédié s’appliquent au propriétaire du circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="21e4f-149">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="21e4f-150">Tous les réseaux virtuels partagent la même bande passante.</span><span class="sxs-lookup"><span data-stu-id="21e4f-150">All virtual networks share the same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="21e4f-151">Administration - propriétaires de circuit et utilisateurs de circuit</span><span class="sxs-lookup"><span data-stu-id="21e4f-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="21e4f-152">Le « propriétaire du circuit » est l’utilisateur avec pouvoir autorisé de la ressource de circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="21e4f-152">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="21e4f-153">Le propriétaire du circuit peut créer des autorisations utilisables par les « utilisateurs du circuit ».</span><span class="sxs-lookup"><span data-stu-id="21e4f-153">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="21e4f-154">Les utilisateurs du circuit sont les propriétaires des passerelles de réseau virtuel qui ne figurent pas dans le même abonnement que le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="21e4f-154">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="21e4f-155">Les utilisateurs du circuit peuvent échanger des autorisations (une seule autorisation par réseau virtuel).</span><span class="sxs-lookup"><span data-stu-id="21e4f-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="21e4f-156">Le propriétaire du circuit a le pouvoir de modifier et de révoquer les autorisations à tout moment.</span><span class="sxs-lookup"><span data-stu-id="21e4f-156">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="21e4f-157">La révocation d’une autorisation entraîne la suppression de toutes les connexions de l’abonnement dont l’accès a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="21e4f-157">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="21e4f-158">Opérations du propriétaire du circuit</span><span class="sxs-lookup"><span data-stu-id="21e4f-158">Circuit owner operations</span></span>

<span data-ttu-id="21e4f-159">**Création d’une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="21e4f-159">**To create a connection authorization**</span></span>

<span data-ttu-id="21e4f-160">Le propriétaire du circuit crée une autorisation.</span><span class="sxs-lookup"><span data-stu-id="21e4f-160">The circuit owner creates an authorization.</span></span> <span data-ttu-id="21e4f-161">Cela entraîne la création d'une clé d'autorisation qui peut être utilisée par un utilisateur du circuit pour se connecter à ses passerelles de réseau virtuel vers un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="21e4f-161">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="21e4f-162">Une autorisation n’est valide que pour une seule connexion.</span><span class="sxs-lookup"><span data-stu-id="21e4f-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="21e4f-163">Dans le panneau ExpressRoute, cliquez sur **Autorisations**. Tapez un **nom** pour l’autorisation, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="21e4f-163">In the ExpressRoute blade, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span></span>

    ![Autorisations](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="21e4f-165">Une fois la configuration enregistrée, copiez **l’ID de ressource** et la **clé d’autorisation**.</span><span class="sxs-lookup"><span data-stu-id="21e4f-165">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span></span>

    ![Clé d’autorisation](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="21e4f-167">**Suppression d’une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="21e4f-167">**To delete a connection authorization**</span></span>

<span data-ttu-id="21e4f-168">Vous pouvez supprimer une connexion en sélectionnant l’icône **Supprimer** dans le panneau de votre connexion.</span><span class="sxs-lookup"><span data-stu-id="21e4f-168">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="21e4f-169">Opérations de l’utilisateur du circuit</span><span class="sxs-lookup"><span data-stu-id="21e4f-169">Circuit user operations</span></span>

<span data-ttu-id="21e4f-170">L’utilisateur du circuit a besoin de l’ID de ressource et d’une clé d’autorisation du propriétaire du circuit.</span><span class="sxs-lookup"><span data-stu-id="21e4f-170">The circuit user needs the resource ID and an authorization key from the circuit owner.</span></span> 

<span data-ttu-id="21e4f-171">**Réclamation d’une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="21e4f-171">**To redeem a connection authorization**</span></span>

1.  <span data-ttu-id="21e4f-172">Cliquez sur le bouton **+Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="21e4f-172">Click the **+New** button.</span></span>

    ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="21e4f-174">Recherchez l’option **Connexion** dans la Place de marché. Sélectionnez-la, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="21e4f-174">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span></span>

    ![Rechercher une connexion](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="21e4f-176">Vérifiez que l’option **Type de connexion** est définie sur « ExpressRoute ».</span><span class="sxs-lookup"><span data-stu-id="21e4f-176">Make sure the **Connection type** is set to "ExpressRoute".</span></span>


4.  <span data-ttu-id="21e4f-177">Renseignez les détails, puis cliquez sur **OK** dans le panneau De base.</span><span class="sxs-lookup"><span data-stu-id="21e4f-177">Fill in the details, then click **OK** in the Basics blade.</span></span>

    ![Panneau Informations de base](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="21e4f-179">Dans le panneau **Paramètres**, sélectionnez **Passerelle de réseau virtuel**, puis cochez la case **Redeem authorization** (Réclamer l’autorisation).</span><span class="sxs-lookup"><span data-stu-id="21e4f-179">In the **Settings** blade, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="21e4f-180">Entrez la **clé d’autorisation** et **l’URI du circuit appairé**, puis donnez un nom à la connexion.</span><span class="sxs-lookup"><span data-stu-id="21e4f-180">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span></span> <span data-ttu-id="21e4f-181">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="21e4f-181">Click **OK**.</span></span>

    ![Panneau Paramètres](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="21e4f-183">Passez en revue les informations contenues dans le panneau **Résumé**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="21e4f-183">Review the information in the **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="21e4f-184">**Libération d’une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="21e4f-184">**To release a connection authorization**</span></span>

<span data-ttu-id="21e4f-185">Vous pouvez libérer une autorisation en supprimant la connexion qui lie le circuit ExpressRoute et le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="21e4f-185">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21e4f-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21e4f-186">Next steps</span></span>
<span data-ttu-id="21e4f-187">Pour plus d'informations sur ExpressRoute, consultez le [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="21e4f-187">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
