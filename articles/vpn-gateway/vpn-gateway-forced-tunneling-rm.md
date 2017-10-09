---
title: "Configurer le tunneling forcé pour les connexions de site à site - Resource Manager | Microsoft Docs"
description: "Comment tooredirect ou 'force' tous les Internet liées au trafic arrière tooyour emplacement local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>Configurer le tunneling forcé à l’aide de modèle de déploiement du Gestionnaire de ressources Azure hello

Forcé tunneling permet de rediriger ou de « forcer » tous les Internet liées au trafic tooyour arrière local emplacement via un tunnel VPN de Site à Site pour l’inspection et d’audit. Il s’agit d’une condition de sécurité critique pour la plupart des stratégies informatiques d’entreprise. Sans tunneling forcé, le trafic Internet à partir de vos machines virtuelles dans Azure toujours parcourt à partir de l’infrastructure réseau Azure directement out toohello Internet, sans hello option tooallow vous tooinspect ou audit du trafic hello. Accès Internet non autorisé peut entraîner la divulgation de tooinformation ou d’autres types de failles de sécurité.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

Cet article vous guide dans la configuration forcé tunneling pour les réseaux virtuels créés à l’aide du modèle de déploiement du Gestionnaire de ressources hello. Le tunneling forcé peut être configuré à l’aide de PowerShell, pas via le portail de hello. Si vous souhaitez tooconfigure tunneling pour le modèle de déploiement classique hello forcé, sélectionnez l’article classique hello suivant la liste déroulante :

> [!div class="op_single_selector"]
> * [PowerShell - Classique](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>À propos du tunneling forcé

Hello suivant le diagramme illustre le fonctionnement du tunneling forcé. 

![Tunneling forcé](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

Dans l’exemple hello ci-dessus, hello frontal sous-réseau n’est pas forcé en tunnel. les charges de travail Hello dans le sous-réseau du serveur frontal hello continuer tooaccept et répondre toocustomer demandes de hello Internet directement. Hello sous-réseaux de niveau intermédiaire et principaux sont forcés en tunnel. Toutes les connexions sortantes à partir de ces toohello deux sous-réseaux Internet sera forcée ou redirigée retour tooan sur site local via l’une des hello que les tunnels VPN de S2S.

Cela vous permet de toorestrict et inspecter les accès Internet à partir de vos machines virtuelles ou services cloud dans Azure, tout en continuant tooenable votre architecture de service à plusieurs niveaux requise. S’il n’y a aucune charge de travail sur Internet dans vos réseaux virtuels, vous pouvez également appliquer forcé tunneling toohello réseaux virtuels entiers.

## <a name="requirements-and-considerations"></a>Conditions requises et éléments à prendre en compte

Le tunneling forcé dans Azure est configuré via les itinéraires de réseau virtuel définis par l’utilisateur. Redirection du trafic tooan local de site est exprimé comme passerelle VPN Azure toohello itinéraire par défaut. Pour plus d’informations sur les réseaux virtuels et les itinéraires définis par l’utilisateur, consultez [Itinéraires définis par l’utilisateur et transfert IP](../virtual-network/virtual-networks-udr-overview.md).

* Chaque sous-réseau du réseau virtuel dispose d’une table de routage système intégrée. table de routage système Hello a hello trois groupes d’itinéraires suivants :
  
  * **Les itinéraires de réseau virtuel locales :** directement toohello machines virtuelles de destination Bonjour même réseau virtuel.
  * **Itinéraires locaux :** passerelle VPN Azure de toohello.
  * **L’itinéraire par défaut :** directement toohello Internet. Les paquets destinés aux toohello des adresses IP privées non couvertes par les itinéraires hello deux précédents sont supprimés.
* Cette procédure utilise des itinéraires définis par l’utilisateur (UDR) toocreate un tooadd table de routage un itinéraire par défaut, puis associer hello routage table tooyour réseau virtuel ou les sous-réseaux tooenable forcé tunneling sur ces sous-réseaux.
* Le tunneling forcé doit être associé à un réseau virtuel équipé d’une passerelle VPN avec itinéraire. Vous devez tooset un « site par défaut » entre le réseau virtuel de hello intersite sites locaux toohello connecté. En outre, hello local périphérique VPN doit être configuré à l’aide de 0.0.0.0/0 comme des sélecteurs de trafic. 
* ExpressRoute le tunneling forcé n’est pas configuré via ce mécanisme, mais au lieu de cela, est activé par annonce un itinéraire par défaut via hello BGP ExpressRoute sessions d’homologation. Pour plus d’informations, consultez hello [Documentation d’ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="configuration-overview"></a>Présentation de la configuration

Hello procédure vous permet de créer un groupe de ressources et un réseau virtuel. Vous créerez ensuite une passerelle VPN et configurerez le tunneling forcé. Dans cette procédure, réseau virtuel de hello 'MultiTier-VNet' a trois sous-réseaux : « Frontal », « Intermédiaire » et « Principal », avec quatre connexions intersites : 'DefaultSiteHQ' et trois Branches.

étapes de la procédure Hello définir hello 'DefaultSiteHQ' comme connexion de site par défaut hello pour le tunneling forcé et configurer hello « Intermédiaire » et « Backend » toouse de sous-réseaux tunneling forcé.

## <a name="before-you-begin"></a>Avant de commencer

Installer la version la plus récente hello Hello applets de commande PowerShell de gestionnaire de ressources Azure. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello.

### <a name="toolog-in"></a>toolog dans

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>Configurer un tunneling forcé

1. Créez un groupe de ressources.

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. Créez un réseau virtuel et spécifiez vos sous-réseaux.

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. Créer des passerelles de réseau local hello.

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. Créer la règle de table et d’itinéraire de routage hello.

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. Associer hello itinéraire table toohello milieu de gamme et des sous-réseaux du serveur principal.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Créez hello passerelle avec un site par défaut. Cette étape prend certaines toocomplete de temps, parfois 45 minutes ou plus, étant donné que vous créez et configurez hello passerelle.<br> Hello **- GatewayDefaultSite** est hello paramètre d’applet de commande qui permet d’hello forcé routage toowork de configuration, par conséquent, prenez soin tooconfigure ce paramètre correctement. Il est disponible uniquement dans PowerShell 1.0 ou une version ultérieure.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. Établir une connexion VPN hello Site à Site.

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```