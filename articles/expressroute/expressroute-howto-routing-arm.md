---
title: "Configuration de l’acheminement (homologation) d’un circuit ExpressRoute - Resource Manager, PowerShell et Azure | Microsoft Docs"
description: "Cet article vous guide tout au long des étapes de création et d’approvisionnement de l’homologation privée, publique et Microsoft d’un circuit ExpressRoute. Cet article vous montre également comment vérifier l'état, mettre à jour ou supprimer des homologations pour votre circuit."
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
ms.openlocfilehash: af68955b78239832e413e1b59e033d7d3da8d599
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="6b271-104">Créer et modifier l’homologation d’un circuit ExpressRoute à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b271-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="6b271-105">Cet article explique comment créer et gérer la configuration du routage d’un circuit ExpressRoute dans le modèle de déploiement Resource Manager à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b271-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="6b271-106">Vous pouvez également mettre à jour, supprimer et déprovisionner des homologations d’un circuit ExpressRoute, ainsi qu’en vérifier l’état.</span><span class="sxs-lookup"><span data-stu-id="6b271-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="6b271-107">Si vous souhaitez utiliser une autre méthode pour votre circuit, sélectionnez un article dans la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="6b271-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b271-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="6b271-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b271-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="6b271-110">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="6b271-111">Vidéo - Homologation privée</span><span class="sxs-lookup"><span data-stu-id="6b271-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="6b271-112">Vidéo - Homologation publique</span><span class="sxs-lookup"><span data-stu-id="6b271-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="6b271-113">Vidéo - Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="6b271-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="6b271-114">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="6b271-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="6b271-115">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="6b271-115">Configuration prerequisites</span></span>

* <span data-ttu-id="6b271-116">Installez la dernière version des applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b271-116">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="6b271-117">Pour plus d’informations, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6b271-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="6b271-118">Veillez à consulter les pages relatives aux [conditions préalables](expressroute-prerequisites.md), à la [configuration requise pour le routage](expressroute-routing.md) et aux [flux de travail](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="6b271-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="6b271-119">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="6b271-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="6b271-120">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et faites-le activer par votre fournisseur de connectivité avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="6b271-120">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="6b271-121">Pour que vous puissiez exécuter les applets de commande décrites dans cet article, le circuit ExpressRoute doit être dans un état approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="6b271-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in this article.</span></span>

<span data-ttu-id="6b271-122">Ces instructions s'appliquent uniquement aux circuits créés avec des fournisseurs de services proposant des services de connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="6b271-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="6b271-123">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="6b271-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b271-124">Nous n'annonçons pas d’homologations configurées par les fournisseurs de services via le portail de gestion des services.</span><span class="sxs-lookup"><span data-stu-id="6b271-124">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="6b271-125">Nous travaillons sur la prochaine activation de cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6b271-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="6b271-126">Contactez votre fournisseur de services avant de configurer des homologations BGP.</span><span class="sxs-lookup"><span data-stu-id="6b271-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="6b271-127">Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="6b271-128">Vous pouvez configurer les homologations dans l’ordre de votre choix.</span><span class="sxs-lookup"><span data-stu-id="6b271-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="6b271-129">Toutefois, vous devez veiller à finaliser une par une la configuration de chaque homologation.</span><span class="sxs-lookup"><span data-stu-id="6b271-129">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="6b271-130">Homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-130">Azure private peering</span></span>

<span data-ttu-id="6b271-131">Cette section explique comment créer, obtenir, mettre à jour et supprimer la configuration d’homologation privée Azure pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-131">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="6b271-132">Pour créer une homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-132">To create Azure private peering</span></span>

