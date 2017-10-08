---
title: "Configuration de connexions ExpressRoute et VPN de site à site pouvant coexister : Resource Manager :Azure | Microsoft Docs"
description: "Cet article vous guide tout au long de la configuration d’une connexion ExpressRoute et d’une connexion VPN de site à site pouvant coexister pour le modèle de déploiement Resource Manager."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>Configurer la coexistence de connexions de site à site et ExpressRoute
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - Classique](expressroute-howto-coexist-classic.md)
> 
> 

La configuration de connexions VPN de site à site et ExpressRoute coexistantes possède plusieurs avantages. Vous pouvez configurer un VPN de Site à Site comme un chemin d’accès sécurisé de basculement pour ExressRoute, ou utiliser des VPN de Site à Site tooconnect toosites qui ne sont pas connectés via ExpressRoute. Nous aborderons hello étapes tooconfigure les deux scénarios dans cet article. Cet article s’applique le modèle de déploiement du Gestionnaire de ressources toohello et utilise PowerShell. Cette configuration n’est pas disponible dans hello portail Azure.

> [!IMPORTANT]
> Circuits ExpressRoute doivent être préconfigurés avant de suivre les instructions hello ci-dessous. Assurez-vous que vous avez suivi les guides hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et [configurer le routage](expressroute-howto-routing-arm.md) avant de continuer.
> 
> 

