---
title: "Obtention de tables ARP - Resource Manager : guide de résolution des problèmes Azure ExpressRoute | Microsoft Docs"
description: "Cette page fournit des instructions sur l’obtention des tables ARP pour un circuit ExpressRoute"
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: a65b1ba2998eae33b3e73bd2492fbbf025eb5946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-resource-manager-deployment-model"></a><span data-ttu-id="3ea0f-103">Obtention de tables ARP dans le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3ea0f-103">Getting ARP tables in the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ea0f-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3ea0f-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="3ea0f-105">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="3ea0f-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="3ea0f-106">Cet article vous guide tout au long des étapes d’apprentissage des tables ARP pour votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-106">This article walks you through the steps to learn the ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3ea0f-107">Ce document a pour objet de vous aider à diagnostiquer et résoudre les problèmes simples.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="3ea0f-108">Il n’a pas pour objet de remplacer le support de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="3ea0f-109">Si vous ne parvenez pas à résoudre le problème en suivant les conseils ci-dessous, ouvrez un ticket de support auprès du [support Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) .</span><span class="sxs-lookup"><span data-stu-id="3ea0f-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable to solve the problem using the guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="3ea0f-110">Protocole ARP (Address Resolution Protocol) et tables ARP</span><span class="sxs-lookup"><span data-stu-id="3ea0f-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="3ea0f-111">Le protocole ARP (Address Resolution Protocol) est un protocole de couche 2 défini dans [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="3ea0f-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="3ea0f-112">ARP est utilisé pour mapper l’adresse Ethernet (adresse MAC) avec une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-112">ARP is used to map the Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="3ea0f-113">La table ARP fournit un mappage de l’adresse ipv4 et de l’adresse MAC pour une homologation particulière.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-113">The ARP table provides a mapping of the ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="3ea0f-114">La table ARP d’une homologation de circuit ExpressRoute fournit les informations suivantes pour chaque interface (principale et secondaire)</span><span class="sxs-lookup"><span data-stu-id="3ea0f-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="3ea0f-115">Mappage de l’adresse IP de l’interface du routeur local sur l’adresse MAC</span><span class="sxs-lookup"><span data-stu-id="3ea0f-115">Mapping of on-premises router interface ip address to the MAC address</span></span>
2. <span data-ttu-id="3ea0f-116">Mappage de l’adresse IP de l’interface du routeur ExpressRoute sur l’adresse MAC</span><span class="sxs-lookup"><span data-stu-id="3ea0f-116">Mapping of ExpressRoute router interface ip address to the MAC address</span></span>
3. <span data-ttu-id="3ea0f-117">Âge du mappage</span><span class="sxs-lookup"><span data-stu-id="3ea0f-117">Age of the mapping</span></span>

<span data-ttu-id="3ea0f-118">Les tables ARP permettent de valider la configuration de la couche 2 et de résoudre les problèmes de connectivité de base de la couche 2.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="3ea0f-119">Exemple de table ARP :</span><span class="sxs-lookup"><span data-stu-id="3ea0f-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="3ea0f-120">La section suivante fournit des informations sur l’affichage des tables ARP vues par les routeurs de bordure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-120">The following section provides information on how you can view the ARP tables seen by the ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="3ea0f-121">Conditions préalables à l’apprentissage des tables ARP</span><span class="sxs-lookup"><span data-stu-id="3ea0f-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="3ea0f-122">Assurez-vous que vous disposez des éléments suivants avant de poursuivre</span><span class="sxs-lookup"><span data-stu-id="3ea0f-122">Ensure that you have the following before you progress further</span></span>