1. <span data-ttu-id="6b271-133">Importez le module PowerShell pour ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-133">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="6b271-134">Vous devez installer la dernière version du programme d'installation PowerShell à partir de [PowerShell Gallery](http://www.powershellgallery.com/) et importer les modules Azure Resource Manager dans la session PowerShell pour utiliser les applets de commande ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-134">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="6b271-135">Vous devrez exécuter PowerShell en tant qu'administrateur.</span><span class="sxs-lookup"><span data-stu-id="6b271-135">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="6b271-136">Importez tous les modules AzureRM.* dans la plage de version sémantique connue.</span><span class="sxs-lookup"><span data-stu-id="6b271-136">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="6b271-137">Vous pouvez également importer un seul module sélectionné dans la plage de version sémantique connue.</span><span class="sxs-lookup"><span data-stu-id="6b271-137">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="6b271-138">Connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="6b271-138">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="6b271-139">Sélectionnez l’abonnement pour lequel vous souhaitez créer le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-139">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="6b271-140">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="6b271-141">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et faites-le approvisionner par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="6b271-141">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="6b271-142">Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l'homologation privée Azure pour vous.</span><span class="sxs-lookup"><span data-stu-id="6b271-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="6b271-143">Dans ce cas, vous n'aurez pas besoin de suivre les instructions indiquées dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="6b271-143">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="6b271-144">Toutefois, si votre fournisseur de connectivité ne gère pas le routage pour vous, après avoir créé votre circuit, continuez la configuration à l’aide de la procédure qui suit.</span><span class="sxs-lookup"><span data-stu-id="6b271-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="6b271-145">Vérifiez que le circuit ExpressRoute est approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="6b271-145">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="6b271-146">Consultez l’exemple qui suit :</span><span class="sxs-lookup"><span data-stu-id="6b271-146">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="6b271-147">La réponse ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="6b271-147">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="6b271-148">Configurez l'homologation privée Azure pour le circuit.</span><span class="sxs-lookup"><span data-stu-id="6b271-148">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="6b271-149">Assurez-vous de disposer des éléments suivants avant de procéder aux étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6b271-149">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="6b271-150">Un sous-réseau /30 pour le lien principal.</span><span class="sxs-lookup"><span data-stu-id="6b271-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="6b271-151">Le sous-réseau ne doit faire partie d’aucun espace d’adressage réservé aux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="6b271-151">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="6b271-152">Un sous-réseau /30 pour le lien secondaire.</span><span class="sxs-lookup"><span data-stu-id="6b271-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="6b271-153">Le sous-réseau ne doit faire partie d’aucun espace d’adressage réservé aux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="6b271-153">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="6b271-154">Un ID VLAN valide pour établir cette homologation.</span><span class="sxs-lookup"><span data-stu-id="6b271-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="6b271-155">Assurez-vous qu'aucune autre homologation sur le circuit n'utilise le même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="6b271-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="6b271-156">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="6b271-156">AS number for peering.</span></span> <span data-ttu-id="6b271-157">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="6b271-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="6b271-158">Vous pouvez utiliser un numéro AS privé pour cette homologation.</span><span class="sxs-lookup"><span data-stu-id="6b271-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="6b271-159">Veillez à ne pas utiliser le numéro 65515.</span><span class="sxs-lookup"><span data-stu-id="6b271-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="6b271-160">**(Facultatif)** Un hachage MD5 si vous choisissez d’en utiliser un.</span><span class="sxs-lookup"><span data-stu-id="6b271-160">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="6b271-161">Utilisez l’exemple suivant pour configurer l’homologation privée Azure pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="6b271-161">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="6b271-162">Si vous choisissez d’utiliser un hachage MD5, exécutez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b271-162">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="6b271-163">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="6b271-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="6b271-164">Pour afficher les détails d’une homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-164">To view Azure private peering details</span></span>

<span data-ttu-id="6b271-165">Vous pouvez obtenir les détails de la configuration à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b271-165">You can get configuration details by using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="6b271-166">Pour mettre à jour la configuration d'homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-166">To update Azure private peering configuration</span></span>

