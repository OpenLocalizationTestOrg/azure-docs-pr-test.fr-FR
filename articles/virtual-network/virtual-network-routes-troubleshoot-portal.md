---
title: "itinéraires aaaTroubleshoot - portail | Documents Microsoft"
description: "Découvrez comment les itinéraires tootroubleshoot dans le modèle de déploiement Azure Resource Manager hello d’hello portail Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a>Résoudre les problèmes des itinéraires à l’aide de hello portail Azure
> [!div class="op_single_selector"]
> * [portail Azure](virtual-network-routes-troubleshoot-portal.md)
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

1. Connexion toohello portail Azure à https://portal.azure.com.
2. Cliquez sur **davantage de services**, puis cliquez sur **virtuels** dans la liste hello qui s’affiche.
3. Sélectionnez un tootroubleshoot de machine virtuelle à partir de la liste hello qui s’affiche et un panneau de machine virtuelle avec les options s’affiche.
4. Cliquez sur **Diagnostiquer et résoudre les problèmes**, puis sélectionnez un problème courant. Pour cet exemple, **je ne peux pas me connecter toomy machine virtuelle Windows** est sélectionnée.

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. Étapes s’affichent sous le problème de hello, comme indiqué dans hello illustration suivante :

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    Cliquez sur *itinéraires effectifs* dans la liste hello des étapes recommandées.
6. Hello **itinéraires effectifs** panneau s’affiche, comme indiqué dans hello illustration suivante :

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    Si votre machine virtuelle ne comporte qu’une seule carte réseau, elle est sélectionnée par défaut. Si vous avez plusieurs cartes réseau, sélectionnez association hello pour lequel vous souhaitez les itinéraires effectifs de tooview hello.

   > [!NOTE]
   > Si hello VM associés hello carte réseau n’est pas en cours d’exécution, les itinéraires efficaces ne seront pas affichées. Uniquement hello itinéraires effectifs 200 premiers sont affichés dans le portail de hello. Pour une liste complète de hello, cliquez sur **télécharger**. Vous pouvez filtrer davantage sur les résultats à partir du fichier .csv téléchargé de hello hello.
   >
   >

    Notez suivant hello dans la sortie de hello :

   * **Source**: indique le type hello d’itinéraire. Les itinéraires système sont affichés en tant que *Default*, les itinéraires définis par l’utilisateur en tant que *User* et les itinéraires de passerelle (statiques ou BGP) en tant que *VPNGateway*.
   * **État**: indique l’état de l’itinéraire effectif de hello. Les valeurs possibles sont *Actif* ou *Non valide*.
   * **AddressPrefixes**: Spécifie le préfixe d’adresse hello de l’itinéraire effectif de hello en notation CIDR.
   * **type de tronçon suivant**: indique le saut suivant hello hello donnée d’itinéraire. Les valeurs possibles sont *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* ou *Null*. La valeur *Null* pour **nextHopType** dans un itinéraire défini par l’utilisateur peut indiquer un itinéraire non valide. Par exemple, si **nextHopType** est *VirtualAppliance* et hello network appliance virtuelle machine virtuelle n’est pas dans un état de mise en service en cours d’exécution. Si **nextHopType** est *VPNGateway* et qu’aucune passerelle mis en service en cours d’exécution dans hello réseau virtuel donné, les itinéraires hello peuvent devenir non valides.
7. Il n’existe aucun toohello itinéraire répertorié *WestUS-VNET3* réseau virtuel (préfixe 10.10.0.0/16) à partir de hello *WestUS-VNet1* (préfixe 10.9.0.0/16) dans l’image hello à l’étape précédente de hello. Bonjour illustration suivante, les liens d’homologation hello sont Bonjour *Disconnected* état :

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    lien de Hello bidirectionnel pour hello d’homologation est rompue, qui explique pourquoi VM1 pas pu se connecter tooVM3 Bonjour *WestUS-VNet3* réseau virtuel.
8. Hello image suivante montre les itinéraires hello après avoir établi le lien d’homologation hello bidirectionnel :

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

