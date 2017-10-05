---
title: "Obtention de tables ARP - Classic : guide de résolution des problèmes Azure ExpressRoute | Microsoft Docs"
description: "Cette page fournit des instructions sur l’obtention des tables ARP pour un circuit ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: fcc847b7e30fd55ca759830e0254ab7542e7663e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-classic-deployment-model"></a><span data-ttu-id="762af-103">Obtention de tables ARP dans le modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="762af-103">Getting ARP tables in the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="762af-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="762af-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="762af-105">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="762af-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="762af-106">Cet article vous guide dans la procédure d’obtention des tables ARP (Address Resolution Protocol) pour votre circuit Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="762af-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="762af-107">Ce document a pour objet de vous aider à diagnostiquer et résoudre les problèmes simples.</span><span class="sxs-lookup"><span data-stu-id="762af-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="762af-108">Il n’a pas pour objet de remplacer le support de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="762af-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="762af-109">Si vous ne pouvez pas résoudre le problème en suivant les conseils suivants, ouvrez une demande de support auprès de [Microsoft Azure - Aide + support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="762af-109">If you can't solve the problem by using the following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="762af-110">Protocole ARP (Address Resolution Protocol) et tables ARP</span><span class="sxs-lookup"><span data-stu-id="762af-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="762af-111">ARP est un protocole de couche 2 défini dans [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="762af-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="762af-112">Le protocole ARP permet de mapper une adresse Ethernet (adresse MAC) avec une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="762af-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span></span>

<span data-ttu-id="762af-113">Une table ARP fournit un mappage de l’adresse IPv4 et de l’adresse MAC pour une homologation particulière.</span><span class="sxs-lookup"><span data-stu-id="762af-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="762af-114">La table ARP d’une homologation de circuit ExpressRoute fournit les informations suivantes pour chaque interface (principale et secondaire) :</span><span class="sxs-lookup"><span data-stu-id="762af-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="762af-115">Mappage de l’adresse IP d’une interface de routeur local sur une adresse MAC</span><span class="sxs-lookup"><span data-stu-id="762af-115">Mapping of an on-premises router interface IP address to a MAC address</span></span>
2. <span data-ttu-id="762af-116">Mappage de l’adresse IP d’une interface de routeur ExpressRoute sur une adresse MAC</span><span class="sxs-lookup"><span data-stu-id="762af-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span></span>
3. <span data-ttu-id="762af-117">Âge du mappage</span><span class="sxs-lookup"><span data-stu-id="762af-117">The age of the mapping</span></span>

<span data-ttu-id="762af-118">Les tables ARP permettent de valider la configuration de la couche 2 et de résoudre les problèmes de connectivité de base de la couche 2.</span><span class="sxs-lookup"><span data-stu-id="762af-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="762af-119">Vous trouverez ci-dessous un exemple de table ARP :</span><span class="sxs-lookup"><span data-stu-id="762af-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="762af-120">La section suivante fournit des informations sur l’affichage des tables ARP vues par les routeurs périphériques ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="762af-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="762af-121">Conditions préalables à l’utilisation des tables ARP</span><span class="sxs-lookup"><span data-stu-id="762af-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="762af-122">Assurez-vous que vous disposez des éléments suivants avant de poursuivre :</span><span class="sxs-lookup"><span data-stu-id="762af-122">Ensure that you have the following before you continue:</span></span>

* <span data-ttu-id="762af-123">Un circuit ExpressRoute valide configuré avec au moins une homologation.</span><span class="sxs-lookup"><span data-stu-id="762af-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="762af-124">Le circuit doit être entièrement configuré par le fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="762af-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="762af-125">Vous (ou votre fournisseur de connectivité) devez configurer au moins une des homologations (Azure privé, Azure public ou Microsoft) sur ce circuit.</span><span class="sxs-lookup"><span data-stu-id="762af-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="762af-126">Plages d’adresses IP utilisées pour configurer les homologations (Azure privé, Azure public et Microsoft).</span><span class="sxs-lookup"><span data-stu-id="762af-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="762af-127">Passez en revue les exemples d’affectation d’adresses IP sur la [page de configuration requise pour le routage ExpressRoute](expressroute-routing.md) pour comprendre de quelle manière les adresses IP sont mappées aux interfaces de votre côté et du côté d’ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="762af-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span></span> <span data-ttu-id="762af-128">Vous pouvez obtenir plus d’informations sur la configuration d’homologation en examinant la [page de configuration d’homologation ExpressRoute](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="762af-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="762af-129">Informations de votre équipe réseau ou de votre fournisseur de connectivité sur les adresses MAC des interfaces utilisées avec ces adresses IP.</span><span class="sxs-lookup"><span data-stu-id="762af-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="762af-130">Le dernier module Windows PowerShell pour Azure (version 1.50 ou plus récente).</span><span class="sxs-lookup"><span data-stu-id="762af-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="762af-131">Tables ARP pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="762af-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="762af-132">Cette section fournit des instructions sur l’affichage des tables ARP pour chaque type d’homologation à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="762af-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="762af-133">Avant de continuer, vous ou votre fournisseur de connectivité devez configurer l’homologation.</span><span class="sxs-lookup"><span data-stu-id="762af-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span></span> <span data-ttu-id="762af-134">Chaque circuit a deux chemins d’accès (principal et secondaire).</span><span class="sxs-lookup"><span data-stu-id="762af-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="762af-135">Vous pouvez contrôler indépendamment la table ARP de chaque chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="762af-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="762af-136">Tables ARP pour l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="762af-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="762af-137">L’applet de commande suivante fournit les tables ARP pour l’homologation privée Azure :</span><span class="sxs-lookup"><span data-stu-id="762af-137">The following cmdlet provides the ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="762af-138">Vous trouverez ci-dessous un exemple de sortie pour l’un des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="762af-138">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="762af-139">Tables ARP pour l’homologation publique Azure :</span><span class="sxs-lookup"><span data-stu-id="762af-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="762af-140">L’applet de commande suivante fournit les tables ARP pour l’homologation publique Azure :</span><span class="sxs-lookup"><span data-stu-id="762af-140">The following cmdlet provides the ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="762af-141">Vous trouverez ci-dessous un exemple de sortie pour l’un des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="762af-141">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="762af-142">Vous trouverez ci-dessous un exemple de sortie pour l’un des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="762af-142">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="762af-143">Tables ARP pour l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="762af-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="762af-144">L’applet de commande suivante fournit les tables ARP de l’homologation Microsoft :</span><span class="sxs-lookup"><span data-stu-id="762af-144">The following cmdlet provides the ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="762af-145">Un exemple de sortie est affiché ci-dessous pour l’un des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="762af-145">Sample output is shown below for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="762af-146">Utilisation de ces informations</span><span class="sxs-lookup"><span data-stu-id="762af-146">How to use this information</span></span>
<span data-ttu-id="762af-147">La table ARP d’une homologation peut servir à valider la connectivité et la configuration de la couche 2.</span><span class="sxs-lookup"><span data-stu-id="762af-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="762af-148">Cette section fournit une vue d’ensemble de l’aspect des tables ARP dans différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="762af-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="762af-149">Table ARP lorsqu’un circuit est à l’état opérationnel (attendu)</span><span class="sxs-lookup"><span data-stu-id="762af-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="762af-150">La table ARP dispose d’une entrée pour le côté local avec une adresse IP valide et une adresse MAC, ainsi que d’une entrée similaire pour le côté Microsoft.</span><span class="sxs-lookup"><span data-stu-id="762af-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span></span>
* <span data-ttu-id="762af-151">Le dernier octet de l’adresse IP locale est toujours un nombre impair.</span><span class="sxs-lookup"><span data-stu-id="762af-151">The last octet of the on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="762af-152">Le dernier octet de l’adresse IP Microsoft est toujours un nombre pair.</span><span class="sxs-lookup"><span data-stu-id="762af-152">The last octet of the Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="762af-153">La même adresse MAC s’affiche côté Microsoft pour les trois homologations (principales/secondaires).</span><span class="sxs-lookup"><span data-stu-id="762af-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-the-connectivity-provider-side-has-problems"></a><span data-ttu-id="762af-154">Table ARP en cas de problèmes en local ou côté fournisseur de connectivité</span><span class="sxs-lookup"><span data-stu-id="762af-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span></span>
 <span data-ttu-id="762af-155">Une seule entrée apparaît dans la table ARP.</span><span class="sxs-lookup"><span data-stu-id="762af-155">Only one entry appears in the ARP table.</span></span> <span data-ttu-id="762af-156">Elle affiche le mappage entre l’adresse MAC et l’adresse IP utilisée côté Microsoft.</span><span class="sxs-lookup"><span data-stu-id="762af-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="762af-157">Si vous rencontrez un problème de ce type, ouvrez une demande de support auprès de votre fournisseur de connectivité pour le résoudre.</span><span class="sxs-lookup"><span data-stu-id="762af-157">If you experience an issue like this, open a support request with your connectivity provider to resolve it.</span></span>
> 
> 

### <a name="arp-table-when-the-microsoft-side-has-problems"></a><span data-ttu-id="762af-158">Table ARP en cas de problèmes côté Microsoft</span><span class="sxs-lookup"><span data-stu-id="762af-158">ARP table when the Microsoft side has problems</span></span>
* <span data-ttu-id="762af-159">Aucune table ARP ne s’affiche pour une homologation en cas de problèmes côté Microsoft.</span><span class="sxs-lookup"><span data-stu-id="762af-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span>
* <span data-ttu-id="762af-160">Ouvrez une demande de support auprès de [Microsoft Azure - Aide + support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="762af-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="762af-161">Précisez que vous avez un problème au niveau de la connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="762af-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="762af-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="762af-162">Next steps</span></span>
* <span data-ttu-id="762af-163">Valider les configurations de couche 3 pour votre circuit ExpressRoute :</span><span class="sxs-lookup"><span data-stu-id="762af-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="762af-164">Obtenir un récapitulatif d’itinéraires pour déterminer l’état des sessions BGP.</span><span class="sxs-lookup"><span data-stu-id="762af-164">Get a route summary to determine the state of BGP sessions.</span></span>
  * <span data-ttu-id="762af-165">Obtenir une table d’itinéraires pour déterminer quels préfixes sont publiés sur ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="762af-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="762af-166">Valider le transfert des données en examinant les octets en entrée et en sortie.</span><span class="sxs-lookup"><span data-stu-id="762af-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="762af-167">Ouvrir une demande de support auprès de [Microsoft Azure - Aide + support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) si vous rencontrez encore des problèmes.</span><span class="sxs-lookup"><span data-stu-id="762af-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

