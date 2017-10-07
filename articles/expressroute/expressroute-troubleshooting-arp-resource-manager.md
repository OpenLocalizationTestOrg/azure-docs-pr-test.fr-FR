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
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a>Mise en route ARP tables dans le modèle de déploiement du Gestionnaire de ressources hello
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - Classique](expressroute-troubleshooting-arp-classic.md)
> 
> 

Cet article vous guide tout au long de hello de toolearn étapes hello QU'ARP tables votre circuit ExpressRoute. 

> [!IMPORTANT]
> Ce document est prévue toohelp vous diagnostiquez et résoudre les problèmes de simples. Il n’est pas prévue toobe un remplacement pour le support technique de Microsoft. Vous devez ouvrir un ticket de support avec [prise en charge de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) en cas de problème de hello toosolve impossible à l’aide d’instructions hello décrites ci-dessous.
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Protocole ARP (Address Resolution Protocol) et tables ARP
Le protocole ARP (Address Resolution Protocol) est un protocole de couche 2 défini dans [RFC 826](https://tools.ietf.org/html/rfc826). ARP est utilisé toomap hello Ethernet (adresse MAC) avec une adresse ip.

Hello table ARP fournit un mappage d’adresse ipv4 de hello et une adresse MAC pour une homologation particulier. Hello table ARP d’un circuit ExpressRoute d’homologation fournit hello suivant des informations pour chaque interface (principal et secondaire)

1. Mappage d’adresse MAC de local routeur interface ip adresse toohello
2. Mappage d’adresse MAC de ExpressRoute routeur interface ip adresse toohello
3. Durée de vie de mappage de hello

Les tables ARP permettent de valider la configuration de la couche 2 et de résoudre les problèmes de connectivité de base de la couche 2. 

Exemple de table ARP : 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


Hello section suivante fournit des informations sur la façon dont vous pouvez afficher hello tables ARP visibles par les routeurs de périphérie hello ExpressRoute. 

## <a name="prerequisites-for-learning-arp-tables"></a>Conditions préalables à l’apprentissage des tables ARP
Assurez-vous d’avoir hello suivant avant de vous davantage de progression

* Un circuit ExpressRoute valide configuré avec au moins une homologation. circuit de Hello doit être entièrement configuré par le fournisseur de connectivité hello. Vous (ou votre fournisseur de connectivité) doit avoir configuré au moins un des homologations hello (public Azure de privé, Azure et Microsoft) sur ce circuit.
* Plages d’adresses IP utilisées pour la configuration des homologations hello (public Azure de privé, Azure et Microsoft). Passez en revue les exemples de l’attribution d’adresses hello ip Bonjour [page de spécifications de routage ExpressRoute](expressroute-routing.md) tooget une compréhension de la façon dont les adresses ip sont mappées toointerfaces votre côté et hello ExpressRoute côté. Vous pouvez obtenir des informations sur la configuration d’homologation hello en examinant hello [page de configuration d’homologation ExpressRoute](expressroute-howto-routing-arm.md).
* Pour plus d’informations à partir de votre équipe réseau / fournisseur de connectivité sur des adresses MAC hello des interfaces utilisées avec ces adresses IP.
* Vous devez disposer du module PowerShell plus récent hello pour Azure (version 1,50 ou une version ultérieure).

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a>Obtention de tables hello ARP votre circuit ExpressRoute
Cette section fournit des instructions sur la façon dont vous pouvez afficher hello tables ARP par homologation à l’aide de PowerShell. Vous ou votre fournisseur de connectivité doit avoir configuré hello d’homologation avant de poursuivre. Chaque circuit a deux chemins d’accès (principal et secondaire). Vous pouvez vérifier hello table ARP pour chaque chemin d’accès indépendamment.

### <a name="arp-tables-for-azure-private-peering"></a>Tables ARP pour l’homologation privée Azure
Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation privée Azure

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

Exemple de sortie est illustrée ci-dessous pour un des chemins d’accès hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Tables ARP pour l’homologation publique Azure
Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation publique Azure

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


Exemple de sortie est illustrée ci-dessous pour un des chemins d’accès hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Tables ARP pour l’homologation Microsoft
Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation de Microsoft

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


Exemple de sortie est illustrée ci-dessous pour un des chemins d’accès hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Comment toouse ces informations
Hello table ARP d’une homologation peut servir toodetermine valider la configuration de la couche 2 et la connectivité. Cette section fournit une vue d’ensemble de l’aspect des tables ARP dans différents scénarios.

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a>Table ARP lorsqu’un circuit est dans un état opérationnel (état attendu)
* Hello table ARP aura une entrée pour le côté local de hello avec une adresse IP valide et une adresse MAC et une entrée similaire pour hello côté de Microsoft. 
* dernier octet de Hello d’adresse ip de local hello sera toujours un nombre impair.
* Hello dernier octet de hello adresse ip de Microsoft sera toujours un nombre pair.
* Hello même adresse MAC apparaîtront sur hello côté Microsoft pour tous les 3 homologations (principales / secondaire). 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a>Table ARP en cas de problèmes côté fournisseur de connectivité/local
Si des problèmes avec hello localement ou fournisseur de connectivité peuvent apparaître qu’une seule entrée sera Bonjour ARP table ou hello local MAC adresse affichera incomplète. Cette opération affiche le mappage hello entre hello adresse MAC et l’adresse IP utilisée dans hello côté de Microsoft. 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

ou
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> Ouvrez une demande de support avec votre toodebug de fournisseur de connectivité de tels problèmes. Si hello table ARP ne dispose pas des adresses IP des interfaces de hello mappé tooMAC adresses, hello révision informations suivantes :
> 
> 1. Si hello première adresse IP du sous-réseau de hello /30 affecté pour la liaison hello entre hello MSEE-PR et MSEE est utilisé sur l’interface hello de MSEE-PR. Azure utilise toujours l’adresse IP de la deuxième hello pour MSEEs.
> 2. Vérifiez si le client hello (C-Tag) et balises VLAN de service (S-Tag) correspondent à la fois sur la paire de MSEE-PR et MSEE.
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a>Table ARP en cas de problèmes côté Microsoft
* Vous ne verrez pas un tableau ARP pour une homologation si des problèmes sur hello côté de Microsoft. 
* Ouvrez un incident auprès du [support technique Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Spécifiez que vous avez un problème au niveau de la connectivité de couche 2. 

## <a name="next-steps"></a>Étapes suivantes
* Valider les configurations de couche 3 pour votre circuit ExpressRoute
  * Obtention de l’itinéraire résumé toodetermine hello état de sessions BGP 
  * Obtenir toodetermine de table de routage les préfixes sont publiés sur ExpressRoute
* Valider le transfert des données en examinant les octets en entrée/sortie
* Ouvrez un ticket de support auprès du [support Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) si vous rencontrez encore des problèmes.

