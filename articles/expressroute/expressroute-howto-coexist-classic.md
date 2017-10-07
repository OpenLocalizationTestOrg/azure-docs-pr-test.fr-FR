---
title: "Configuration de connexions ExpressRoute et VPN de site à site pouvant coexister : classique : Azure | Microsoft Docs"
description: "Cet article vous guide dans la configuration d’une connexion VPN de Site à Site qui peut coexister pour le modèle de déploiement classique hello et ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a>Configurer la coexistence de connexions de site à site et ExpressRoute (classique)
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - Classique](expressroute-howto-coexist-classic.md)
> 
> 

Ayant la possibilité de hello tooconfigure VPN de Site à Site et ExpressRoute présente plusieurs avantages. Vous pouvez configurer un VPN de Site à Site comme un chemin d’accès sécurisé de basculement pour ExressRoute, ou utiliser des VPN de Site à Site tooconnect toosites qui ne sont pas connectés via ExpressRoute. Les deux scénarios dans cet article, nous allons aborder hello étapes tooconfigure. Cet article concerne le modèle de déploiement classique toohello. Cette configuration n’est pas disponible dans le portail de hello.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**À propos des modèles de déploiement Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> Circuits ExpressRoute doivent être préconfigurés avant de suivre les instructions hello ci-dessous. Assurez-vous que vous avez suivi les guides hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et [configurer le routage](expressroute-howto-routing-classic.md) avant de suivre les étapes de hello ci-dessous.
> 
> 

