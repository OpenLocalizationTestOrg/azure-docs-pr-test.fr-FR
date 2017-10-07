---
title: "itinéraires aaaTroubleshoot - PowerShell | Documents Microsoft"
description: "Découvrez comment tootroubleshoot route dans le modèle de déploiement hello Azure Resource Manager à l’aide d’Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a>Résoudre des problèmes d’itinéraires à l’aide d’Azure PowerShell
> [!div class="op_single_selector"]
> * [Portail Azure](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

Si vous rencontrez tooor de problèmes de connectivité réseau à partir de votre Machine virtuelle (VM) Azure, itinéraires affecte votre flux de trafic de machine virtuelle. Cet article fournit une vue d’ensemble des fonctionnalités des diagnostics pour les itinéraires toohelp dépannage.

Des tables d’itinéraires sont associées aux sous-réseaux, qui s’appliquent à toutes les interfaces réseau de ce sous-réseau. Hello les types d’itinéraires suivants peut être l’interface de réseau tooeach appliqué :

* **Itinéraires système :** par défaut, chaque sous-réseau créé dans un réseau virtuel Azure a des tables d’itinéraires système qui permettent le trafic de réseau virtuel local, le trafic local au moyen de passerelles VPN et le trafic Internet. Il existe également des itinéraires système pour les réseaux virtuels homologués.
* **Itinéraires BGP :** propagées interfaces toonetwork via ExpressRoute ou les connexions VPN site à site. En savoir plus sur le routage BGP en lisant hello [BGP avec les passerelles VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) et [présentation ExpressRoute](../expressroute/expressroute-introduction.md) articles.
* **Itinéraires définis par l’utilisateur (UDR) :** si vous utilisez les dispositifs réseau virtuel ou sont-tunneling forcé réseau local du tooan le trafic via un VPN de site à site, vous pouvez avoir des itinéraires définis par l’utilisateur (UDRs) associés à votre table d’itinéraires de sous-réseau. Si vous n’êtes pas familiarisé avec UDRs, lecture hello [itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md#user-defined-routes) l’article.

Hello itinéraires différents qui peuvent être appliqués tooa interface de réseau, il peut être difficile toodetermine les itinéraires d’agrégation sont efficaces. toohelp dépanner la connectivité de réseau d’ordinateurs virtuels, vous pouvez afficher tous les itinéraires effectifs hello pour une interface réseau dans le modèle de déploiement du Gestionnaire de ressources Azure hello.

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a>À l’aide de flux de trafic d’itinéraires effectifs tootroubleshoot machine virtuelle
Cet article utilise hello suivant le scénario comme une tooillustrate exemple comment tootroubleshoot hello effective route pour une interface réseau :

Une machine virtuelle (*VM1*) connecté toohello réseau virtuel (*VNet1*, préfixe : 10.9.0.0/16) échoue tooconnect tooa VM(VM3) dans un réseau virtuel qui vient d’être ressources (*VNet3*, 10.10.0.0/16 du préfixe). Il y a aucune UDRs ou le protocole BGP n’achemine appliqué tooVM1-NIC1 network interface connectée toohello VM uniquement les itinéraires système sont appliquées.

Cet article explique comment toodetermine hello provoquer d’erreur de connexion hello, à l’aide de la fonctionnalité d’itinéraires effectifs dans un modèle de déploiement de gestion des ressources Azure.
Alors que hello exemple utilise uniquement les itinéraires système, hello les mêmes étapes peut être utilisé toodetermine échecs de connexion entrant et sortant sur n’importe quel type d’itinéraire.

> [!NOTE]
> Si votre machine virtuelle possède plusieurs cartes réseau attachée, vérifiez itinéraires effectifs pour chacun des hello toodiagnose NIC tooand du problèmes de connectivité de réseau à partir d’une machine virtuelle.
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a>Afficher les itinéraires effectifs pour une machine virtuelle
toosee hello agrégation itinéraires qui sont appliqué tooa machine virtuelle, hello complète comme suit :

### <a name="view-effective-routes-for-a-network-interface"></a>Afficher les itinéraires effectifs pour une interface réseau
toosee hello agrégation itinéraires qui sont appliqués tooa interface de réseau, hello complète comme suit :

1. Démarrer un tooAzure de session et de connexion Azure PowerShell. Si vous n’êtes pas familiarisé avec Azure PowerShell, lire hello [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.
2. Hello commande ci-dessous retourne interface réseau tooa tous les itinéraires appliquées nommé *NIC1 de VM1* dans le groupe de ressources hello *RG1*.
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Si vous ne connaissez pas nom hello d’une interface réseau, tapez Bonjour commande tooretrieve hello nom de toutes les interfaces réseau dans un group.* de ressources
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   Hello sortie suivante recherche une sortie similaire toohello chaque hello de sous-réseau itinéraire appliqué toohello à que carte réseau est connectée :
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   Notez suivant hello dans la sortie de hello :
   
   * **Nom**: nom de l’itinéraire effectif de hello peut être vide, sauf mention spéciale, itinéraires définis par l’utilisateur. 
   * **État**: indique l’état de l’itinéraire effectif de hello. Les valeurs possibles sont « Actif » ou « Non valide ».
   * **AddressPrefixes**: Spécifie le préfixe d’adresse hello de l’itinéraire effectif de hello en notation CIDR. 
   * **type de tronçon suivant**: indique le saut suivant hello hello donnée d’itinéraire. Les valeurs possibles sont *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* ou *Null*. La valeur *Null* pour **nextHopType** dans un itinéraire défini par l’utilisateur peut indiquer un itinéraire non valide. Par exemple, si **nextHopType** est *VirtualAppliance* et hello network appliance virtuelle machine virtuelle n’est pas dans un état de mise en service en cours d’exécution. Si **nextHopType** est *VPNGateway* et qu’aucune passerelle mis en service en cours d’exécution dans hello réseau virtuel donné, les itinéraires hello peuvent devenir non valides.
   * **NextHopIpAddress**: Spécifie l’adresse IP de hello du tronçon suivant de hello de l’itinéraire effectif de hello.
   
   Hello commande ci-dessous retourne les itinéraires hello dans une table tooview plus facile :
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   Hello de sortie suivant est certaines de sortie hello reçue pour le scénario hello décrit précédemment :
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. Il n’existe aucun toohello itinéraire répertorié *WestUS-VNet3* réseau virtuel (10.10.0.0/16)** à partir du préfixe *WestUS-VNet1* (préfixe 10.9.0.0/16) dans la sortie de hello à partir de l’étape précédente de hello. Comme indiqué dans hello illustration suivante, hello lien d’homologation du réseau virtuel avec hello *WestUS-VNet3* réseau virtuel est Bonjour *Disconnected* état.
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    lien de Hello bidirectionnel pour hello d’homologation est rompue, qui explique pourquoi VM1 pas pu se connecter tooVM3 Bonjour *WestUS-VNet3* réseau virtuel. Configurez de nouveau un lien VNET Peering bidirectionnel pour les réseaux virtuels *WestUS-VNet1* et *WestUS-VNet3*. sortie Hello retourné après que le lien d’homologation du réseau virtuel hello est correctement établie :
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    Après avoir déterminé le problème de hello, vous pouvez ajouter, supprimer, ou modifier des routes et tables d’itinéraires. Hello du type suivant de commande toosee une liste des commandes hello utilisé toodo ainsi :
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a>Considérations
Quelques tookeep choses à l’esprit lorsque vous parcourez la liste hello des itinéraires retourné :

* Les itinéraires sont basés sur la correspondance de préfixe la plus longue parmi les itinéraires définis par l’utilisateur, BGP et système. S’il existe plusieurs itinéraires avec hello même locales correspondent, alors un itinéraire est sélectionné en fonction de son origine dans hello suivant l’ordre :
  
  * Itinéraire défini par l’utilisateur
  * Itinéraire BGP
  * Itinéraire système (par défaut)
    
    Avec les itinéraires effectifs, vous pouvez uniquement afficher les itinéraires effectifs qui correspondent au Gestionnaire de stratégies locales en fonction de tous les itinéraires de disponible hello. En affichant la manière dont les itinéraires hello sont en réalité évalués pour une carte réseau donnée, il est ainsi beaucoup plus facile tootroubleshoot des itinéraires spécifiques qui affecte la connectivité à partir de votre machine virtuelle.
* Si vous avez UDRs et que vous envoyez appliance virtuelle du trafic tooa réseau (NVA), avec *VirtualAppliance* en tant que **tronçon suivant**, vérifiez que le transfert IP est activé sur le trafic hello réception hello NVA ou les paquets sont ignorés. 
* Si le tunneling forcé est activé, tout le trafic Internet sortant sera routé tooon local. RDP/SSH à partir de tooyour Internet que machine virtuelle peut ne pas fonctionne avec ce paramètre, en fonction de comment hello local gère ce trafic. 
  Le tunneling forcé peut être activé :
  * si vous utilisez un VPN de site à site, en établissant un itinéraire défini par l’utilisateur avec nextHopType en tant que passerelle VPN ;
  * si un itinéraire par défaut est annoncé sur BGP.
* Pour le réseau virtuel d’homologation du trafic toowork correctement, un itinéraire de système **nextHopType** *VNetPeering* doit exister pour hello homologuer plage de préfixe de réseau virtuel. Si un itinéraire de ce type n’existe pas et hello réseau virtuel d’homologation link recherche OK :
  * Patientez quelques secondes, puis recommencez s’il s’agit d’un lien d’homologation récemment établi. Occasionnellement dure plus longtemps toopropagate itinéraires tooall hello interfaces réseau présentes dans un sous-réseau.
  * Règles du groupe de sécurité réseau (NSG) affecte les flux de trafic hello. Pour plus d’informations, consultez hello [résoudre les problèmes des groupes de sécurité réseau](virtual-network-nsg-troubleshoot-powershell.md) l’article.

