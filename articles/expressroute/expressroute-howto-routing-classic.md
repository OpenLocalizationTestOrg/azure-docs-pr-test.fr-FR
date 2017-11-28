---
title: "Configuration de l’acheminement (homologation) d’un circuit ExpressRoute - Azure Classic | Microsoft Docs"
description: "Cet article vous guide tout au long des étapes de création et d’approvisionnement de l’homologation privée, publique et Microsoft d’un circuit ExpressRoute. Cet article vous montre également comment vérifier l'état, mettre à jour ou supprimer des homologations pour votre circuit."
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
ms.openlocfilehash: 37713db70f3ae837edafc997b78b16b121d0a885
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="13840-104">Créer et modifier l’homologation pour un circuit ExpressRoute (Classic)</span><span class="sxs-lookup"><span data-stu-id="13840-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13840-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="13840-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="13840-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13840-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="13840-107">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="13840-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="13840-108">Vidéo - Homologation privée</span><span class="sxs-lookup"><span data-stu-id="13840-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="13840-109">Vidéo - Homologation publique</span><span class="sxs-lookup"><span data-stu-id="13840-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="13840-110">Vidéo - Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="13840-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="13840-111">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="13840-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="13840-112">Cet article vous guide tout au long des étapes de création et de gestion de la configuration du routage d'un circuit ExpressRoute à l'aide de PowerShell et du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="13840-112">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the classic deployment model.</span></span> <span data-ttu-id="13840-113">Les étapes ci-dessous vous montreront également comment vérifier l'état, mettre à jour ou supprimer et annuler l’approvisionnement des homologations d'un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="13840-113">The steps below will also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="13840-114">**À propos des modèles de déploiement Azure**</span><span class="sxs-lookup"><span data-stu-id="13840-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="13840-115">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="13840-115">Configuration prerequisites</span></span>
* <span data-ttu-id="13840-116">Vous devez installer la dernière version des applets de commande PowerShell Azure Service Management (SM).</span><span class="sxs-lookup"><span data-stu-id="13840-116">You will need the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="13840-117">Pour en savoir plus, voir [Prise en main des applets de commande PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="13840-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="13840-118">Veillez à consulter les pages relatives aux [conditions préalables](expressroute-prerequisites.md), à la [configuration requise pour le routage](expressroute-routing.md) et aux [flux de travail](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="13840-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="13840-119">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="13840-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="13840-120">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et faites-le activer par votre fournisseur de connectivité avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="13840-120">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="13840-121">Le circuit ExpressRoute doit être dans un état approvisionné et activé pour être en mesure d'exécuter les applets de commande décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="13840-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13840-122">Ces instructions s'appliquent uniquement aux circuits créés avec des fournisseurs de services proposant des services de connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="13840-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="13840-123">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement IPVPN, à l’image de MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="13840-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="13840-124">Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="13840-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="13840-125">Vous pouvez configurer les homologations dans l’ordre de votre choix.</span><span class="sxs-lookup"><span data-stu-id="13840-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="13840-126">Toutefois, vous devez veiller à finaliser une par une la configuration de chaque homologation.</span><span class="sxs-lookup"><span data-stu-id="13840-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>


### <a name="log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="13840-127">Connectez-vous à votre compte Azure et sélectionnez un abonnement</span><span class="sxs-lookup"><span data-stu-id="13840-127">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="13840-128">Ouvrez la console PowerShell avec des droits élevés et connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="13840-128">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="13840-129">Utilisez l’exemple suivant pour faciliter votre connexion :</span><span class="sxs-lookup"><span data-stu-id="13840-129">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="13840-130">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="13840-130">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="13840-131">Si vous avez plusieurs abonnements, sélectionnez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="13840-131">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="13840-132">Utilisez l’applet de commande suivante pour ajouter votre abonnement Azure à PowerShell pour le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="13840-132">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="13840-133">Homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="13840-133">Azure private peering</span></span>
<span data-ttu-id="13840-134">Cette section fournit des instructions sur la façon de créer, obtenir, mettre à jour et supprimer la configuration d'homologation privée Azure pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="13840-134">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="13840-135">Pour créer une homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="13840-135">To create Azure private peering</span></span>
1. <span data-ttu-id="13840-136">**Importez le module PowerShell pour ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="13840-136">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="13840-137">Vous devez importer les modules Azure et ExpressRoute dans la session PowerShell pour utiliser les applets de commande ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="13840-137">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="13840-138">Exécutez les commandes suivantes pour importer les modules Azure et ExpressRoute dans la session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13840-138">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="13840-139">**Créez un circuit ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="13840-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="13840-140">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et faites-le approvisionner par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="13840-140">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="13840-141">Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l'homologation privée Azure pour vous.</span><span class="sxs-lookup"><span data-stu-id="13840-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="13840-142">Dans ce cas, vous n'aurez pas besoin de suivre les instructions indiquées dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="13840-142">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="13840-143">Toutefois, si votre fournisseur de connectivité ne gère pas le routage pour vous, après avoir créé votre circuit, suivez les instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="13840-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span> 
3. <span data-ttu-id="13840-144">**Vérifiez que le circuit ExpressRoute est approvisionné.**</span><span class="sxs-lookup"><span data-stu-id="13840-144">**Check the ExpressRoute circuit to ensure it is provisioned.**</span></span>
   
    <span data-ttu-id="13840-145">Vous devez tout d'abord vérifier que le circuit ExpressRoute est approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="13840-145">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="13840-146">Reportez-vous à l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="13840-146">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="13840-147">Assurez-vous que le circuit affiche l’état Provisioned (approvisionné) et Enabled (activé).</span><span class="sxs-lookup"><span data-stu-id="13840-147">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="13840-148">Si ce n'est pas le cas, contactez votre fournisseur de connectivité afin que votre circuit affiche l’état requis.</span><span class="sxs-lookup"><span data-stu-id="13840-148">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="13840-149">**Configurez l'homologation privée Azure pour le circuit.**</span><span class="sxs-lookup"><span data-stu-id="13840-149">**Configure Azure private peering for the circuit.**</span></span>
   
    <span data-ttu-id="13840-150">Assurez-vous de disposer des éléments suivants avant de procéder aux étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="13840-150">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
   * <span data-ttu-id="13840-151">Un sous-réseau /30 pour le lien principal.</span><span class="sxs-lookup"><span data-stu-id="13840-151">A /30 subnet for the primary link.</span></span> <span data-ttu-id="13840-152">Ce sous-réseau ne doit faire partie d’aucun espace d'adressage réservé aux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="13840-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="13840-153">Un sous-réseau /30 pour le lien secondaire.</span><span class="sxs-lookup"><span data-stu-id="13840-153">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="13840-154">Ce sous-réseau ne doit faire partie d’aucun espace d'adressage réservé aux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="13840-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="13840-155">Un ID VLAN valide pour établir cette homologation.</span><span class="sxs-lookup"><span data-stu-id="13840-155">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="13840-156">Assurez-vous qu'aucune autre homologation sur le circuit n'utilise le même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="13840-156">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="13840-157">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="13840-157">AS number for peering.</span></span> <span data-ttu-id="13840-158">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="13840-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="13840-159">Vous pouvez utiliser un numéro AS privé pour cette homologation.</span><span class="sxs-lookup"><span data-stu-id="13840-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="13840-160">Veillez à ne pas utiliser le numéro 65515.</span><span class="sxs-lookup"><span data-stu-id="13840-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="13840-161">Un hachage MD5 si vous choisissez d’en utiliser un.</span><span class="sxs-lookup"><span data-stu-id="13840-161">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="13840-162">**Cette étape est facultative**.</span><span class="sxs-lookup"><span data-stu-id="13840-162">**This is optional**.</span></span>
     
    <span data-ttu-id="13840-163">Vous pouvez exécuter l’applet de commande suivante pour configurer l’homologation privée Azure pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="13840-163">You can run the following cmdlet to configure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="13840-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="13840-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="13840-165">Vous pouvez utiliser l'applet de commande ci-dessous si vous choisissez d'utiliser un hachage MD5.</span><span class="sxs-lookup"><span data-stu-id="13840-165">You can use the cmdlet below if you choose to use an MD5 hash.</span></span>
     
        <span data-ttu-id="13840-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="13840-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="13840-167">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="13840-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="13840-168">Pour afficher les détails d’une homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="13840-168">To view Azure private peering details</span></span>
<span data-ttu-id="13840-169">Vous pouvez obtenir les détails de la configuration à l'aide de l'applet de commande suivante</span><span class="sxs-lookup"><span data-stu-id="13840-169">You can get configuration details using the following cmdlet</span></span>

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


### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="13840-170">Pour mettre à jour la configuration d'homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="13840-170">To update Azure private peering configuration</span></span>
<span data-ttu-id="13840-171">Vous pouvez mettre à jour toute partie de la configuration à l'aide de l’applet de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="13840-171">You can update any part of the configuration using the following cmdlet.</span></span> <span data-ttu-id="13840-172">Dans l'exemple ci-dessous, l'ID VLAN du circuit est mis à jour de 100 à 500.</span><span class="sxs-lookup"><span data-stu-id="13840-172">In the example below, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="13840-173">Pour supprimer une homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="13840-173">To delete Azure private peering</span></span>
<span data-ttu-id="13840-174">Vous pouvez supprimer votre configuration d’homologation en exécutant l’applet de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="13840-174">You can remove your peering configuration by running the following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="13840-175">Vous devez vous assurer que tous les réseaux virtuels sont dissociés du circuit ExpressRoute avant d'exécuter cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="13840-175">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="13840-176">Homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="13840-176">Azure public peering</span></span>
<span data-ttu-id="13840-177">Cette section fournit des instructions sur la façon de créer, obtenir, mettre à jour et supprimer la configuration d'homologation publique Azure pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="13840-177">This section provides instructions on how to create, get, update and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="13840-178">Pour créer une homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="13840-178">To create Azure public peering</span></span>
1. <span data-ttu-id="13840-179">**Importez le module PowerShell pour ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="13840-179">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="13840-180">Vous devez importer les modules Azure et ExpressRoute dans la session PowerShell pour utiliser les applets de commande ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="13840-180">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="13840-181">Exécutez les commandes suivantes pour importer les modules Azure et ExpressRoute dans la session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13840-181">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="13840-182">**Création d’un circuit ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="13840-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="13840-183">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et faites-le approvisionner par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="13840-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="13840-184">Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l'homologation privée Azure pour vous.</span><span class="sxs-lookup"><span data-stu-id="13840-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="13840-185">Dans ce cas, vous n'aurez pas besoin de suivre les instructions indiquées dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="13840-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="13840-186">Toutefois, si votre fournisseur de connectivité ne gère pas le routage pour vous, après avoir créé votre circuit, suivez les instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="13840-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="13840-187">**Vérification de l’approvisionnement du circuit ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="13840-187">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="13840-188">Vous devez tout d'abord vérifier que le circuit ExpressRoute est approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="13840-188">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="13840-189">Reportez-vous à l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="13840-189">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="13840-190">Assurez-vous que le circuit affiche l’état Provisioned (approvisionné) et Enabled (activé).</span><span class="sxs-lookup"><span data-stu-id="13840-190">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="13840-191">Si ce n'est pas le cas, contactez votre fournisseur de connectivité afin que votre circuit affiche l’état requis.</span><span class="sxs-lookup"><span data-stu-id="13840-191">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="13840-192">**Configuration de l'homologation publique Azure pour le circuit**</span><span class="sxs-lookup"><span data-stu-id="13840-192">**Configure Azure public peering for the circuit**</span></span>
   
    <span data-ttu-id="13840-193">Assurez-vous de disposer des informations suivantes avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="13840-193">Ensure that you have the following information before you proceed further.</span></span>
   
   * <span data-ttu-id="13840-194">Un sous-réseau /30 pour le lien principal.</span><span class="sxs-lookup"><span data-stu-id="13840-194">A /30 subnet for the primary link.</span></span> <span data-ttu-id="13840-195">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="13840-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="13840-196">Un sous-réseau /30 pour le lien secondaire.</span><span class="sxs-lookup"><span data-stu-id="13840-196">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="13840-197">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="13840-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="13840-198">Un ID VLAN valide pour établir cette homologation.</span><span class="sxs-lookup"><span data-stu-id="13840-198">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="13840-199">Assurez-vous qu'aucune autre homologation sur le circuit n'utilise le même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="13840-199">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="13840-200">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="13840-200">AS number for peering.</span></span> <span data-ttu-id="13840-201">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="13840-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="13840-202">Un hachage MD5 si vous choisissez d’en utiliser un.</span><span class="sxs-lookup"><span data-stu-id="13840-202">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="13840-203">**Cette étape est facultative**.</span><span class="sxs-lookup"><span data-stu-id="13840-203">**This is optional**.</span></span>
     
    <span data-ttu-id="13840-204">Vous pouvez exécuter l’applet de commande suivante pour configurer l’homologation publique Azure pour votre circuit</span><span class="sxs-lookup"><span data-stu-id="13840-204">You can run the following cmdlet to configure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="13840-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="13840-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="13840-206">Vous pouvez utiliser l'applet de commande ci-dessous si vous choisissez d'utiliser un hachage MD5</span><span class="sxs-lookup"><span data-stu-id="13840-206">You can use the cmdlet below if you choose to use an MD5 hash</span></span>
     
        <span data-ttu-id="13840-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="13840-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="13840-208">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="13840-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="13840-209">Pour afficher les détails d’une homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="13840-209">To view Azure public peering details</span></span>
<span data-ttu-id="13840-210">Vous pouvez obtenir les détails de la configuration à l'aide de l'applet de commande suivante</span><span class="sxs-lookup"><span data-stu-id="13840-210">You can get configuration details using the following cmdlet</span></span>

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


### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="13840-211">Pour mettre à jour la configuration d'homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="13840-211">To update Azure public peering configuration</span></span>
<span data-ttu-id="13840-212">Vous pouvez mettre à jour toute partie de la configuration à l'aide de l’applet de commande suivante</span><span class="sxs-lookup"><span data-stu-id="13840-212">You can update any part of the configuration using the following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="13840-213">L'ID VLAN du circuit est mis à jour de 200 à 600 dans l’exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="13840-213">The VLAN ID of the circuit is being updated from 200 to 600 in the above example.</span></span>

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="13840-214">Pour supprimer une homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="13840-214">To delete Azure public peering</span></span>
<span data-ttu-id="13840-215">Vous pouvez supprimer votre configuration d’homologation en exécutant l’applet de commande suivante</span><span class="sxs-lookup"><span data-stu-id="13840-215">You can remove your peering configuration by running the following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="13840-216">Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="13840-216">Microsoft peering</span></span>
<span data-ttu-id="13840-217">Cette section fournit des instructions sur la façon de créer, obtenir, mettre à jour et supprimer la configuration d'homologation Microsoft pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="13840-217">This section provides instructions on how to create, get, update and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="13840-218">Pour créer une homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="13840-218">To create Microsoft peering</span></span>
1. <span data-ttu-id="13840-219">**Importez le module PowerShell pour ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="13840-219">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="13840-220">Vous devez importer les modules Azure et ExpressRoute dans la session PowerShell pour utiliser les applets de commande ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="13840-220">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="13840-221">Exécutez les commandes suivantes pour importer les modules Azure et ExpressRoute dans la session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13840-221">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="13840-222">**Création d’un circuit ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="13840-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="13840-223">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et faites-le approvisionner par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="13840-223">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="13840-224">Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l'homologation privée Azure pour vous.</span><span class="sxs-lookup"><span data-stu-id="13840-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="13840-225">Dans ce cas, vous n'aurez pas besoin de suivre les instructions indiquées dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="13840-225">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="13840-226">Toutefois, si votre fournisseur de connectivité ne gère pas le routage pour vous, après avoir créé votre circuit, suivez les instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="13840-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="13840-227">**Vérification de l’approvisionnement du circuit ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="13840-227">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="13840-228">Vous devez tout d'abord vérifier que le circuit ExpressRoute est approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="13840-228">You must first check to see if the ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="13840-229">Assurez-vous que le circuit affiche l’état Provisioned (approvisionné) et Enabled (activé).</span><span class="sxs-lookup"><span data-stu-id="13840-229">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="13840-230">Si ce n'est pas le cas, contactez votre fournisseur de connectivité afin que votre circuit affiche l’état requis.</span><span class="sxs-lookup"><span data-stu-id="13840-230">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="13840-231">**Configuration de l'homologation Microsoft pour le circuit**</span><span class="sxs-lookup"><span data-stu-id="13840-231">**Configure Microsoft peering for the circuit**</span></span>
   
    <span data-ttu-id="13840-232">Assurez-vous de disposer des informations suivantes avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="13840-232">Make sure that you have the following information before you proceed.</span></span>
   
   * <span data-ttu-id="13840-233">Un sous-réseau /30 pour le lien principal.</span><span class="sxs-lookup"><span data-stu-id="13840-233">A /30 subnet for the primary link.</span></span> <span data-ttu-id="13840-234">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="13840-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="13840-235">Un sous-réseau /30 pour le lien secondaire.</span><span class="sxs-lookup"><span data-stu-id="13840-235">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="13840-236">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="13840-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="13840-237">Un ID VLAN valide pour établir cette homologation.</span><span class="sxs-lookup"><span data-stu-id="13840-237">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="13840-238">Assurez-vous qu'aucune autre homologation sur le circuit n'utilise le même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="13840-238">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="13840-239">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="13840-239">AS number for peering.</span></span> <span data-ttu-id="13840-240">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="13840-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="13840-241">Préfixes publiés : vous devez fournir une liste de tous les préfixes que vous prévoyez de publier sur la session BGP.</span><span class="sxs-lookup"><span data-stu-id="13840-241">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="13840-242">Seuls les préfixes d'adresses IP publiques sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="13840-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="13840-243">Vous pouvez envoyer une liste séparée par des virgules si vous prévoyez d'envoyer un jeu de préfixes.</span><span class="sxs-lookup"><span data-stu-id="13840-243">You can send a comma separated list if you plan to send a set of prefixes.</span></span> <span data-ttu-id="13840-244">Ces préfixes doivent être enregistrés en votre nom dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="13840-244">These prefixes must be registered to you in an RIR / IRR.</span></span>
   * <span data-ttu-id="13840-245">ASN client : si vous publiez des préfixes non enregistrés dans le numéro AS d’homologation, vous pouvez spécifier le numéro AS avec lequel ils sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="13840-245">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span> <span data-ttu-id="13840-246">**Cette étape est facultative**.</span><span class="sxs-lookup"><span data-stu-id="13840-246">**This is optional**.</span></span>
   * <span data-ttu-id="13840-247">Nom du registre de routage : vous pouvez spécifier les registres RIR/IRR par rapport auxquels le numéro AS et les préfixes sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="13840-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="13840-248">Un hachage MD5 si vous choisissez d’en utiliser un.</span><span class="sxs-lookup"><span data-stu-id="13840-248">An MD5 hash, if you choose to use one.</span></span> <span data-ttu-id="13840-249">**Cette étape est facultative.**</span><span class="sxs-lookup"><span data-stu-id="13840-249">**This is optional.**</span></span>
     
    <span data-ttu-id="13840-250">Vous pouvez exécuter l'applet de commande suivante afin de configurer l’homologation Microsoft pour votre circuit</span><span class="sxs-lookup"><span data-stu-id="13840-250">You can run the following cmdlet to configure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="13840-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="13840-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="13840-252">Pour afficher les détails de l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="13840-252">To view Microsoft peering details</span></span>
<span data-ttu-id="13840-253">Vous pouvez obtenir les détails de la configuration à l'aide de l'applet de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="13840-253">You can get configuration details using the following cmdlet.</span></span>

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


### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="13840-254">Pour mettre à jour la configuration d’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="13840-254">To update Microsoft peering configuration</span></span>
<span data-ttu-id="13840-255">Vous pouvez mettre à jour toute partie de la configuration à l'aide de l’applet de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="13840-255">You can update any part of the configuration using the following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="13840-256">Pour supprimer une homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="13840-256">To delete Microsoft peering</span></span>
<span data-ttu-id="13840-257">Vous pouvez supprimer votre configuration d’homologation en exécutant l’applet de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="13840-257">You can remove your peering configuration by running the following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="13840-258">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13840-258">Next steps</span></span>
<span data-ttu-id="13840-259">Ensuite, [liez un réseau virtuel à un circuit ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="13840-259">Next, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="13840-260">Pour plus d'informations sur les workflows, consultez [Workflows ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="13840-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="13840-261">Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="13840-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