<span data-ttu-id="6b271-167">Vous pouvez mettre à jour toute partie de la configuration à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b271-167">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="6b271-168">Dans cet exemple, l’ID VLAN du circuit est mis à jour de 100 à 500.</span><span class="sxs-lookup"><span data-stu-id="6b271-168">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="6b271-169">Pour supprimer une homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-169">To delete Azure private peering</span></span>

<span data-ttu-id="6b271-170">Vous pouvez supprimer votre configuration d’homologation en exécutant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b271-170">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="6b271-171">Vous devez vous assurer que tous les réseaux virtuels sont dissociés du circuit ExpressRoute avant d’exécuter cet exemple.</span><span class="sxs-lookup"><span data-stu-id="6b271-171">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="6b271-172">Homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-172">Azure public peering</span></span>

<span data-ttu-id="6b271-173">Cette section explique comment créer, obtenir, mettre à jour et supprimer la configuration d’homologation publique Azure pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-173">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="6b271-174">Pour créer une homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-174">To create Azure public peering</span></span>

1. <span data-ttu-id="6b271-175">Importez le module PowerShell pour ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-175">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="6b271-176">Vous devez installer la dernière version du programme d'installation PowerShell à partir de [PowerShell Gallery](http://www.powershellgallery.com/) et importer les modules Azure Resource Manager dans la session PowerShell pour utiliser les applets de commande ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-176">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="6b271-177">Vous devrez exécuter PowerShell en tant qu'administrateur.</span><span class="sxs-lookup"><span data-stu-id="6b271-177">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="6b271-178">Importez tous les modules AzureRM.* dans la plage de version sémantique connue.</span><span class="sxs-lookup"><span data-stu-id="6b271-178">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="6b271-179">Vous pouvez également importer un seul module sélectionné dans la plage de version sémantique connue.</span><span class="sxs-lookup"><span data-stu-id="6b271-179">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="6b271-180">Connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="6b271-180">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="6b271-181">Sélectionnez l’abonnement pour lequel vous souhaitez créer le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-181">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="6b271-182">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="6b271-183">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et faites-le approvisionner par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="6b271-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="6b271-184">Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l'homologation privée Azure pour vous.</span><span class="sxs-lookup"><span data-stu-id="6b271-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="6b271-185">Dans ce cas, vous n'aurez pas besoin de suivre les instructions indiquées dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="6b271-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="6b271-186">Toutefois, si votre fournisseur de connectivité ne gère pas le routage pour vous, après avoir créé votre circuit, continuez la configuration à l’aide de la procédure qui suit.</span><span class="sxs-lookup"><span data-stu-id="6b271-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="6b271-187">Vérifiez que le circuit ExpressRoute est approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="6b271-187">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="6b271-188">Consultez l’exemple qui suit :</span><span class="sxs-lookup"><span data-stu-id="6b271-188">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="6b271-189">La réponse ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="6b271-189">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="6b271-190">Configurez l’homologation publique Azure pour le circuit.</span><span class="sxs-lookup"><span data-stu-id="6b271-190">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="6b271-191">Assurez-vous que vous disposez des informations suivantes avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="6b271-191">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="6b271-192">Un sous-réseau /30 pour le lien principal.</span><span class="sxs-lookup"><span data-stu-id="6b271-192">A /30 subnet for the primary link.</span></span> <span data-ttu-id="6b271-193">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="6b271-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="6b271-194">Un sous-réseau /30 pour le lien secondaire.</span><span class="sxs-lookup"><span data-stu-id="6b271-194">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="6b271-195">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="6b271-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="6b271-196">Un ID VLAN valide pour établir cette homologation.</span><span class="sxs-lookup"><span data-stu-id="6b271-196">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="6b271-197">Assurez-vous qu'aucune autre homologation sur le circuit n'utilise le même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="6b271-197">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="6b271-198">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="6b271-198">AS number for peering.</span></span> <span data-ttu-id="6b271-199">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="6b271-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="6b271-200">**Facultatif :** un hachage MD5 si vous choisissez d’en utiliser un.</span><span class="sxs-lookup"><span data-stu-id="6b271-200">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="6b271-201">Exécutez l’exemple suivant pour configurer l’homologation publique Azure pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="6b271-201">Run the following example to configure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="6b271-202">Si vous choisissez d’utiliser un hachage MD5, utilisez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b271-202">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="6b271-203">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="6b271-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="6b271-204">Pour afficher les détails d’une homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-204">To view Azure public peering details</span></span>