* <span data-ttu-id="3ea0f-123">Un circuit ExpressRoute valide configuré avec au moins une homologation.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="3ea0f-124">Le circuit doit être entièrement configuré par le fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="3ea0f-125">Vous (ou votre fournisseur de connectivité) devez avoir configuré au moins une des homologations (Azure privé, Azure public et Microsoft) sur ce circuit.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-125">You (or your connectivity provider) must have configured at least one of the peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="3ea0f-126">Plages d’adresses IP utilisées pour configurer les homologations (Azure privé, Azure public et Microsoft).</span><span class="sxs-lookup"><span data-stu-id="3ea0f-126">IP address ranges used for configuring the peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="3ea0f-127">Passez en revue les exemples d’affectation d’adresses IP sur la [page de configuration requise pour le routage ExpressRoute](expressroute-routing.md) pour comprendre de quelle manière les adresses IP sont mappées aux interfaces de votre côté et du côté d’ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-127">Review the ip address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how ip addresses are mapped to interfaces on your side and on the ExpressRoute side.</span></span> <span data-ttu-id="3ea0f-128">Vous pouvez obtenir plus d’informations sur la configuration d’homologation en examinant la [page de configuration d’homologation ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="3ea0f-128">You can get information on the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="3ea0f-129">Informations de votre équipe réseau/fournisseur de connectivité sur les adresses MAC des interfaces utilisées avec ces adresses IP.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-129">Information from your networking team / connectivity provider on the MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="3ea0f-130">Vous devez disposer du dernier module PowerShell pour Azure (version 1.50 ou plus récente).</span><span class="sxs-lookup"><span data-stu-id="3ea0f-130">You must have the latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-the-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="3ea0f-131">Obtention des tables ARP pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3ea0f-131">Getting the ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="3ea0f-132">Cette section fournit des instructions sur la manière d’afficher les tables ARP par homologation à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-132">This section provides instructions on how you can view the ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="3ea0f-133">Vous ou votre fournisseur de connectivité devez avoir configuré l’homologation avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-133">You or your connectivity provider must have configured the peering before progressing further.</span></span> <span data-ttu-id="3ea0f-134">Chaque circuit a deux chemins d’accès (principal et secondaire).</span><span class="sxs-lookup"><span data-stu-id="3ea0f-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="3ea0f-135">Vous pouvez contrôler indépendamment la table ARP de chaque chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="3ea0f-136">Tables ARP pour l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="3ea0f-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="3ea0f-137">L’applet de commande suivante fournit les tables ARP pour l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="3ea0f-137">The following cmdlet provides the ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="3ea0f-138">Un exemple de sortie est affiché ci-dessous pour l’un des chemins d’accès</span><span class="sxs-lookup"><span data-stu-id="3ea0f-138">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="3ea0f-139">Tables ARP pour l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="3ea0f-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="3ea0f-140">L’applet de commande suivante fournit les tables ARP pour l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="3ea0f-140">The following cmdlet provides the ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="3ea0f-141">Un exemple de sortie est affiché ci-dessous pour l’un des chemins d’accès</span><span class="sxs-lookup"><span data-stu-id="3ea0f-141">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="3ea0f-142">Tables ARP pour l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="3ea0f-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="3ea0f-143">L’applet de commande suivante fournit les tables ARP de l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="3ea0f-143">The following cmdlet provides the ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="3ea0f-144">Un exemple de sortie est affiché ci-dessous pour l’un des chemins d’accès</span><span class="sxs-lookup"><span data-stu-id="3ea0f-144">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="3ea0f-145">Utilisation de ces informations</span><span class="sxs-lookup"><span data-stu-id="3ea0f-145">How to use this information</span></span>
<span data-ttu-id="3ea0f-146">La table ARP d’une homologation peut servir à valider la connectivité et la configuration de la couche 2.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-146">The ARP table of a peering can be used to determine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="3ea0f-147">Cette section fournit une vue d’ensemble de l’aspect des tables ARP dans différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="3ea0f-148">Table ARP lorsqu’un circuit est dans un état opérationnel (état attendu)</span><span class="sxs-lookup"><span data-stu-id="3ea0f-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="3ea0f-149">La table ARP aura une entrée pour le côté local avec une adresse IP valide et une adresse MAC, ainsi qu’une entrée similaire pour le côté Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-149">The ARP table will have an entry for the on-premises side with a valid IP address and MAC address and a similar entry for the Microsoft side.</span></span> 
* <span data-ttu-id="3ea0f-150">Le dernier octet de l’adresse IP locale sera toujours un nombre impair.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-150">The last octet of the on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="3ea0f-151">Le dernier octet de l’adresse IP Microsoft sera toujours un nombre pair.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-151">The last octet of the Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="3ea0f-152">La même adresse MAC s’affichera côté Microsoft pour les trois homologations (principales/secondaires).</span><span class="sxs-lookup"><span data-stu-id="3ea0f-152">The same MAC address will appear on the Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="3ea0f-153">Table ARP en cas de problèmes côté fournisseur de connectivité/local</span><span class="sxs-lookup"><span data-stu-id="3ea0f-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="3ea0f-154">Si vous rencontrez des problèmes liés au site ou au fournisseur de connectivité, vous pouvez constater qu’une seule entrée apparaîtra dans la table ARP ou l’adresse MAC locale sera incomplète.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-154">If there are issues with the on-premises or connectivity provider you may see that either only one entry will appear in the ARP table or the on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="3ea0f-155">Cette commande affiche le mappage entre l’adresse MAC et l’adresse IP utilisée côté Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-155">This will show the mapping between the MAC address and IP address used in the Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="3ea0f-156">ou</span><span class="sxs-lookup"><span data-stu-id="3ea0f-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="3ea0f-157">Ouvrez une demande de support avec votre fournisseur de connectivité pour déboguer ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-157">Open a support request with your connectivity provider to debug such issues.</span></span> <span data-ttu-id="3ea0f-158">Si la table ARP ne comprend pas les adresses IP des interfaces mappées sur des adresses MAC, passez en revue les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ea0f-158">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
> 
> 1. <span data-ttu-id="3ea0f-159">Si la première adresse IP du sous-réseau /30 affecté pour la liaison entre les MSEE-PR et MSEE est utilisée dans l’interface de MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-159">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="3ea0f-160">Azure utilise toujours la deuxième adresse IP pour les MSEE.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-160">Azure always uses the second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="3ea0f-161">Vérifiez si les balises VLAN du client (C-Tag) et du service (S-Tag) correspondent à la paire MSEE-PR et MSEE.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-161">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="3ea0f-162">Table ARP en cas de problèmes côté Microsoft</span><span class="sxs-lookup"><span data-stu-id="3ea0f-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="3ea0f-163">Aucune table ARP ne s’affiche pour une homologation en cas de problèmes côté Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-163">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span> 
* <span data-ttu-id="3ea0f-164">Ouvrez un incident auprès du [support technique Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="3ea0f-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="3ea0f-165">Spécifiez que vous avez un problème au niveau de la connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3ea0f-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ea0f-166">Next Steps</span></span>
* <span data-ttu-id="3ea0f-167">Valider les configurations de couche 3 pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3ea0f-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="3ea0f-168">Obtenir un récapitulatif d’itinéraires pour déterminer l’état des sessions BGP</span><span class="sxs-lookup"><span data-stu-id="3ea0f-168">Get route summary to determine the state of BGP sessions</span></span> 
  * <span data-ttu-id="3ea0f-169">Obtenir une table d’itinéraires pour déterminer quels préfixes sont publiés sur ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3ea0f-169">Get route table to determine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="3ea0f-170">Valider le transfert des données en examinant les octets en entrée/sortie</span><span class="sxs-lookup"><span data-stu-id="3ea0f-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="3ea0f-171">Ouvrez un ticket de support auprès du [support Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) si vous rencontrez encore des problèmes.</span><span class="sxs-lookup"><span data-stu-id="3ea0f-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