## <a name="limits-and-limitations"></a>Limites et limitations
* **Le routage de transit n’est pas pris en charge.** Vous ne pouvez effectuer de routage (via Azure) entre votre réseau local connecté via le réseau VPN de site à site et votre réseau local connecté via ExpressRoute.
* **Le routage point à site n’est pas pris en charge.** Vous ne pouvez pas activer le point-to-site VPN connexions toohello même réseau virtuel qui est connecté tooExpressRoute. Point-to-site VPN et ExpressRoute ne peuvent pas coexister pour hello même réseau virtuel.
* **Le tunneling forcé ne peut pas être activé sur la passerelle VPN de Site à Site hello.** Vous pouvez uniquement « forcer » tous les Internet liées au trafic tooyour arrière sur réseau local via ExpressRoute.
* **La passerelle de référence de base n’est pas prise en charge.** Vous devez utiliser une passerelle de base SKU pour les deux hello [passerelle ExpressRoute](expressroute-about-virtual-network-gateways.md) et hello [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Seule la passerelle VPN basée sur un itinéraire est prise en charge.** Vous devez utiliser une [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) basée sur un itinéraire.
* L’**itinéraire statique doit être configuré pour votre passerelle VPN.** Si votre réseau local est connecté tooboth ExpressRoute et un Site à Site VPN, vous devez disposer un itinéraire statique configuré dans votre toohello de connexion de réseau local tooroute hello Site-à-Site VPN Internet public.
* La **passerelle ExpressRoute doit être configurée en premier.** Vous devez d’abord créer passerelle ExpressRoute de hello avant d’ajouter de la passerelle VPN de Site à Site hello.

## <a name="configuration-designs"></a>Modèles de configuration
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Configurer un réseau VPN de site à site comme un chemin d’accès de basculement pour ExpressRoute
Vous pouvez configurer une connexion VPN de site à site en tant que sauvegarde pour ExpressRoute. Cela s’applique uniquement toovirtual réseaux lié toohello chemin d’accès d’homologation privée Azure. Il n’existe aucune solution de basculement basée sur des réseaux VPN pour les services accessibles via les homologations Azure public et Microsoft. lien principal de hello est toujours Hello circuit ExpressRoute. Flux de données via un chemin d’accès de Site à Site VPN hello uniquement si hello circuit ExpressRoute échoue. 

> [!NOTE]
> Alors que le circuit ExpressRoute est préférable à VPN de Site à Site lorsque les deux itinéraires sont hello même, Azure utilisera itinéraire de hello plus long préfixe correspondance toochoose hello vers la destination du paquet hello.
> 
> 

![Coexister](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Configurer un toosites tooconnect VPN de Site à Site ne pas connecté via ExpressRoute
Vous pouvez configurer votre réseau où certains sites connectent directement tooAzure via le VPN de Site à Site, et certains sites via ExpressRoute. 

![Coexister](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> Vous ne pouvez pas configurer un réseau virtuel comme un routeur de transit.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>En sélectionnant hello étapes toouse
Il existe deux ensembles différents de toochoose procédures à partir de connexions de tooconfigure de commande peuvent coexister. procédure de configuration Hello que vous sélectionnez dépend si vous disposez d’un réseau virtuel existant que vous souhaitez tooconnect à, ou que vous voulez toocreate un réseau virtuel.

* Je ne disposer d’un réseau virtuel et devez toocreate une.
  
    Si vous n’avez pas déjà un réseau virtuel, cette procédure vous guidera création d’un réseau virtuel à l’aide du modèle de déploiement classique hello et la création de nouvelles connexions VPN de Site à Site et ExpressRoute. tooconfigure, suivez les étapes dans la section de l’article hello hello [toocreate un nouveau réseau virtuel et les connexions de coexistence](#new).
* J’ai déjà un réseau virtuel répondant au modèle de déploiement classique
  
    Vous disposez peut-être déjà d’un réseau virtuel avec une connexion VPN de site à site existante ou une connexion ExpressRoute. Hello section article [tooconfigure coexsiting les connexions pour un réseau virtuel existant déjà](#add) vous guide dans la suppression de la passerelle de hello et la création de nouvelles connexions VPN de Site à Site et ExpressRoute. Notez que lors de la création de nouvelles connexions hello, les étapes de hello doivent être effectuées dans un ordre spécifique. N’utilisez pas les instructions hello dans d’autres articles de toocreate vos passerelles et les connexions.
  
    Dans cette procédure, la création de connexions peuvent coexister sera requièrent que vous toodelete votre passerelle, puis configurez nouvelles passerelles. Cela signifie que vous devrez temps mort pour les connexions entre différents locaux pendant que vous supprimez et recréez la passerelle et les connexions, mais vous n’aurez pas toomigrate un de vos machines virtuelles ou services tooa nouveau réseau virtuel. Vos machines virtuelles et les services seront toujours en mesure de toocommunicate sortantes via l’équilibrage de charge hello lorsque vous configurez votre passerelle s’ils ne sont donc toodo configuré.

## <a name="new"></a>toocreate un nouveau réseau virtuel et la coexistence de connexions
Cette procédure vous guide dans la création d’un réseau virtuel et dans l’établissement de nouvelles connexions de site à site et ExpressRoute appelées à coexister.

1. Vous devez tooinstall hello dernière version de hello applets de commande PowerShell de Azure. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello. Notez que les applets de commande hello que vous allez utiliser pour cette configuration peut être légèrement différente de celle que vous connaissez peut-être. Applets de commande hello toouse vraiment être spécifié dans ces instructions. 
2. Créez un schéma pour votre réseau virtuel. Pour plus d’informations sur le schéma de configuration hello, consultez [schéma de configuration de réseau virtuel Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   
    Lorsque vous créez votre schéma, assurez-vous que vous utilisez hello valeurs suivantes :
   
   * sous-réseau de passerelle de Hello pour hello du réseau virtuel doit être /27 ou un préfixe plus court (par exemple, /26 ou /25).
   * type de connexion de passerelle Hello est « dédié ».
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. Après la création et la configuration de votre fichier de schéma xml, téléchargez les fichiers hello. Cette opération crée votre réseau virtuel.
   
    Utilisez hello suivant tooupload de l’applet de commande de votre fichier, en remplaçant la valeur de hello avec vos propres.
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw"></a>Créez une passerelle ExpressRoute. Être toospecify vraiment hello GatewaySKU comme *Standard*, *hautes performances*, ou *UltraPerformance* et hello le type de passerelle en tant que *DynamicRouting*.
   
    Utilisez hello suivant l’exemple, en remplaçant les valeurs hello pour votre propre.
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. Lier le circuit ExpressRoute toohello hello ExpressRoute passerelle. Une fois cette étape terminée, hello entre votre réseau local et le Azure via ExpressRoute, est établie.
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a>Créez ensuite la passerelle VPN de site à site. Hello GatewaySKU doit être *Standard*, *hautes performances*, ou *UltraPerformance* et hello le type de passerelle doit être *DynamicRouting*.
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    paramètres de passerelle de réseau virtuel hello tooretrieve, y compris l’ID de passerelle hello et adresse IP publique hello, utilisent hello `Get-AzureVirtualNetworkGateway` applet de commande.
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. Créez une entité de passerelle VPN de site local. Cette commande ne configure pas votre passerelle VPN locale. Au lieu de cela, il vous permet de paramètres de la passerelle locale hello tooprovide, telles que des adresses IP publiques de hello et hello localement l’espace d’adressage, afin que hello passerelle VPN Azure peut se connecter tooit.
   
   > [!IMPORTANT]
   > site local de Hello pour hello VPN de Site à Site n’est pas défini dans le fichier netcfg de hello. Au lieu de cela, vous devez utiliser ce paramètres de site local cmdlet toospecify hello. Vous ne pouvez pas définir à l’aide du portail ou fichier netcfg de hello.
   > 
   > 
   
    Utilisez hello suivant l’exemple, en remplaçant les valeurs hello par les vôtres.
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > Si votre réseau local possède plusieurs itinéraires, vous pouvez tous les transmettre sous la forme d’un tableau.  $MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")  
   > 
   > 

    paramètres de passerelle de réseau virtuel hello tooretrieve, y compris l’ID de passerelle hello et adresse IP publique hello, utilisent hello `Get-AzureVirtualNetworkGateway` applet de commande. Consultez hello l’exemple suivant.

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. Configurez votre passerelle VPN locale appareil tooconnect toohello nouveau. Utilisez les informations de hello que vous avez récupéré à l’étape 6 lors de la configuration de votre périphérique VPN. Pour plus d’informations sur la configuration du périphérique VPN, consultez la rubrique [Configuration de périphérique VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
2. Passerelle VPN de Site à Site du hello lien sur la passerelle locale toohello Azure.
   
    Dans cet exemple, connectedEntityId est ID de passerelle locale hello, qui se trouve en exécutant `Get-AzureLocalNetworkGateway`. Vous pouvez trouver virtualNetworkGatewayId à l’aide de hello `Get-AzureVirtualNetworkGateway` applet de commande. Après cette étape, hello entre votre réseau local et Azure via hello connexion VPN de Site à Site est établie.

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a>connexions de coexsiting tooconfigure pour un réseau virtuel existant
Si vous avez un réseau virtuel existant, vérifiez la taille de sous-réseau de passerelle hello. Si le sous-réseau de passerelle hello est /28 ou /29, vous devez tout d’abord supprimer la passerelle de réseau virtuel hello et augmenter la taille de sous-réseau de passerelle hello. Hello étapes décrites dans cette section vous indiquent comment toodo qui.

Si le sous-réseau de passerelle hello est /27 ou supérieure et réseau virtuel de hello est connecté via ExpressRoute, vous pouvez ignorer les étapes hello ci-dessous et continuer trop[« Étape 6 : créer une passerelle VPN de Site à Site »](#vpngw) dans la section précédente de hello.

> [!NOTE]
> Lorsque vous supprimez la passerelle existante de hello, votre site local perdrez réseau virtuel de hello connexion tooyour lorsque vous travaillez sur cette configuration.
> 
> 

1. Vous devez la version la plus récente hello tooinstall Hello applets de commande PowerShell de gestionnaire de ressources Azure. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello. Notez que les applets de commande hello que vous allez utiliser pour cette configuration peut être légèrement différente de celle que vous connaissez peut-être. Applets de commande hello toouse vraiment être spécifié dans ces instructions. 
2. Supprimer la passerelle hello ExpressRoute ou VPN de Site à Site existante. Utilisez hello suivant l’applet de commande, en remplaçant les valeurs hello par les vôtres.
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. Exporter le schéma de réseau virtuel hello. Utilisez hello suivant l’applet de commande PowerShell, en remplaçant les valeurs hello par les vôtres.
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. Modifier le schéma de fichier de configuration de réseau hello afin que le sous-réseau de passerelle hello est /27 ou un préfixe plus court (par exemple, /26 ou /25). Consultez hello l’exemple suivant. 
   
   > [!NOTE]
   > Si vous n’avez pas suffisamment d’adresses IP dans votre taille de sous-réseau de passerelle de réseau virtuel tooincrease hello, vous devez tooadd plus d’espace d’adressage IP. Pour plus d’informations sur le schéma de configuration hello, consultez [schéma de configuration de réseau virtuel Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. Si votre passerelle précédente était un VPN de Site à Site, vous devez également modifier type de connexion hello trop**dédié**.
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. À ce stade, vous disposez d’un réseau virtuel sans passerelles. toocreate nouvelles passerelles et vos connexions, vous pouvez poursuivre [étape 4 : créer une passerelle ExpressRoute](#gw), située dans hello précédant l’ensemble d’étapes.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md)