<span data-ttu-id="6b271-205">Vous pouvez obtenir des détails sur la configuration à l’aide de l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6b271-205">You can get configuration details using the following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="6b271-206">Pour mettre à jour la configuration d'homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-206">To update Azure public peering configuration</span></span>

<span data-ttu-id="6b271-207">Vous pouvez mettre à jour toute partie de la configuration à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b271-207">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="6b271-208">Dans cet exemple, l’ID VLAN du circuit est mis à jour de 200 à 600.</span><span class="sxs-lookup"><span data-stu-id="6b271-208">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="6b271-209">Pour supprimer une homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="6b271-209">To delete Azure public peering</span></span>

<span data-ttu-id="6b271-210">Vous pouvez supprimer votre configuration d’homologation en exécutant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b271-210">You can remove your peering configuration by running the following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="6b271-211">Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="6b271-211">Microsoft peering</span></span>

<span data-ttu-id="6b271-212">Cette section explique comment créer, obtenir, mettre à jour et supprimer la configuration d’homologation Microsoft pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-212">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b271-213">L’homologation Microsoft des circuits ExpressRoute qui ont été configurés avant le 1er août 2017 entraînera la publication de tous les préfixes de service via l’homologation Microsoft, même si aucun filtre d’itinéraire n’est défini.</span><span class="sxs-lookup"><span data-stu-id="6b271-213">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="6b271-214">L’homologation Microsoft des circuits ExpressRoute qui sont configurés le 1er août 2017 ou après n’entraînera la publication d’aucun préfixe tant qu’un filtre de routage n’aura pas été attaché au circuit.</span><span class="sxs-lookup"><span data-stu-id="6b271-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="6b271-215">Pour plus d’informations, consultez [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurer un filtre d’itinéraire pour l’homologation Microsoft).</span><span class="sxs-lookup"><span data-stu-id="6b271-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="6b271-216">Pour créer une homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="6b271-216">To create Microsoft peering</span></span>

