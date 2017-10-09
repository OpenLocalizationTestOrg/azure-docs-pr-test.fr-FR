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
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a>Mise en route ARP tables dans le modèle de déploiement classique de hello
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - Classique](expressroute-troubleshooting-arp-classic.md)
> 
> 

Cet article vous guide tout au long des étapes hello pour l’obtention des tables du protocole ARP (Address Resolution) hello pour votre circuit ExpressRoute d’Azure.

> [!IMPORTANT]
> Ce document est prévue toohelp vous diagnostiquez et résoudre les problèmes de simples. Il n’est pas prévue toobe un remplacement pour le support technique de Microsoft. Si vous ne pouvez pas résoudre les problème de hello à l’aide de hello suivant recommandations, ouvrez une demande de support avec [Microsoft Azure aide + support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Protocole ARP (Address Resolution Protocol) et tables ARP
ARP est un protocole de couche 2 défini dans [RFC 826](https://tools.ietf.org/html/rfc826). ARP est toomap utilisé une Ethernet (adresse MAC) tooan adresse IP.

Une table ARP fournit un mappage d’adresse IPv4 de hello et une adresse MAC pour une homologation particulier. Hello table ARP d’un circuit ExpressRoute d’homologation fournit hello informations pour chaque interface (principal et secondaire) suivantes :

1. Mappage d’une adresse MAC de local routeur interface IP adresse tooa
2. Mappage d’une adresse MAC de ExpressRoute routeur interface IP adresse tooa
3. âge Hello du mappage de hello

Les tables ARP permettent de valider la configuration de la couche 2 et de résoudre les problèmes de connectivité de base de la couche 2.

Vous trouverez ci-dessous un exemple de table ARP :

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Hello suivant la section fournit des informations sur comment tooview hello tables ARP vus par les routeurs de périphérie hello ExpressRoute.

## <a name="prerequisites-for-using-arp-tables"></a>Conditions préalables à l’utilisation des tables ARP
Vérifiez que vous disposez des éléments suivants de hello avant de continuer :

* Un circuit ExpressRoute valide configuré avec au moins une homologation. circuit de Hello doit être entièrement configuré par le fournisseur de connectivité hello. Vous (ou votre fournisseur de connectivité) devez configurer au moins un des homologations hello (public Azure de privé, Azure, ou Microsoft) sur ce circuit.
* Plages d’adresses IP qui sont utilisées pour la configuration des homologations hello (public Azure de privé, Azure et Microsoft). Passez en revue les exemples de l’attribution d’adresses hello IP Bonjour [page de spécifications de routage ExpressRoute](expressroute-routing.md) tooget une compréhension de la façon dont les adresses IP sont mappées toointerfaces sur votre aise et hello ExpressRoute côté. Vous pouvez obtenir des informations sur la configuration d’homologation de hello en examinant hello [page de configuration d’homologation ExpressRoute](expressroute-howto-routing-classic.md).
* Informations à partir de votre fournisseur d’équipe ou de la connectivité réseau sur des adresses MAC hello des interfaces de hello sont utilisées avec ces adresses IP.
* Hello dernier module Windows PowerShell pour Azure (version 1.50 ou ultérieure).

## <a name="arp-tables-for-your-expressroute-circuit"></a>Tables ARP pour votre circuit ExpressRoute
Cette section fournit des instructions sur la façon dont les tables tooview hello ARP pour chaque type d’homologation à l’aide de PowerShell. Avant de continuer, vous ou votre fournisseur de connectivité doit d’homologation de hello tooconfigure. Chaque circuit a deux chemins d’accès (principal et secondaire). Vous pouvez vérifier hello table ARP pour chaque chemin d’accès indépendamment.

### <a name="arp-tables-for-azure-private-peering"></a>Tables ARP pour l’homologation privée Azure
Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation privée Azure :

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

Voici un exemple de sortie pour un des chemins d’accès hello :

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Tables ARP pour l’homologation publique Azure :
Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation publique Azure :

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

Voici un exemple de sortie pour un des chemins d’accès hello :

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Voici un exemple de sortie pour un des chemins d’accès hello :

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Tables ARP pour l’homologation Microsoft
Hello suivant l’applet de commande fournit hello ARP tables pour l’homologation de Microsoft :

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


Exemple de sortie est illustrée ci-dessous pour un des chemins d’accès hello :

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Comment toouse ces informations
Hello table ARP d’une homologation peut être la connectivité et la configuration de la couche 2 de toovalidate utilisé. Cette section fournit une vue d’ensemble de l’aspect des tables ARP dans différents scénarios.

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a>Table ARP lorsqu’un circuit est à l’état opérationnel (attendu)
* Hello table ARP possède une entrée pour le côté local de hello avec une adresse IP et MAC valide et une entrée similaire pour hello côté de Microsoft.
* Hello dernier octet de l’adresse IP de local hello est toujours un nombre impair.
* Hello dernier octet de hello adresse IP de Microsoft est toujours un nombre pair.
* Hello même adresse MAC s’affiche sur hello côté Microsoft pour tous les homologations de trois (principal/secondaire).

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a>Table ARP lorsqu’il est sur site ou lorsque le côté du fournisseur de connectivité hello rencontre des problèmes
 Qu’une seule entrée apparaît dans la table ARP de hello. Il montre le mappage hello entre hello adresse MAC et hello IP utilisé sur hello côté de Microsoft.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> Si vous rencontrez un problème comme suit, ouvrez une prise en charge de demande avec votre tooresolve de fournisseur de connectivité.
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a>Table ARP lorsque hello côté de Microsoft rencontre des problèmes
* Vous ne verrez pas un tableau ARP pour une homologation si des problèmes sur hello côté de Microsoft.
* Ouvrez une demande de support auprès de [Microsoft Azure - Aide + support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Précisez que vous avez un problème au niveau de la connectivité de couche 2.

## <a name="next-steps"></a>Étapes suivantes
* Valider les configurations de couche 3 pour votre circuit ExpressRoute :
  * Obtenir un état de hello itinéraire résumé toodetermine de sessions BGP.
  * Obtenir un toodetermine de table de routage les préfixes sont publiés sur ExpressRoute.
* Valider le transfert des données en examinant les octets en entrée et en sortie.
* Ouvrir une demande de support auprès de [Microsoft Azure - Aide + support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) si vous rencontrez encore des problèmes.

