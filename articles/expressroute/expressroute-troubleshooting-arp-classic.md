---
title: "Obtention de tables ARP - Classic : guide de résolution des problèmes Azure ExpressRoute | Microsoft Docs"
description: Cette page fournit des instructions pour la mise en route hello ARP tables pour un circuit ExpressRoute.
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
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a><span data-ttu-id="1106f-103">Mise en route ARP tables dans le modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="1106f-103">Getting ARP tables in hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1106f-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1106f-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="1106f-105">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="1106f-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="1106f-106">Cet article vous guide tout au long des étapes hello pour l’obtention des tables du protocole ARP (Address Resolution) hello pour votre circuit ExpressRoute d’Azure.</span><span class="sxs-lookup"><span data-stu-id="1106f-106">This article walks you through hello steps for getting hello Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1106f-107">Ce document est prévue toohelp vous diagnostiquez et résoudre les problèmes de simples.</span><span class="sxs-lookup"><span data-stu-id="1106f-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="1106f-108">Il n’est pas prévue toobe un remplacement pour le support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1106f-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="1106f-109">Si vous ne pouvez pas résoudre les problème de hello à l’aide de hello suivant recommandations, ouvrez une demande de support avec [Microsoft Azure aide + support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="1106f-109">If you can't solve hello problem by using hello following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="1106f-110">Protocole ARP (Address Resolution Protocol) et tables ARP</span><span class="sxs-lookup"><span data-stu-id="1106f-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="1106f-111">ARP est un protocole de couche 2 défini dans [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="1106f-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="1106f-112">ARP est toomap utilisé une Ethernet (adresse MAC) tooan adresse IP.</span><span class="sxs-lookup"><span data-stu-id="1106f-112">ARP is used toomap an Ethernet address (MAC address) tooan IP address.</span></span>

<span data-ttu-id="1106f-113">Une table ARP fournit un mappage d’adresse IPv4 de hello et une adresse MAC pour une homologation particulier.</span><span class="sxs-lookup"><span data-stu-id="1106f-113">An ARP table provides a mapping of hello IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="1106f-114">Hello table ARP d’un circuit ExpressRoute d’homologation fournit hello informations pour chaque interface (principal et secondaire) suivantes :</span><span class="sxs-lookup"><span data-stu-id="1106f-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="1106f-115">Mappage d’une adresse MAC de local routeur interface IP adresse tooa</span><span class="sxs-lookup"><span data-stu-id="1106f-115">Mapping of an on-premises router interface IP address tooa MAC address</span></span>
2. <span data-ttu-id="1106f-116">Mappage d’une adresse MAC de ExpressRoute routeur interface IP adresse tooa</span><span class="sxs-lookup"><span data-stu-id="1106f-116">Mapping of an ExpressRoute router interface IP address tooa MAC address</span></span>
3. <span data-ttu-id="1106f-117">âge Hello du mappage de hello</span><span class="sxs-lookup"><span data-stu-id="1106f-117">hello age of hello mapping</span></span>

<span data-ttu-id="1106f-118">Les tables ARP permettent de valider la configuration de la couche 2 et de résoudre les problèmes de connectivité de base de la couche 2.</span><span class="sxs-lookup"><span data-stu-id="1106f-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="1106f-119">Vous trouverez ci-dessous un exemple de table ARP :</span><span class="sxs-lookup"><span data-stu-id="1106f-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="1106f-120">Hello suivant la section fournit des informations sur comment tooview hello tables ARP vus par les routeurs de périphérie hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1106f-120">hello following section provides information about how tooview hello ARP tables that are seen by hello ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="1106f-121">Conditions préalables à l’utilisation des tables ARP</span><span class="sxs-lookup"><span data-stu-id="1106f-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="1106f-122">Vérifiez que vous disposez des éléments suivants de hello avant de continuer :</span><span class="sxs-lookup"><span data-stu-id="1106f-122">Ensure that you have hello following before you continue:</span></span>

* <span data-ttu-id="1106f-123">Un circuit ExpressRoute valide configuré avec au moins une homologation.</span><span class="sxs-lookup"><span data-stu-id="1106f-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="1106f-124">circuit de Hello doit être entièrement configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="1106f-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="1106f-125">Vous (ou votre fournisseur de connectivité) devez configurer au moins un des homologations hello (public Azure de privé, Azure, ou Microsoft) sur ce circuit.</span><span class="sxs-lookup"><span data-stu-id="1106f-125">You (or your connectivity provider) must configure at least one of hello peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="1106f-126">Plages d’adresses IP qui sont utilisées pour la configuration des homologations hello (public Azure de privé, Azure et Microsoft).</span><span class="sxs-lookup"><span data-stu-id="1106f-126">IP address ranges that are used for configuring hello peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="1106f-127">Passez en revue les exemples de l’attribution d’adresses hello IP Bonjour [page de spécifications de routage ExpressRoute](expressroute-routing.md) tooget une compréhension de la façon dont les adresses IP sont mappées toointerfaces sur votre aise et hello ExpressRoute côté.</span><span class="sxs-lookup"><span data-stu-id="1106f-127">Review hello IP address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how IP addresses are mapped toointerfaces on your aise and on hello ExpressRoute side.</span></span> <span data-ttu-id="1106f-128">Vous pouvez obtenir des informations sur la configuration d’homologation de hello en examinant hello [page de configuration d’homologation ExpressRoute](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="1106f-128">You can get information about hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="1106f-129">Informations à partir de votre fournisseur d’équipe ou de la connectivité réseau sur des adresses MAC hello des interfaces de hello sont utilisées avec ces adresses IP.</span><span class="sxs-lookup"><span data-stu-id="1106f-129">Information from your networking team or connectivity provider about hello MAC addresses of hello interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="1106f-130">Hello dernier module Windows PowerShell pour Azure (version 1.50 ou ultérieure).</span><span class="sxs-lookup"><span data-stu-id="1106f-130">hello latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="1106f-131">Tables ARP pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1106f-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="1106f-132">Cette section fournit des instructions sur la façon dont les tables tooview hello ARP pour chaque type d’homologation à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1106f-132">This section provides instructions about how tooview hello ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="1106f-133">Avant de continuer, vous ou votre fournisseur de connectivité doit d’homologation de hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="1106f-133">Before you continue, either you or your connectivity provider needs tooconfigure hello peering.</span></span> <span data-ttu-id="1106f-134">Chaque circuit a deux chemins d’accès (principal et secondaire).</span><span class="sxs-lookup"><span data-stu-id="1106f-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="1106f-135">Vous pouvez vérifier hello table ARP pour chaque chemin d’accès indépendamment.</span><span class="sxs-lookup"><span data-stu-id="1106f-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="1106f-136">Tables ARP pour l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="1106f-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="1106f-137">Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation privée Azure :</span><span class="sxs-lookup"><span data-stu-id="1106f-137">hello following cmdlet provides hello ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="1106f-138">Voici un exemple de sortie pour un des chemins d’accès hello :</span><span class="sxs-lookup"><span data-stu-id="1106f-138">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="1106f-139">Tables ARP pour l’homologation publique Azure :</span><span class="sxs-lookup"><span data-stu-id="1106f-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="1106f-140">Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation publique Azure :</span><span class="sxs-lookup"><span data-stu-id="1106f-140">hello following cmdlet provides hello ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="1106f-141">Voici un exemple de sortie pour un des chemins d’accès hello :</span><span class="sxs-lookup"><span data-stu-id="1106f-141">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="1106f-142">Voici un exemple de sortie pour un des chemins d’accès hello :</span><span class="sxs-lookup"><span data-stu-id="1106f-142">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="1106f-143">Tables ARP pour l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="1106f-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="1106f-144">Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation de Microsoft :</span><span class="sxs-lookup"><span data-stu-id="1106f-144">hello following cmdlet provides hello ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="1106f-145">Exemple de sortie est illustrée ci-dessous pour un des chemins d’accès hello :</span><span class="sxs-lookup"><span data-stu-id="1106f-145">Sample output is shown below for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="1106f-146">Comment toouse ces informations</span><span class="sxs-lookup"><span data-stu-id="1106f-146">How toouse this information</span></span>
<span data-ttu-id="1106f-147">Hello table ARP d’une homologation peut être la connectivité et la configuration de la couche 2 de toovalidate utilisé.</span><span class="sxs-lookup"><span data-stu-id="1106f-147">hello ARP table of a peering can be used toovalidate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="1106f-148">Cette section fournit une vue d’ensemble de l’aspect des tables ARP dans différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="1106f-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="1106f-149">Table ARP lorsqu’un circuit est à l’état opérationnel (attendu)</span><span class="sxs-lookup"><span data-stu-id="1106f-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="1106f-150">Hello table ARP possède une entrée pour le côté local de hello avec une adresse IP et MAC valide et une entrée similaire pour hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1106f-150">hello ARP table has an entry for hello on-premises side with a valid IP and MAC address, and a similar entry for hello Microsoft side.</span></span>
* <span data-ttu-id="1106f-151">Hello dernier octet de l’adresse IP de local hello est toujours un nombre impair.</span><span class="sxs-lookup"><span data-stu-id="1106f-151">hello last octet of hello on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="1106f-152">Hello dernier octet de hello adresse IP de Microsoft est toujours un nombre pair.</span><span class="sxs-lookup"><span data-stu-id="1106f-152">hello last octet of hello Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="1106f-153">Hello même adresse MAC s’affiche sur hello côté Microsoft pour tous les homologations de trois (principal/secondaire).</span><span class="sxs-lookup"><span data-stu-id="1106f-153">hello same MAC address appears on hello Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a><span data-ttu-id="1106f-154">Table ARP lorsqu’il est sur site ou lorsque le côté du fournisseur de connectivité hello rencontre des problèmes</span><span class="sxs-lookup"><span data-stu-id="1106f-154">ARP table when it's on-premises or when hello connectivity-provider side has problems</span></span>
 <span data-ttu-id="1106f-155">Qu’une seule entrée apparaît dans la table ARP de hello.</span><span class="sxs-lookup"><span data-stu-id="1106f-155">Only one entry appears in hello ARP table.</span></span> <span data-ttu-id="1106f-156">Il montre le mappage hello entre hello adresse MAC et hello IP utilisé sur hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1106f-156">It shows hello mapping between hello MAC address and hello IP address that's used on hello Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="1106f-157">Si vous rencontrez un problème comme suit, ouvrez une prise en charge de demande avec votre tooresolve de fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="1106f-157">If you experience an issue like this, open a support request with your connectivity provider tooresolve it.</span></span>
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a><span data-ttu-id="1106f-158">Table ARP lorsque hello côté de Microsoft rencontre des problèmes</span><span class="sxs-lookup"><span data-stu-id="1106f-158">ARP table when hello Microsoft side has problems</span></span>
* <span data-ttu-id="1106f-159">Vous ne verrez pas un tableau ARP pour une homologation si des problèmes sur hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1106f-159">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span>
* <span data-ttu-id="1106f-160">Ouvrez une demande de support auprès de [Microsoft Azure - Aide + support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="1106f-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="1106f-161">Précisez que vous avez un problème au niveau de la connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="1106f-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1106f-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1106f-162">Next steps</span></span>
* <span data-ttu-id="1106f-163">Valider les configurations de couche 3 pour votre circuit ExpressRoute :</span><span class="sxs-lookup"><span data-stu-id="1106f-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="1106f-164">Obtenir un état de hello itinéraire résumé toodetermine de sessions BGP.</span><span class="sxs-lookup"><span data-stu-id="1106f-164">Get a route summary toodetermine hello state of BGP sessions.</span></span>
  * <span data-ttu-id="1106f-165">Obtenir un toodetermine de table de routage les préfixes sont publiés sur ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1106f-165">Get a route table toodetermine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="1106f-166">Valider le transfert des données en examinant les octets en entrée et en sortie.</span><span class="sxs-lookup"><span data-stu-id="1106f-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="1106f-167">Ouvrir une demande de support auprès de [Microsoft Azure - Aide + support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) si vous rencontrez encore des problèmes.</span><span class="sxs-lookup"><span data-stu-id="1106f-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