## <a name="limits-and-limitations"></a>Limites et limitations
* **Le routage de transit n’est pas pris en charge.** Vous ne pouvez effectuer de routage (via Azure) entre votre réseau local connecté via le réseau VPN de site à site et votre réseau local connecté via ExpressRoute.
* **La passerelle de référence de base n’est pas prise en charge.** Vous devez utiliser une passerelle de base SKU pour les deux hello [passerelle ExpressRoute](expressroute-about-virtual-network-gateways.md) et hello [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Seule la passerelle VPN basée sur un itinéraire est prise en charge.** Vous devez utiliser une [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) basée sur un itinéraire.
* L’**itinéraire statique doit être configuré pour votre passerelle VPN.** Si votre réseau local est connecté tooboth ExpressRoute et un Site à Site VPN, vous devez disposer un itinéraire statique configuré dans votre toohello de connexion de réseau local tooroute hello Site-à-Site VPN Internet public.
* **Passerelle ExpressRoute doit être configurée en premier et lié tooa circuit.** Vous devez créez d’abord passerelle ExpressRoute de hello et liez-le tooa circuit avant d’ajouter de la passerelle VPN de hello Site-à-Site.

## <a name="configuration-designs"></a>Modèles de configuration
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Configurer un réseau VPN de site à site comme un chemin d’accès de basculement pour ExpressRoute
Vous pouvez configurer une connexion VPN de site à site en tant que sauvegarde pour ExpressRoute. Cela s’applique uniquement toovirtual réseaux lié toohello chemin d’accès d’homologation privée Azure. Il n’existe aucune solution de basculement basée sur des réseaux VPN pour les services accessibles via les homologations Azure public et Microsoft. lien principal de hello est toujours Hello circuit ExpressRoute. Les données transitent via le chemin d’accès de Site à Site VPN hello uniquement si hello circuit ExpressRoute échoue.

> [!NOTE]
> Alors que le circuit ExpressRoute est préférable à VPN de Site à Site lorsque les deux itinéraires sont hello même, Azure utilisera itinéraire de hello plus long préfixe correspondance toochoose hello vers la destination du paquet hello.
> 
> 

![Coexister](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Configurer un toosites tooconnect VPN de Site à Site ne pas connecté via ExpressRoute
Vous pouvez configurer votre réseau où certains sites connectent directement tooAzure via le VPN de Site à Site, et certains sites via ExpressRoute. 

![Coexister](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> Vous ne pouvez pas configurer un réseau virtuel comme un routeur de transit.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>En sélectionnant hello étapes toouse
Il existe deux ensembles de toochoose de procédures à partir de différents. procédure de configuration de Hello que vous sélectionnez dépend de si vous disposez d’un réseau virtuel existant que vous souhaitez tooconnect à, ou que vous voulez toocreate un réseau virtuel.

* Je ne disposer d’un réseau virtuel et devez toocreate une.
  
    Cette procédure vous guide dans la création d’un réseau virtuel si vous n’en possédez pas encore un. Elle vous demande d’utiliser le modèle de déploiement Resource Manager et de créer de nouvelles connexions ExpressRoute et VPN de site à site. tooconfigure un réseau virtuel, suivez les étapes de hello dans [toocreate un nouveau réseau virtuel et les connexions de coexistence](#new).
* J’ai déjà un réseau virtuel répondant au modèle de déploiement Resource Manager.
  
    Vous disposez peut-être déjà d’un réseau virtuel avec une connexion VPN de site à site existante ou une connexion ExpressRoute. Hello [tooconfigure de coexistence connexions pour un réseau virtuel existant déjà](#add) section vous présente la suppression de la passerelle de hello et la création de nouvelles connexions VPN de Site à Site et ExpressRoute. Lorsque vous créez hello de nouvelles connexions, les étapes de hello doivent être effectuées dans un ordre spécifique. N’utilisez pas les instructions hello dans d’autres articles de toocreate vos passerelles et les connexions.
  
    Dans cette procédure, la création de connexions peuvent coexister requiert vous toodelete votre passerelle, puis configurez les nouvelles passerelles. Vous devez les temps d’arrêt pour les connexions entre différents locaux pendant que vous supprimez et recréez la passerelle et les connexions, mais vous n’aurez pas toomigrate un de vos machines virtuelles ou services tooa nouveau réseau virtuel. Vos machines virtuelles et les services seront toujours en mesure de toocommunicate sortantes via l’équilibrage de charge hello lorsque vous configurez votre passerelle s’ils ne sont donc toodo configuré.

## <a name="new"></a>toocreate un nouveau réseau virtuel et la coexistence de connexions
Cette procédure vous guide dans la création d’un réseau virtuel et de connexions de site à site et ExpressRoute appelées à coexister.

1. Installez hello dernière version de hello applets de commande PowerShell de Azure. Pour plus d’informations sur l’installation des applets de commande hello, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). les applets de commande Hello que vous utilisez pour cette configuration peuvent être légèrement différentes de celle que vous connaissez peut-être. Applets de commande hello toouse vraiment être spécifié dans ces instructions.
2. Connectez-vous au compte de tooyour et configurer hello environnement.

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. Créez un réseau virtuel et un sous-réseau de passerelle. Pour plus d’informations sur la configuration du réseau virtuel hello, consultez [configuration de réseau virtuel Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).
   
   > [!IMPORTANT]
   > Hello sous-réseau de passerelle doit être /27 ou un préfixe plus court (par exemple, /26 ou /25).
   > 
   > 
   
    Créez un nouveau réseau virtuel.

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    Ajoutez des sous-réseaux.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Enregistrer la configuration du réseau virtuel hello.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a>Créez une passerelle ExpressRoute. Pour plus d’informations sur la configuration de passerelle ExpressRoute hello, consultez [configuration de la passerelle ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Hello GatewaySKU doit être *Standard*, *hautes performances*, ou *UltraPerformance*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. Lier le circuit ExpressRoute toohello hello ExpressRoute passerelle. Une fois cette étape terminée, hello entre votre réseau local et le Azure via ExpressRoute, est établie. Pour plus d’informations sur l’opération de liaison hello, consultez [des réseaux virtuels lien tooExpressRoute](expressroute-howto-linkvnet-arm.md).

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>Créez ensuite la passerelle VPN de site à site. Pour plus d’informations sur la configuration de passerelle VPN hello, consultez [configurer un réseau virtuel avec une connexion Site à Site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md). Hello GatewaySKU doit être *Standard*, *hautes performances*, ou *UltraPerformance*. doit Hello VpnType *RouteBased*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    La passerelle VPN Azure prend en charge le protocole de routage BGP. Vous pouvez spécifier ASN (en tant que nombre) pour ce réseau virtuel en ajoutant le commutateur - Asn de hello Bonjour commande suivante. Ne pas spécifier ce paramètre sera par défaut tooAS numéro 65515.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    Vous pouvez trouver hello BGP d’homologation IP et hello en tant que numéro que Azure utilise pour la passerelle du VPN hello dans $azureVpn.BgpSettings.BgpPeeringAddress et $azureVpn.BgpSettings.Asn. Pour plus d’informations, consultez [Configurer BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) pour la passerelle VPN Azure.
7. Créez une entité de passerelle VPN de site local. Cette commande ne configure pas votre passerelle VPN locale. Au lieu de cela, il vous permet de paramètres de la passerelle locale hello tooprovide, telles que des adresses IP publiques de hello et hello localement l’espace d’adressage, afin que hello passerelle VPN Azure peut se connecter tooit.
   
    Si votre périphérique VPN local prend uniquement en charge le routage statique, vous pouvez configurer des itinéraires statiques hello Bonjour de configuration suivant :

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Si votre périphérique VPN local prend en charge hello BGP et que vous souhaitez utiliser le routage dynamique tooenable, vous devez tooknow hello BGP d’homologation IP et hello comme numéro de votre réseau privé virtuel local qui utilise de périphérique.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. Configurez votre passerelle VPN locale appareil tooconnect toohello nouveau VPN Azure. Pour plus d’informations sur la configuration du périphérique VPN, consultez la rubrique [Configuration de périphérique VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
9. Passerelle VPN de Site à Site du hello lien sur la passerelle locale toohello Azure.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>connexions de coexistence tooconfigure pour un réseau virtuel existant
Si vous avez un réseau virtuel existant, vérifiez la taille de sous-réseau de passerelle hello. Si le sous-réseau de passerelle hello est /28 ou /29, vous devez tout d’abord supprimer la passerelle de réseau virtuel hello et augmenter la taille de sous-réseau de passerelle hello. Hello étapes décrites dans cette section vous montrent comment toodo qui.

Si le sous-réseau de passerelle hello est /27 ou supérieure et réseau virtuel de hello est connecté via ExpressRoute, vous pouvez ignorer les étapes hello ci-dessous et continuer trop[« Étape 6 : créer une passerelle VPN de Site à Site »](#vpngw) dans la section précédente de hello. 

> [!NOTE]
> Lorsque vous supprimez la passerelle existante de hello, votre site local perdrez réseau virtuel de hello connexion tooyour lorsque vous travaillez sur cette configuration. 
> 
> 

1. Vous devez tooinstall hello dernière version de hello applets de commande PowerShell de Azure. Pour plus d’informations sur l’installation des applets de commande, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). les applets de commande Hello que vous utilisez pour cette configuration peuvent être légèrement différentes de celle que vous connaissez peut-être. Applets de commande hello toouse vraiment être spécifié dans ces instructions. 
2. Supprimer la passerelle hello ExpressRoute ou VPN de Site à Site existante.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. Supprimez le sous-réseau de la passerelle.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. Ajoutez un sous-réseau de passerelle défini sur /27 ou plus.
   
   > [!NOTE]
   > Si vous n’avez pas suffisamment d’adresses IP dans votre taille de sous-réseau de passerelle de réseau virtuel tooincrease hello, vous devez tooadd plus d’espace d’adressage IP.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Enregistrer la configuration du réseau virtuel hello.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. À ce stade, vous disposez d’un réseau virtuel sans passerelle. toocreate nouvelles passerelles et vos connexions, vous pouvez poursuivre [étape 4 : créer une passerelle ExpressRoute](#gw), située dans hello précédant l’ensemble d’étapes.

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a>passerelle VPN de tooadd point-to-site configuration toohello
Vous pouvez suivre les étapes de hello ci-dessous passerelle VPN tooyour tooadd Point-to-Site configuration dans une configuration de coexistence.

1. Ajoutez le pool d’adresses des clients VPN.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. Téléchargez tooAzure de certificat racine hello VPN pour la passerelle VPN. Dans cet exemple, il est supposé que ce certificat racine de hello est stocké sur l’ordinateur local de hello où hello suivant d’applets de commande PowerShell est exécuté.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

Pour plus d’informations sur le réseau VPN point à site, consultez la rubrique [Configuration d’une connexion point à site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).