1. <span data-ttu-id="6b271-217">Importez le module PowerShell pour ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-217">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="6b271-218">Vous devez installer la dernière version du programme d'installation PowerShell à partir de [PowerShell Gallery](http://www.powershellgallery.com/) et importer les modules Azure Resource Manager dans la session PowerShell pour utiliser les applets de commande ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-218">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="6b271-219">Vous devrez exécuter PowerShell en tant qu'administrateur.</span><span class="sxs-lookup"><span data-stu-id="6b271-219">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="6b271-220">Importez tous les modules AzureRM.* dans la plage de version sémantique connue.</span><span class="sxs-lookup"><span data-stu-id="6b271-220">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="6b271-221">Vous pouvez également importer un seul module sélectionné dans la plage de version sémantique connue.</span><span class="sxs-lookup"><span data-stu-id="6b271-221">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="6b271-222">Connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="6b271-222">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="6b271-223">Sélectionnez l’abonnement pour lequel vous souhaitez créer le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-223">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="6b271-224">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b271-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="6b271-225">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et faites-le approvisionner par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="6b271-225">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="6b271-226">Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l'homologation privée Azure pour vous.</span><span class="sxs-lookup"><span data-stu-id="6b271-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="6b271-227">Dans ce cas, vous n'aurez pas besoin de suivre les instructions indiquées dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="6b271-227">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="6b271-228">Toutefois, si votre fournisseur de connectivité ne gère pas le routage pour vous, après avoir créé votre circuit, continuez la configuration à l’aide de la procédure qui suit.</span><span class="sxs-lookup"><span data-stu-id="6b271-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="6b271-229">Vérifiez que le circuit ExpressRoute est approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="6b271-229">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="6b271-230">Consultez l’exemple qui suit :</span><span class="sxs-lookup"><span data-stu-id="6b271-230">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="6b271-231">La réponse ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="6b271-231">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="6b271-232">Configurez l’homologation Microsoft pour le circuit.</span><span class="sxs-lookup"><span data-stu-id="6b271-232">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="6b271-233">Assurez-vous de disposer des informations suivantes avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="6b271-233">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="6b271-234">Un sous-réseau /30 pour le lien principal.</span><span class="sxs-lookup"><span data-stu-id="6b271-234">A /30 subnet for the primary link.</span></span> <span data-ttu-id="6b271-235">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="6b271-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="6b271-236">Un sous-réseau /30 pour le lien secondaire.</span><span class="sxs-lookup"><span data-stu-id="6b271-236">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="6b271-237">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="6b271-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="6b271-238">Un ID VLAN valide pour établir cette homologation.</span><span class="sxs-lookup"><span data-stu-id="6b271-238">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="6b271-239">Assurez-vous qu'aucune autre homologation sur le circuit n'utilise le même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="6b271-239">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="6b271-240">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="6b271-240">AS number for peering.</span></span> <span data-ttu-id="6b271-241">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="6b271-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="6b271-242">Préfixes publiés : vous devez fournir une liste de tous les préfixes que vous prévoyez de publier sur la session BGP.</span><span class="sxs-lookup"><span data-stu-id="6b271-242">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="6b271-243">Seuls les préfixes d'adresses IP publiques sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="6b271-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="6b271-244">Si vous prévoyez d’envoyer un jeu de préfixes, vous pouvez envoyer une liste séparée par des virgules.</span><span class="sxs-lookup"><span data-stu-id="6b271-244">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="6b271-245">Ces préfixes doivent être enregistrés en votre nom dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="6b271-245">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="6b271-246">**(Facultatif)** ASN client : si vous publiez des préfixes non enregistrés dans le numéro de système autonome d’homologation, vous pouvez spécifier le numéro de système autonome avec lequel ils sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="6b271-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="6b271-247">Nom du registre de routage : vous pouvez spécifier les registres RIR/IRR par rapport auxquels le numéro AS et les préfixes sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="6b271-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="6b271-248">**Facultatif :** un hachage MD5 si vous choisissez d’en utiliser un.</span><span class="sxs-lookup"><span data-stu-id="6b271-248">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="6b271-249">Utilisez l’exemple suivant afin de configurer l’homologation Microsoft pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="6b271-249">Use the following example to configure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="6b271-250">Pour obtenir des détails sur l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="6b271-250">To get Microsoft peering details</span></span>

<span data-ttu-id="6b271-251">Vous pouvez obtenir les détails de la configuration à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b271-251">You can get configuration details using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="6b271-252">Pour mettre à jour la configuration d’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="6b271-252">To update Microsoft peering configuration</span></span>

<span data-ttu-id="6b271-253">Vous pouvez mettre à jour toute partie de la configuration à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b271-253">You can update any part of the configuration using the following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="6b271-254">Pour supprimer une homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="6b271-254">To delete Microsoft peering</span></span>

<span data-ttu-id="6b271-255">Vous pouvez supprimer votre configuration d’homologation en exécutant l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6b271-255">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="6b271-256">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b271-256">Next steps</span></span>

<span data-ttu-id="6b271-257">Ensuite, [liez un réseau virtuel à un circuit ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="6b271-257">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="6b271-258">Pour plus d'informations sur les workflows ExpressRoute, consultez [Workflows ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="6b271-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="6b271-259">Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="6b271-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="6b271-260">Pour plus d’informations sur l’utilisation des réseaux virtuels, consultez la page [Présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b271-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
