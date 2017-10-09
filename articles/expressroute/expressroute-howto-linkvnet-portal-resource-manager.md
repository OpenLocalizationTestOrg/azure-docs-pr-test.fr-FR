---
title: "Lier un circuit ExpressRoute de tooan réseau virtuel : portail Azure | Documents Microsoft"
description: "Ce document fournit une vue d’ensemble du mode toolink virtuel réseaux des circuits tooExpressRoute (réseaux virtuels)."
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
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="19c91-103">Se connecter à un circuit ExpressRoute de tooan réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="19c91-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19c91-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="19c91-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="19c91-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="19c91-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="19c91-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="19c91-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="19c91-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="19c91-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="19c91-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="19c91-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="19c91-109">Cet article vous permet de lier des circuits ExpressRoute de tooAzure des réseaux virtuels (réseaux virtuels) à l’aide du modèle de déploiement du Gestionnaire de ressources hello et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="19c91-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and hello Azure portal.</span></span> <span data-ttu-id="19c91-110">Réseaux virtuels peuvent être soit Bonjour les même abonnement, ou ils peuvent faire partie d’un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="19c91-110">Virtual networks can either be in hello same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="19c91-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="19c91-111">Before you begin</span></span>
* <span data-ttu-id="19c91-112">Hello de révision [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="19c91-112">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="19c91-113">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="19c91-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="19c91-114">Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) et avoir des circuits hello activé par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="19c91-114">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="19c91-115">Vérifiez que l’homologation privée Azure est configurée pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="19c91-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="19c91-116">Consultez hello [configurer le routage](expressroute-howto-routing-portal-resource-manager.md) article pour obtenir des instructions de routage.</span><span class="sxs-lookup"><span data-stu-id="19c91-116">See hello [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="19c91-117">Assurez-vous que l’homologation privée Azure est configuré et est l’homologation BGP hello entre votre réseau et de Microsoft afin que vous pouvez activer la connectivité de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="19c91-117">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="19c91-118">Vérifiez qu’un réseau virtuel et une passerelle de réseau virtuel ont été créés et entièrement approvisionnés.</span><span class="sxs-lookup"><span data-stu-id="19c91-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="19c91-119">Suivez les instructions de hello trop[créer une passerelle de réseau virtuel pour ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="19c91-119">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="19c91-120">Une passerelle de réseau virtuel pour ExpressRoute utilise hello « ExpressRoute », le type de passerelle VPN pas.</span><span class="sxs-lookup"><span data-stu-id="19c91-120">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="19c91-121">Vous pouvez lier de circuit de ExpressRoute standard too10 réseaux virtuels tooa.</span><span class="sxs-lookup"><span data-stu-id="19c91-121">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="19c91-122">Tous les réseaux virtuels doivent être Bonjour même région géopolitique lors de l’utilisation d’un circuit ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="19c91-122">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="19c91-123">Vous pouvez lier un réseau virtuel en dehors de la région de hello géopolitique de hello circuit ExpressRoute ou vous connecter à un plus grand nombre de réseaux virtuels tooyour circuit ExpressRoute si vous avez activé le module complémentaire de hello ExpressRoute premium.</span><span class="sxs-lookup"><span data-stu-id="19c91-123">You can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="19c91-124">Vérifiez hello [FAQ](expressroute-faqs.md) pour plus d’informations sur le module complémentaire de hello premium.</span><span class="sxs-lookup"><span data-stu-id="19c91-124">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>
* <span data-ttu-id="19c91-125">Vous pouvez [visualiser une vidéo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) avant le début toobetter comprendre les étapes hello.</span><span class="sxs-lookup"><span data-stu-id="19c91-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning toobetter understand hello steps.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="19c91-126">Connecter un réseau virtuel Bonjour même circuit de tooa d’abonnement</span><span class="sxs-lookup"><span data-stu-id="19c91-126">Connect a virtual network in hello same subscription tooa circuit</span></span>

### <a name="toocreate-a-connection"></a><span data-ttu-id="19c91-127">toocreate une connexion</span><span class="sxs-lookup"><span data-stu-id="19c91-127">toocreate a connection</span></span>

> [!NOTE]
> <span data-ttu-id="19c91-128">Informations sur la configuration BGP seront afficheront pas si le fournisseur de couche 3 hello configuré votre homologations.</span><span class="sxs-lookup"><span data-stu-id="19c91-128">BGP configuration information will not show up if hello layer 3 provider configured your peerings.</span></span> <span data-ttu-id="19c91-129">Si votre circuit est dans un état configuré, vous devez être en mesure de toocreate connexions.</span><span class="sxs-lookup"><span data-stu-id="19c91-129">If your circuit is in a provisioned state, you should be able toocreate connections.</span></span>
>

1. <span data-ttu-id="19c91-130">Assurez-vous que votre circuit ExpressRoute et l'homologation privée Azure ont été correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="19c91-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="19c91-131">Suivez les instructions de hello dans [créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et [configurer le routage](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="19c91-131">Follow hello instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="19c91-132">Votre circuit ExpressRoute doit ressembler à hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="19c91-132">Your ExpressRoute circuit should look like hello following image:</span></span>

    ![Capture d’écran Circuit ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="19c91-134">Vous pouvez maintenant commencer l’approvisionnement un toolink connexion votre tooyour de passerelle de réseau virtuel circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="19c91-134">You can now start provisioning a connection toolink your virtual network gateway tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="19c91-135">Cliquez sur **connexion** > **ajouter** tooopen hello **ajouter une connexion** panneau, puis configurez les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="19c91-135">Click **Connection** > **Add** tooopen hello **Add connection** blade, and then configure hello values.</span></span>

    ![Capture d’écran Ajouter une connexion](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="19c91-137">Une fois que votre connexion a été correctement configurée, votre objet de connexion affiche les informations de hello pour les connexions hello.</span><span class="sxs-lookup"><span data-stu-id="19c91-137">After your connection has been successfully configured, your connection object will show hello information for hello connection.</span></span>

     ![Capture d’écran Objet de connexion](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a><span data-ttu-id="19c91-139">toodelete une connexion</span><span class="sxs-lookup"><span data-stu-id="19c91-139">toodelete a connection</span></span>
<span data-ttu-id="19c91-140">Vous pouvez supprimer une connexion en sélectionnant hello **supprimer** icône Panneau hello pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="19c91-140">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="19c91-141">Connecter un réseau virtuel dans un circuit de tooa autre abonnement</span><span class="sxs-lookup"><span data-stu-id="19c91-141">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="19c91-142">Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="19c91-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="19c91-143">la figure ci-dessous Hello schématique simple de fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="19c91-143">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="19c91-145">Chaque hello petits clouds dans cloud volumineux de hello est utilisé toorepresent abonnements appartenant aux départements toodifferent au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="19c91-145">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span>
- <span data-ttu-id="19c91-146">Chacun des services hello au sein de l’organisation de hello permettre utiliser leur propre abonnement pour le déploiement de leurs services, mais elles peuvent partager un réseau local ExpressRoute circuit tooconnect tooyour précédent.</span><span class="sxs-lookup"><span data-stu-id="19c91-146">Each of hello departments within hello organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span>
- <span data-ttu-id="19c91-147">Un seul département (dans cet exemple : informatique) peut posséder de circuit ExpressRoute de hello.</span><span class="sxs-lookup"><span data-stu-id="19c91-147">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="19c91-148">Autres abonnements au sein de l’organisation de hello peuvent utiliser le circuit ExpressRoute de hello.</span><span class="sxs-lookup"><span data-stu-id="19c91-148">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="19c91-149">Frais de connectivité et de bande passante pour le circuit de hello dédié sera propriétaire du circuit ExpressRoute toohello appliqué.</span><span class="sxs-lookup"><span data-stu-id="19c91-149">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="19c91-150">Tous les réseaux virtuels partagent hello même bande passante.</span><span class="sxs-lookup"><span data-stu-id="19c91-150">All virtual networks share hello same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="19c91-151">Administration - propriétaires de circuit et utilisateurs de circuit</span><span class="sxs-lookup"><span data-stu-id="19c91-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="19c91-152">Hello propriétaire du circuit est un utilisateur autorisé de la puissance de hello ressource de circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="19c91-152">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="19c91-153">propriétaire du circuit Hello peut créer des autorisations qui peuvent être utilisées par les utilisateurs de circuit.</span><span class="sxs-lookup"><span data-stu-id="19c91-153">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="19c91-154">Les utilisateurs de circuit sont les propriétaires du réseau virtuel qui ne sont pas dans les passerelles hello même abonnement que hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="19c91-154">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="19c91-155">Les utilisateurs du circuit peuvent échanger des autorisations (une seule autorisation par réseau virtuel).</span><span class="sxs-lookup"><span data-stu-id="19c91-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="19c91-156">propriétaire du circuit Hello possède les autorisations hello power toomodify et révoquer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="19c91-156">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="19c91-157">Révocation de des résultats d’autorisation dans toutes les connexions de la liaison en cours de suppression de l’abonnement hello dont l’accès a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="19c91-157">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="19c91-158">Opérations du propriétaire du circuit</span><span class="sxs-lookup"><span data-stu-id="19c91-158">Circuit owner operations</span></span>

<span data-ttu-id="19c91-159">**toocreate une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="19c91-159">**toocreate a connection authorization**</span></span>

<span data-ttu-id="19c91-160">propriétaire du circuit Hello crée une autorisation.</span><span class="sxs-lookup"><span data-stu-id="19c91-160">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="19c91-161">Cela entraîne la création de hello d’une clé d’autorisation qui peut être utilisé par un tooconnect utilisateur de circuit leur toohello de passerelles de réseau virtuel circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="19c91-161">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="19c91-162">Une autorisation n’est valide que pour une seule connexion.</span><span class="sxs-lookup"><span data-stu-id="19c91-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="19c91-163">Dans le panneau de ExpressRoute hello, cliquez sur **autorisations** , puis tapez un **nom** pour l’autorisation de hello et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="19c91-163">In hello ExpressRoute blade, Click **Authorizations** and then type a **name** for hello authorization and click **Save**.</span></span>

    ![Autorisations](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="19c91-165">Une fois l’enregistrement de la configuration hello copier hello **ID de ressource** et hello **clé d’autorisation**.</span><span class="sxs-lookup"><span data-stu-id="19c91-165">Once hello configuration is saved, copy hello **Resource ID** and hello **Authorization Key**.</span></span>

    ![Clé d’autorisation](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="19c91-167">**toodelete une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="19c91-167">**toodelete a connection authorization**</span></span>

<span data-ttu-id="19c91-168">Vous pouvez supprimer une connexion en sélectionnant hello **supprimer** icône Panneau hello pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="19c91-168">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="19c91-169">Opérations de l’utilisateur du circuit</span><span class="sxs-lookup"><span data-stu-id="19c91-169">Circuit user operations</span></span>

<span data-ttu-id="19c91-170">utilisateur du circuit Hello a besoin d’ID de ressource hello et une clé d’autorisation du propriétaire du circuit hello.</span><span class="sxs-lookup"><span data-stu-id="19c91-170">hello circuit user needs hello resource ID and an authorization key from hello circuit owner.</span></span> 

<span data-ttu-id="19c91-171">**tooredeem une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="19c91-171">**tooredeem a connection authorization**</span></span>

1.  <span data-ttu-id="19c91-172">Cliquez sur hello **+ nouveau** bouton.</span><span class="sxs-lookup"><span data-stu-id="19c91-172">Click hello **+New** button.</span></span>

    ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="19c91-174">Recherchez **« Connexion »** Bonjour Marketplace, sélectionnez-le, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="19c91-174">Search for **"Connection"** in hello Marketplace, select it, and click **Create**.</span></span>

    ![Rechercher une connexion](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="19c91-176">Vérifiez que hello **type de connexion** est défini trop « ExpressRoute ».</span><span class="sxs-lookup"><span data-stu-id="19c91-176">Make sure hello **Connection type** is set too"ExpressRoute".</span></span>


4.  <span data-ttu-id="19c91-177">Renseignez les détails de hello, puis cliquez sur **OK** dans le panneau des principes de base hello.</span><span class="sxs-lookup"><span data-stu-id="19c91-177">Fill in hello details, then click **OK** in hello Basics blade.</span></span>

    ![Panneau Informations de base](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="19c91-179">Bonjour **paramètres** panneau, sélectionnez hello **passerelle de réseau virtuel** et vérifiez hello **échanger d’autorisation** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="19c91-179">In hello **Settings** blade, Select hello **Virtual network gateway** and check hello **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="19c91-180">Entrez hello **clé d’autorisation** et hello **homologue circuit URI** et renommer les connexions hello.</span><span class="sxs-lookup"><span data-stu-id="19c91-180">Enter hello **Authorization key** and hello **Peer circuit URI** and give hello connection a name.</span></span> <span data-ttu-id="19c91-181">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="19c91-181">Click **OK**.</span></span>

    ![Panneau Paramètres](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="19c91-183">Passez en revue les informations de hello Bonjour **Résumé** panneau, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="19c91-183">Review hello information in hello **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="19c91-184">**toorelease une autorisation de connexion**</span><span class="sxs-lookup"><span data-stu-id="19c91-184">**toorelease a connection authorization**</span></span>

<span data-ttu-id="19c91-185">Vous pouvez libérer une autorisation en supprimant la connexion hello qui établit un lien réseau virtuel du toohello circuit ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="19c91-185">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19c91-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19c91-186">Next steps</span></span>
<span data-ttu-id="19c91-187">Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="19c91-187">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
