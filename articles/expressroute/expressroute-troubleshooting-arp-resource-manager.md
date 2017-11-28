---
title: "Obtention de tables ARP - Resource Manager : guide de résolution des problèmes Azure ExpressRoute | Microsoft Docs"
description: Cette page fournit des instructions sur la mise en route hello ARP tables pour un circuit ExpressRoute
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
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a><span data-ttu-id="e3ab0-103">Mise en route ARP tables dans le modèle de déploiement du Gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="e3ab0-103">Getting ARP tables in hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3ab0-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3ab0-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="e3ab0-105">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="e3ab0-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="e3ab0-106">Cet article vous guide tout au long de hello de toolearn étapes hello QU'ARP tables votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-106">This article walks you through hello steps toolearn hello ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e3ab0-107">Ce document est prévue toohelp vous diagnostiquez et résoudre les problèmes de simples.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="e3ab0-108">Il n’est pas prévue toobe un remplacement pour le support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="e3ab0-109">Vous devez ouvrir un ticket de support avec [prise en charge de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) en cas de problème de hello toosolve impossible à l’aide d’instructions hello décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable toosolve hello problem using hello guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="e3ab0-110">Protocole ARP (Address Resolution Protocol) et tables ARP</span><span class="sxs-lookup"><span data-stu-id="e3ab0-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="e3ab0-111">Le protocole ARP (Address Resolution Protocol) est un protocole de couche 2 défini dans [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="e3ab0-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="e3ab0-112">ARP est utilisé toomap hello Ethernet (adresse MAC) avec une adresse ip.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-112">ARP is used toomap hello Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="e3ab0-113">Hello table ARP fournit un mappage d’adresse ipv4 de hello et une adresse MAC pour une homologation particulier.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-113">hello ARP table provides a mapping of hello ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="e3ab0-114">Hello table ARP d’un circuit ExpressRoute d’homologation fournit hello suivant des informations pour chaque interface (principal et secondaire)</span><span class="sxs-lookup"><span data-stu-id="e3ab0-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="e3ab0-115">Mappage d’adresse MAC de local routeur interface ip adresse toohello</span><span class="sxs-lookup"><span data-stu-id="e3ab0-115">Mapping of on-premises router interface ip address toohello MAC address</span></span>
2. <span data-ttu-id="e3ab0-116">Mappage d’adresse MAC de ExpressRoute routeur interface ip adresse toohello</span><span class="sxs-lookup"><span data-stu-id="e3ab0-116">Mapping of ExpressRoute router interface ip address toohello MAC address</span></span>
3. <span data-ttu-id="e3ab0-117">Durée de vie de mappage de hello</span><span class="sxs-lookup"><span data-stu-id="e3ab0-117">Age of hello mapping</span></span>

<span data-ttu-id="e3ab0-118">Les tables ARP permettent de valider la configuration de la couche 2 et de résoudre les problèmes de connectivité de base de la couche 2.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="e3ab0-119">Exemple de table ARP :</span><span class="sxs-lookup"><span data-stu-id="e3ab0-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="e3ab0-120">Hello section suivante fournit des informations sur la façon dont vous pouvez afficher hello tables ARP visibles par les routeurs de périphérie hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-120">hello following section provides information on how you can view hello ARP tables seen by hello ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="e3ab0-121">Conditions préalables à l’apprentissage des tables ARP</span><span class="sxs-lookup"><span data-stu-id="e3ab0-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="e3ab0-122">Assurez-vous d’avoir hello suivant avant de vous davantage de progression</span><span class="sxs-lookup"><span data-stu-id="e3ab0-122">Ensure that you have hello following before you progress further</span></span>

* <span data-ttu-id="e3ab0-123">Un circuit ExpressRoute valide configuré avec au moins une homologation.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="e3ab0-124">circuit de Hello doit être entièrement configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="e3ab0-125">Vous (ou votre fournisseur de connectivité) doit avoir configuré au moins un des homologations hello (public Azure de privé, Azure et Microsoft) sur ce circuit.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-125">You (or your connectivity provider) must have configured at least one of hello peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="e3ab0-126">Plages d’adresses IP utilisées pour la configuration des homologations hello (public Azure de privé, Azure et Microsoft).</span><span class="sxs-lookup"><span data-stu-id="e3ab0-126">IP address ranges used for configuring hello peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="e3ab0-127">Passez en revue les exemples de l’attribution d’adresses hello ip Bonjour [page de spécifications de routage ExpressRoute](expressroute-routing.md) tooget une compréhension de la façon dont les adresses ip sont mappées toointerfaces votre côté et hello ExpressRoute côté.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-127">Review hello ip address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how ip addresses are mapped toointerfaces on your side and on hello ExpressRoute side.</span></span> <span data-ttu-id="e3ab0-128">Vous pouvez obtenir des informations sur la configuration d’homologation hello en examinant hello [page de configuration d’homologation ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e3ab0-128">You can get information on hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="e3ab0-129">Pour plus d’informations à partir de votre équipe réseau / fournisseur de connectivité sur des adresses MAC hello des interfaces utilisées avec ces adresses IP.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-129">Information from your networking team / connectivity provider on hello MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="e3ab0-130">Vous devez disposer du module PowerShell plus récent hello pour Azure (version 1,50 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="e3ab0-130">You must have hello latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="e3ab0-131">Obtention de tables hello ARP votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e3ab0-131">Getting hello ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="e3ab0-132">Cette section fournit des instructions sur la façon dont vous pouvez afficher hello tables ARP par homologation à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-132">This section provides instructions on how you can view hello ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="e3ab0-133">Vous ou votre fournisseur de connectivité doit avoir configuré hello d’homologation avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-133">You or your connectivity provider must have configured hello peering before progressing further.</span></span> <span data-ttu-id="e3ab0-134">Chaque circuit a deux chemins d’accès (principal et secondaire).</span><span class="sxs-lookup"><span data-stu-id="e3ab0-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="e3ab0-135">Vous pouvez vérifier hello table ARP pour chaque chemin d’accès indépendamment.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="e3ab0-136">Tables ARP pour l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="e3ab0-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="e3ab0-137">Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="e3ab0-137">hello following cmdlet provides hello ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="e3ab0-138">Exemple de sortie est illustrée ci-dessous pour un des chemins d’accès hello</span><span class="sxs-lookup"><span data-stu-id="e3ab0-138">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="e3ab0-139">Tables ARP pour l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="e3ab0-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="e3ab0-140">Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="e3ab0-140">hello following cmdlet provides hello ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="e3ab0-141">Exemple de sortie est illustrée ci-dessous pour un des chemins d’accès hello</span><span class="sxs-lookup"><span data-stu-id="e3ab0-141">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="e3ab0-142">Tables ARP pour l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="e3ab0-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="e3ab0-143">Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation de Microsoft</span><span class="sxs-lookup"><span data-stu-id="e3ab0-143">hello following cmdlet provides hello ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="e3ab0-144">Exemple de sortie est illustrée ci-dessous pour un des chemins d’accès hello</span><span class="sxs-lookup"><span data-stu-id="e3ab0-144">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="e3ab0-145">Comment toouse ces informations</span><span class="sxs-lookup"><span data-stu-id="e3ab0-145">How toouse this information</span></span>
<span data-ttu-id="e3ab0-146">Hello table ARP d’une homologation peut servir toodetermine valider la configuration de la couche 2 et la connectivité.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-146">hello ARP table of a peering can be used toodetermine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="e3ab0-147">Cette section fournit une vue d’ensemble de l’aspect des tables ARP dans différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="e3ab0-148">Table ARP lorsqu’un circuit est dans un état opérationnel (état attendu)</span><span class="sxs-lookup"><span data-stu-id="e3ab0-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="e3ab0-149">Hello table ARP aura une entrée pour le côté local de hello avec une adresse IP valide et une adresse MAC et une entrée similaire pour hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-149">hello ARP table will have an entry for hello on-premises side with a valid IP address and MAC address and a similar entry for hello Microsoft side.</span></span> 
* <span data-ttu-id="e3ab0-150">dernier octet de Hello d’adresse ip de local hello sera toujours un nombre impair.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-150">hello last octet of hello on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="e3ab0-151">Hello dernier octet de hello adresse ip de Microsoft sera toujours un nombre pair.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-151">hello last octet of hello Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="e3ab0-152">Hello même adresse MAC apparaîtront sur hello côté Microsoft pour tous les 3 homologations (principales / secondaire).</span><span class="sxs-lookup"><span data-stu-id="e3ab0-152">hello same MAC address will appear on hello Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="e3ab0-153">Table ARP en cas de problèmes côté fournisseur de connectivité/local</span><span class="sxs-lookup"><span data-stu-id="e3ab0-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="e3ab0-154">Si des problèmes avec hello localement ou fournisseur de connectivité peuvent apparaître qu’une seule entrée sera Bonjour ARP table ou hello local MAC adresse affichera incomplète.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-154">If there are issues with hello on-premises or connectivity provider you may see that either only one entry will appear in hello ARP table or hello on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="e3ab0-155">Cette opération affiche le mappage hello entre hello adresse MAC et l’adresse IP utilisée dans hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-155">This will show hello mapping between hello MAC address and IP address used in hello Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="e3ab0-156">ou</span><span class="sxs-lookup"><span data-stu-id="e3ab0-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="e3ab0-157">Ouvrez une demande de support avec votre toodebug de fournisseur de connectivité de tels problèmes.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-157">Open a support request with your connectivity provider toodebug such issues.</span></span> <span data-ttu-id="e3ab0-158">Si hello table ARP ne dispose pas des adresses IP des interfaces de hello mappé tooMAC adresses, hello révision informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3ab0-158">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
> 
> 1. <span data-ttu-id="e3ab0-159">Si hello première adresse IP du sous-réseau de hello /30 affecté pour la liaison hello entre hello MSEE-PR et MSEE est utilisé sur l’interface hello de MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-159">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="e3ab0-160">Azure utilise toujours l’adresse IP de la deuxième hello pour MSEEs.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-160">Azure always uses hello second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="e3ab0-161">Vérifiez si le client hello (C-Tag) et balises VLAN de service (S-Tag) correspondent à la fois sur la paire de MSEE-PR et MSEE.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-161">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="e3ab0-162">Table ARP en cas de problèmes côté Microsoft</span><span class="sxs-lookup"><span data-stu-id="e3ab0-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="e3ab0-163">Vous ne verrez pas un tableau ARP pour une homologation si des problèmes sur hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-163">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span> 
* <span data-ttu-id="e3ab0-164">Ouvrez un incident auprès du [support technique Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="e3ab0-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="e3ab0-165">Spécifiez que vous avez un problème au niveau de la connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e3ab0-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3ab0-166">Next Steps</span></span>
* <span data-ttu-id="e3ab0-167">Valider les configurations de couche 3 pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e3ab0-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="e3ab0-168">Obtention de l’itinéraire résumé toodetermine hello état de sessions BGP</span><span class="sxs-lookup"><span data-stu-id="e3ab0-168">Get route summary toodetermine hello state of BGP sessions</span></span> 
  * <span data-ttu-id="e3ab0-169">Obtenir toodetermine de table de routage les préfixes sont publiés sur ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e3ab0-169">Get route table toodetermine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="e3ab0-170">Valider le transfert des données en examinant les octets en entrée/sortie</span><span class="sxs-lookup"><span data-stu-id="e3ab0-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="e3ab0-171">Ouvrez un ticket de support auprès du [support Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) si vous rencontrez encore des problèmes.</span><span class="sxs-lookup"><span data-stu-id="e3ab0-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

