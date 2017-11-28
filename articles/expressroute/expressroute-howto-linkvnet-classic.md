---
title: "Lier un réseau virtuel à un circuit ExpressRoute avec PowerShell et le portail Azure Classic | Microsoft Docs"
description: "Ce document explique comment lier des réseaux virtuels à des circuits ExpressRoute à l’aide du modèle de déploiement classique et de PowerShell."
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
ms.openlocfilehash: 8df8a4c6ff0897c821e13248e0494b17e1a4992d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="4f6c5-103">Connectez un réseau virtuel à un circuit ExpressRoute à l’aide de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="4f6c5-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f6c5-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4f6c5-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="4f6c5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f6c5-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="4f6c5-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4f6c5-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="4f6c5-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="4f6c5-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="4f6c5-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="4f6c5-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="4f6c5-109">Cet article vous aide à lier des réseaux virtuels à des circuits Azure ExpressRoute à l’aide du modèle de déploiement classique et de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-109">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits by using the classic deployment model and PowerShell.</span></span> <span data-ttu-id="4f6c5-110">Les réseaux virtuels peuvent appartenir au même abonnement ou faire partie d’un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-110">Virtual networks can either be in the same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="4f6c5-111">**À propos des modèles de déploiement Azure**</span><span class="sxs-lookup"><span data-stu-id="4f6c5-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="4f6c5-112">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="4f6c5-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="4f6c5-113">Vous devez utiliser la dernière version des modules Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-113">You need the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="4f6c5-114">Vous pouvez télécharger les modules PowerShell les plus récents à partir de la section PowerShell de la [page des téléchargements Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4f6c5-114">You can download the latest PowerShell modules from the PowerShell section of the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="4f6c5-115">Suivez les instructions de [Comment installer et configurer Azure PowerShell](/powershell/azure/overview) pour des étapes pas à pas permettant de configurer votre ordinateur pour l’utilisation des modules Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-115">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>
2. <span data-ttu-id="4f6c5-116">Avant de commencer la configuration, vous devez examiner les [conditions préalables](expressroute-prerequisites.md), la [configuration requise pour le routage](expressroute-routing.md) et les [flux de travail](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="4f6c5-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="4f6c5-117">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="4f6c5-118">Suivez les instructions pour [créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et faites-le activer par votre fournisseur de service de connectivité.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-118">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span></span>
   * <span data-ttu-id="4f6c5-119">Vérifiez que l’homologation privée Azure est configurée pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="4f6c5-120">Pour obtenir des instructions sur le routage, consultez l’article [Configurer le routage](expressroute-howto-routing-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="4f6c5-120">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="4f6c5-121">Vérifiez que l’homologation privée Azure est être configurée, et que l’homologation BGP entre votre réseau et Microsoft est être opérationnelle pour pouvoir activer la connectivité de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-121">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="4f6c5-122">Vous devez disposer d'un réseau virtuel et d’une passerelle de réseau virtuel créés et totalement approvisionnés.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="4f6c5-123">Suivez les instructions pour [configurer un réseau virtuel pour ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="4f6c5-123">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="4f6c5-124">Vous pouvez lier jusqu’à 10 réseaux virtuels à un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-124">You can link up to 10 virtual networks to an ExpressRoute circuit.</span></span> <span data-ttu-id="4f6c5-125">Tous les réseaux virtuels doivent être situés dans la même région géopolitique.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-125">All virtual networks must be in the same geopolitical region.</span></span> <span data-ttu-id="4f6c5-126">Si vous avez activé le module complémentaire Premium d’ExpressRoute, vous pouvez lier un plus grand nombre de réseaux virtuels à votre circuit ExpressRoute ou des réseaux virtuels situés dans d’autres régions géopolitiques.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-126">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="4f6c5-127">Pour plus d’informations sur le module complémentaire Premium, consultez le [FAQ](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="4f6c5-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="4f6c5-128">Connecter un réseau virtuel du même abonnement à un circuit</span><span class="sxs-lookup"><span data-stu-id="4f6c5-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="4f6c5-129">Vous pouvez lier un réseau virtuel à un circuit ExpressRoute à l’aide de l’applet de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-129">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="4f6c5-130">Assurez-vous que la passerelle de réseau virtuel est créée et prête pour la liaison avant d’exécuter l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="4f6c5-131">Connecter un réseau virtuel d’un autre abonnement à un circuit</span><span class="sxs-lookup"><span data-stu-id="4f6c5-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="4f6c5-132">Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="4f6c5-133">La figure suivante montre un schéma simple sur le fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="4f6c5-134">Chacun des petits clouds dans le cloud principal est utilisé pour représenter les abonnements appartenant à différents services au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="4f6c5-135">Chacun des services au sein de l’organisation peut utiliser son propre abonnement pour déployer ses services, mais ils peuvent partager un même circuit ExpressRoute pour se connecter à votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-135">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="4f6c5-136">Un seul service (dans cet exemple, le service informatique) peut posséder le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="4f6c5-137">D’autres abonnements au sein de l’organisation peuvent utiliser le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="4f6c5-138">Les frais de connectivité et de bande passante pour le circuit dédié s’appliquent au propriétaire du circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-138">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="4f6c5-139">Tous les réseaux virtuels partagent la même bande passante.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="4f6c5-141">Administration</span><span class="sxs-lookup"><span data-stu-id="4f6c5-141">Administration</span></span>
<span data-ttu-id="4f6c5-142">Le *propriétaire du circuit* est l’administrateur/coadministrateur de l’abonnement dans lequel le circuit ExpressRoute est créé.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-142">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span></span> <span data-ttu-id="4f6c5-143">Le propriétaire du circuit peut autoriser les administrateurs/coadministrateurs d’autres abonnements (appelés *utilisateurs du circuit*) à utiliser le circuit dédié dont ils sont propriétaires.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-143">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span></span> <span data-ttu-id="4f6c5-144">Une fois autorisés, les utilisateurs du circuit peuvent lier le réseau virtuel dans leur abonnement au circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-144">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="4f6c5-145">Le propriétaire du circuit a le pouvoir de modifier et de révoquer les autorisations à tout moment.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-145">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="4f6c5-146">La révocation d’une autorisation entraîne la suppression de tous les liens de l’abonnement dont l’accès a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-146">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="4f6c5-147">Opérations du propriétaire du circuit</span><span class="sxs-lookup"><span data-stu-id="4f6c5-147">Circuit owner operations</span></span>

<span data-ttu-id="4f6c5-148">**Création d’une autorisation**</span><span class="sxs-lookup"><span data-stu-id="4f6c5-148">**Creating an authorization**</span></span>

<span data-ttu-id="4f6c5-149">Le propriétaire du circuit autorise les administrateurs d’autres abonnements à utiliser le circuit spécifié.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-149">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span></span> <span data-ttu-id="4f6c5-150">Dans l’exemple ci-dessous, l’administrateur du circuit (Service informatique de Contoso) permet à l’administrateur d’un autre abonnement (Dev-Test) de lier jusqu’à deux réseaux virtuels au circuit.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-150">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span></span> <span data-ttu-id="4f6c5-151">Le service informatique de Contoso le permet en spécifiant l’ID Microsoft de Dev-Test.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-151">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span></span> <span data-ttu-id="4f6c5-152">L'applet de commande n'envoie pas de courrier électronique à l’ID Microsoft spécifié.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-152">The cmdlet doesn't send email to the specified Microsoft ID.</span></span> <span data-ttu-id="4f6c5-153">Le propriétaire du circuit doit notifier explicitement au propriétaire de l’autre abonnement que l’autorisation a pris fin.</span><span class="sxs-lookup"><span data-stu-id="4f6c5-153">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="4f6c5-154">**Vérification des autorisations**</span><span class="sxs-lookup"><span data-stu-id="4f6c5-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="4f6c5-155">Le propriétaire du circuit peut vérifier toutes les autorisations émises sur un circuit donné en exécutant l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4f6c5-155">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

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


<span data-ttu-id="4f6c5-156">**Mise à jour des autorisations**</span><span class="sxs-lookup"><span data-stu-id="4f6c5-156">**Updating authorizations**</span></span>

<span data-ttu-id="4f6c5-157">Le propriétaire du circuit peut modifier les autorisations à l’aide de l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4f6c5-157">The circuit owner can modify authorizations by using the following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="4f6c5-158">**Suppression des autorisations**</span><span class="sxs-lookup"><span data-stu-id="4f6c5-158">**Deleting authorizations**</span></span>

<span data-ttu-id="4f6c5-159">Le propriétaire du circuit peut révoquer/supprimer les autorisations accordées à l’utilisateur en exécutant l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4f6c5-159">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="4f6c5-160">Opérations de l’utilisateur du circuit</span><span class="sxs-lookup"><span data-stu-id="4f6c5-160">Circuit user operations</span></span>

<span data-ttu-id="4f6c5-161">**Vérification des autorisations**</span><span class="sxs-lookup"><span data-stu-id="4f6c5-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="4f6c5-162">L’utilisateur du circuit peut vérifier les autorisations à l’aide de l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4f6c5-162">The circuit user can review authorizations by using the following cmdlet:</span></span>

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

<span data-ttu-id="4f6c5-163">**Échange des autorisations de lien**</span><span class="sxs-lookup"><span data-stu-id="4f6c5-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="4f6c5-164">L’utilisateur du circuit peut exécuter l’applet de commande suivante pour échanger une autorisation de lien :</span><span class="sxs-lookup"><span data-stu-id="4f6c5-164">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="4f6c5-165">Exécutez cette commande dans l’abonnement qui vient d’être lié pour le réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="4f6c5-165">Run this command in the newly linked subscription for the virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="4f6c5-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4f6c5-166">Next steps</span></span>
<span data-ttu-id="4f6c5-167">Pour plus d'informations sur ExpressRoute, consultez le [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="4f6c5-167">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