Pour des scénarios de dépannage plus pour l’évaluation de l’itinéraire et de tunneling forcé, consultez hello [considérations](virtual-network-routes-troubleshoot-portal.md#considerations) section de cet article.

### <a name="view-effective-routes-for-a-network-interface"></a>Afficher les itinéraires effectifs pour une interface réseau
Si le flux de trafic réseau est affecté pour une carte réseau particulière, vous pouvez afficher la liste complète des itinéraires effectifs sur une carte réseau directement. toosee hello agrégation itinéraires qui sont appliqué tooa NIC, hello complète comme suit :

1. Connexion toohello portail Azure à https://portal.azure.com.
2. Cliquez sur **Autres services**, puis sur **Interfaces réseau**.
3. Recherchez hello liste nom hello d’une carte réseau, ou sélectionnez-le dans la liste hello qui s’affiche. Dans cet exemple, la carte **VM1-NIC1** est sélectionnée.
4. Sélectionnez **itinéraires effectifs** Bonjour **interface réseau** panneau, comme indiqué dans hello illustration suivante :

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    Hello **étendue** interface de réseau toohello de valeurs par défaut sélectionnée.

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a>Afficher les itinéraires effectifs pour une table d’itinéraires
Lorsque vous modifiez des itinéraires définis par l’utilisateur (UDRs) dans une table de routage, vous souhaiterez impact de hello tooreview d’itinéraires hello ajouté sur un ordinateur virtuel particulier. Une table d’itinéraires peut être associée à un nombre quelconque de sous-réseaux. Vous pouvez désormais afficher tous les itinéraires efficaces hello pour tous les hello des cartes réseau qui s’applique une table de routage donné, sans avoir de contexte tooswitch hello donné du Panneau de table de routage.

Pour cet exemple, un itinéraire défini par l’utilisateur (*UDRoute*) est spécifié dans une table d’itinéraires (*UDRouteTable*). Cet itinéraire envoie tout le trafic Internet à partir de *Subnet1* Bonjour *WestUS-VNet1* réseau virtuel, via une appliance virtuelle de réseau (NVA), dans *Subnet2* de hello même réseau virtuel. itinéraire de Hello est présenté dans hello illustration suivante :

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

toosee hello d’agrégation des itinéraires pour une table de routage, hello complète comme suit :

1. Connexion toohello portail Azure à https://portal.azure.com.
2. Cliquez sur **Autres services**, puis sur **Tables d’itinéraires**.
3. Liste de hello de recherche pour la table d’itinéraires hello souhaité toosee les itinéraires d’agrégation pour et sélectionnez-le. Dans cet exemple, la table **UDRouteTable** est sélectionnée. Un panneau pour la table d’itinéraires hello sélectionné s’affiche, comme indiqué dans hello illustration suivante :

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. Sélectionnez **itinéraires effectifs** Bonjour **table d’itinéraires** panneau. Hello **étendue** a la valeur table d’itinéraires toohello vous avez sélectionné.
5. Une table de routage peut être appliqué toomultiple sous-réseaux. Sélectionnez hello **sous-réseau** vous souhaitez tooreview à partir de la liste de hello. Dans cet exemple, le sous-réseau **Subnet1** est sélectionné.
6. Sélectionnez une **Interface réseau**. Sous-réseau de toohello connecté sélectionné toutes les cartes réseau sont répertoriées. Dans cet exemple, la carte **VM1-NIC1** est sélectionnée.

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > Si hello carte réseau n’est pas associé à une machine virtuelle en cours d’exécution, aucune itinéraires effectifs ne sont affichés.
   >
   >

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
  * Règles du groupe de sécurité réseau (NSG) affecte les flux de trafic hello. Pour plus d’informations, consultez hello [résoudre les problèmes des groupes de sécurité réseau](virtual-network-nsg-troubleshoot-portal.md) l’article.
