---
title: "Lier un circuit ExpressRoute de tooan réseau virtuel : PowerShell : classique : Azure | Documents Microsoft"
description: "Ce document fournit une vue d’ensemble du mode toolink virtuel réseaux (réseaux virtuels) tooExpressRoute circuits à l’aide de PowerShell et le modèle de déploiement classique hello."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="54ad1-103">Se connecter à un circuit ExpressRoute de tooan de réseau virtuel à l’aide de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="54ad1-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="54ad1-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="54ad1-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="54ad1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="54ad1-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="54ad1-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="54ad1-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="54ad1-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="54ad1-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="54ad1-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="54ad1-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="54ad1-109">Cet article vous aidera à lier des circuits ExpressRoute de tooAzure des réseaux virtuels (réseaux virtuels) à l’aide de PowerShell et le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="54ad1-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="54ad1-110">Réseaux virtuels peuvent être dans hello même abonnement ou peuvent faire partie d’un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="54ad1-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="54ad1-111">**À propos des modèles de déploiement Azure**</span><span class="sxs-lookup"><span data-stu-id="54ad1-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="54ad1-112">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="54ad1-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="54ad1-113">Vous devez la version la plus récente des modules d’Azure PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="54ad1-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="54ad1-114">Vous pouvez télécharger les modules PowerShell dernière hello hello section PowerShell de hello [page de téléchargements Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="54ad1-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="54ad1-115">Suivez les instructions de hello dans [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour obtenir des instructions sur la façon de tooconfigure votre ordinateur toouse hello Azure les modules PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54ad1-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="54ad1-116">Vous devez tooreview hello [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="54ad1-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="54ad1-117">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="54ad1-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="54ad1-118">Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et à ce que votre fournisseur de connectivité Active circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="54ad1-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="54ad1-119">Vérifiez que l’homologation privée Azure est configurée pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="54ad1-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="54ad1-120">Consultez hello [configurer le routage](expressroute-howto-routing-classic.md) article pour obtenir des instructions de routage.</span><span class="sxs-lookup"><span data-stu-id="54ad1-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="54ad1-121">Assurez-vous que l’homologation privée Azure est configuré et est l’homologation BGP hello entre votre réseau et de Microsoft afin que vous pouvez activer la connectivité de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="54ad1-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="54ad1-122">Vous devez disposer d'un réseau virtuel et d’une passerelle de réseau virtuel créés et totalement approvisionnés.</span><span class="sxs-lookup"><span data-stu-id="54ad1-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="54ad1-123">Suivez les instructions de hello trop[configurer un réseau virtuel pour ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="54ad1-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="54ad1-124">Vous pouvez lier des réseaux virtuels de too10 tooan circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="54ad1-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="54ad1-125">Tous les réseaux virtuels doivent être Bonjour même région géopolitique.</span><span class="sxs-lookup"><span data-stu-id="54ad1-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="54ad1-126">Vous pouvez lier un plus grand nombre de réseaux virtuels tooyour circuit ExpressRoute, ou lier des réseaux virtuels situés dans d’autres régions géopolitiques si vous avez activé le module complémentaire de hello ExpressRoute premium.</span><span class="sxs-lookup"><span data-stu-id="54ad1-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="54ad1-127">Vérifiez hello [FAQ](expressroute-faqs.md) pour plus d’informations sur le module complémentaire de hello premium.</span><span class="sxs-lookup"><span data-stu-id="54ad1-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="54ad1-128">Connecter un réseau virtuel Bonjour même circuit de tooa d’abonnement</span><span class="sxs-lookup"><span data-stu-id="54ad1-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="54ad1-129">Vous pouvez lier un circuit ExpressRoute de tooan réseau virtuel à l’aide de hello suivant l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54ad1-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="54ad1-130">Assurez-vous que cette passerelle de réseau virtuel hello est créée et est prête pour la liaison avant d’exécuter les applets de commande hello.</span><span class="sxs-lookup"><span data-stu-id="54ad1-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="54ad1-131">Connecter un réseau virtuel dans un circuit de tooa autre abonnement</span><span class="sxs-lookup"><span data-stu-id="54ad1-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="54ad1-132">Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="54ad1-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="54ad1-133">Hello figure suivante montre une simple principe de fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="54ad1-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="54ad1-134">Chaque hello petits clouds dans cloud volumineux de hello est utilisé toorepresent abonnements appartenant aux départements toodifferent au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="54ad1-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="54ad1-135">Chacun des services hello au sein de l’organisation de hello permettre utiliser leur propre abonnement pour déployer leurs services--mais les services de hello peut partager un réseau local ExpressRoute circuit tooconnect tooyour précédent.</span><span class="sxs-lookup"><span data-stu-id="54ad1-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="54ad1-136">Un seul département (dans cet exemple : informatique) peut posséder de circuit ExpressRoute de hello.</span><span class="sxs-lookup"><span data-stu-id="54ad1-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="54ad1-137">Autres abonnements au sein de l’organisation de hello peuvent utiliser le circuit ExpressRoute de hello.</span><span class="sxs-lookup"><span data-stu-id="54ad1-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="54ad1-138">Frais de connectivité et de bande passante pour le circuit de hello dédié sera propriétaire du circuit ExpressRoute toohello appliqué.</span><span class="sxs-lookup"><span data-stu-id="54ad1-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="54ad1-139">Tous les réseaux virtuels partagent hello même bande passante.</span><span class="sxs-lookup"><span data-stu-id="54ad1-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="54ad1-141">Administration</span><span class="sxs-lookup"><span data-stu-id="54ad1-141">Administration</span></span>
<span data-ttu-id="54ad1-142">Hello *propriétaire du circuit* est hello administrateur/coadministrator d’abonnement hello dans le hello ExpressRoute circuit est créé.</span><span class="sxs-lookup"><span data-stu-id="54ad1-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="54ad1-143">Hello propriétaire du circuit peut autoriser les administrateurs/coadministrators d’autres abonnements, tooas référencé *les utilisateurs de circuit*, toouse hello dédié circuit dont ils sont propriétaires.</span><span class="sxs-lookup"><span data-stu-id="54ad1-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="54ad1-144">Les utilisateurs de circuit peut de circuit ExpressRoute de l’organisation autorisés toouse hello lier le réseau virtuel de hello dans leur toohello abonnement circuit ExpressRoute une fois qu’ils sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="54ad1-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="54ad1-145">propriétaire du circuit Hello possède les autorisations hello power toomodify et révoquer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="54ad1-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="54ad1-146">Révocation d’une autorisation génère tous les liens en cours de suppression de l’abonnement hello dont l’accès a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="54ad1-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="54ad1-147">Opérations du propriétaire du circuit</span><span class="sxs-lookup"><span data-stu-id="54ad1-147">Circuit owner operations</span></span>

<span data-ttu-id="54ad1-148">**Création d’une autorisation**</span><span class="sxs-lookup"><span data-stu-id="54ad1-148">**Creating an authorization**</span></span>

<span data-ttu-id="54ad1-149">Hello propriétaire du circuit autorise les administrateurs de hello d’autres abonnements toouse hello spécifié circuit.</span><span class="sxs-lookup"><span data-stu-id="54ad1-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="54ad1-150">Dans l’exemple suivant de hello, administrateur hello du circuit de hello (Contoso IT) permet d’administrateur hello d’un autre toolink d’abonnement (développement de Test) de circuit de toohello tootwo réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="54ad1-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="54ad1-151">administrateur Contoso Hello permet cela en spécifiant l’ID de développement et de Test Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="54ad1-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="54ad1-152">applet de commande Hello n’envoie pas de courrier électronique toohello spécifié ID Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54ad1-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="54ad1-153">propriétaire du circuit Hello doit tooexplicitly notifier hello autre propriétaire d’abonnement qui hello d’autorisation est terminée.</span><span class="sxs-lookup"><span data-stu-id="54ad1-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="54ad1-154">**Vérification des autorisations**</span><span class="sxs-lookup"><span data-stu-id="54ad1-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="54ad1-155">propriétaire du circuit Hello peut consulter toutes les autorisations qui sont émises sur un circuit en particulier en exécutant hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="54ad1-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="54ad1-156">**Mise à jour des autorisations**</span><span class="sxs-lookup"><span data-stu-id="54ad1-156">**Updating authorizations**</span></span>

<span data-ttu-id="54ad1-157">propriétaire du circuit Hello peut modifier les autorisations à l’aide de hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="54ad1-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="54ad1-158">**Suppression des autorisations**</span><span class="sxs-lookup"><span data-stu-id="54ad1-158">**Deleting authorizations**</span></span>

<span data-ttu-id="54ad1-159">propriétaire du circuit Hello permettre révoquer/supprimer un autorisations toohello utilisateur en exécutant hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="54ad1-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="54ad1-160">Opérations de l’utilisateur du circuit</span><span class="sxs-lookup"><span data-stu-id="54ad1-160">Circuit user operations</span></span>

<span data-ttu-id="54ad1-161">**Vérification des autorisations**</span><span class="sxs-lookup"><span data-stu-id="54ad1-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="54ad1-162">utilisateur de circuit Hello peut passer en revue les autorisations à l’aide de hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="54ad1-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="54ad1-163">**Échange des autorisations de lien**</span><span class="sxs-lookup"><span data-stu-id="54ad1-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="54ad1-164">utilisateur du circuit Hello peut exécuter hello suivant l’applet de commande tooredeem une autorisation de lien :</span><span class="sxs-lookup"><span data-stu-id="54ad1-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="54ad1-165">Exécutez cette commande dans l’abonnement hello qui vient d’être liée pour le réseau virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="54ad1-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="54ad1-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54ad1-166">Next steps</span></span>
<span data-ttu-id="54ad1-167">Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="54ad1-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

