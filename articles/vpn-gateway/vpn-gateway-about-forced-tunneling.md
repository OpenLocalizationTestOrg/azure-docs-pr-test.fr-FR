---
title: "Configurer le tunneling forcé pour les connexions de site à site Azure : modèle de déploiement classique | Microsoft Docs"
description: "Comment tooredirect ou 'force' tous les Internet liées au trafic arrière tooyour emplacement local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a>Configurer le tunneling forcé à l’aide de modèle de déploiement classique de hello

Forcé tunneling permet de rediriger ou de « forcer » tous les Internet liées au trafic tooyour arrière local emplacement via un tunnel VPN de Site à Site pour l’inspection et d’audit. Il s’agit d’une condition de sécurité critique pour la plupart des stratégies informatiques d’entreprise. Sans tunneling forcé, le trafic Internet à partir de vos machines virtuelles dans Azure traverse toujours l’infrastructure réseau Azure directement out toohello Internet, sans hello option tooallow vous tooinspect ou audit du trafic hello. Accès Internet non autorisé peut entraîner la divulgation de tooinformation ou d’autres types de failles de sécurité.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Cet article vous guide dans la configuration forcé tunneling pour les réseaux virtuels créés à l’aide du modèle de déploiement classique hello. Le tunneling forcé peut être configuré à l’aide de PowerShell, pas via le portail de hello. Si vous souhaitez tooconfigure tunneling pour le modèle de déploiement du Gestionnaire de ressources hello forcé, sélectionnez l’article classique hello suivant la liste déroulante :

> [!div class="op_single_selector"]
> * [PowerShell - Classique](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a>Conditions requises et éléments à prendre en compte
Le tunneling forcé dans Azure est configuré par le biais d’itinéraires définis par l’utilisateur de réseau virtuel. Redirection du trafic tooan local de site est exprimé comme passerelle VPN Azure toohello itinéraire par défaut. Hello section suivante répertorie les limite de hello actuelle de la table de routage hello et les itinéraires pour un réseau virtuel Azure :

* Chaque sous-réseau du réseau virtuel dispose d’une table de routage système intégrée. table de routage système Hello a hello trois groupes d’itinéraires suivants :

  * **Les itinéraires de réseau virtuel locales :** directement toohello machines virtuelles de destination Bonjour même réseau virtuel.
  * **Itinéraires locaux :** passerelle VPN Azure de toohello.
  * **L’itinéraire par défaut :** directement toohello Internet. Les paquets destinés aux toohello des adresses IP privées non couvertes par les itinéraires hello deux précédents sont supprimés.
* Avec la version hello d’itinéraires définis par l’utilisateur, vous pouvez créer un tooadd de table de routage un itinéraire par défaut et associez ensuite hello routage table tooyour réseau virtuel ou les sous-réseaux tooenable forcé tunneling sur ces sous-réseaux.
* Vous devez tooset un « site par défaut » entre le réseau virtuel de hello intersite sites locaux toohello connecté.
* Le tunneling forcé doit être associé à un réseau virtuel équipé d'une passerelle VPN à routage dynamique (pas de passerelle statique).
* ExpressRoute le tunneling forcé n’est pas configuré via ce mécanisme, mais au lieu de cela, est activé par annonce un itinéraire par défaut via hello BGP ExpressRoute sessions d’homologation. Consultez hello [Documentation d’ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) pour plus d’informations.

## <a name="configuration-overview"></a>Présentation de la configuration
Dans l’exemple suivant de hello, hello frontal sous-réseau n’est pas forcé en tunnel. les charges de travail Hello dans le sous-réseau du serveur frontal hello continuer tooaccept et répondre toocustomer demandes de hello Internet directement. Hello sous-réseaux de niveau intermédiaire et principaux sont forcés en tunnel. Toutes les connexions sortantes à partir de ces toohello deux sous-réseaux Internet sera forcée ou redirigée retour tooan sur site local via l’une des hello que les tunnels VPN de S2S.

Cela vous permet de toorestrict et inspecter les accès Internet à partir de vos machines virtuelles ou services cloud dans Azure, tout en continuant tooenable votre architecture de service à plusieurs niveaux requise. Vous pouvez également appliquer forcé tunneling toohello réseaux virtuels entiers s’il n’y aucune charge de travail sur Internet dans vos réseaux virtuels.

![Tunneling forcé](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a>Avant de commencer
Vérifiez que vous avez hello suivant d’éléments de configuration avant la configuration de début.

* Un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Un réseau virtuel configuré. 
* version la plus récente Hello Hello applets de commande PowerShell de Azure. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello.

## <a name="configure-forced-tunneling"></a>Configurer un tunneling forcé
Hello procédure vous permet de spécifier un tunneling forcé pour un réseau virtuel. les étapes de configuration de Hello correspondent toohello fichier de configuration de réseau de réseau virtuel.

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

Dans cet exemple, réseau virtuel de hello 'MultiTier-VNet' a trois sous-réseaux : sous-réseaux « Frontal », « Intermédiaire » et « Principal », avec des connexions de site entre quatre : 'DefaultSiteHQ' et trois Branches. 

étapes de Hello seront hello 'DefaultSiteHQ' en tant que connexion de site par défaut hello pour le tunneling forcé et configurez hello intermédiaire et principal sous-réseaux toouse le tunneling forcé.

1. Créez une table de routage. Utilisez hello suivant toocreate de l’applet de commande de votre table d’itinéraires.

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. Ajouter une table de routage toohello de routage par défaut. 

  Hello exemple suivant ajoute une table routage toohello itinéraire par défaut créée à l’étape 1. Notez que hello uniquement les itinéraires pris en charge est le préfixe de destination hello de « 0.0.0.0/0 » toohello saut suivant de « VPNGateway ».

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. Associer des sous-réseaux toohello table routage hello. 

  Après une table de routage est créée et un itinéraire ajouté, utilisez hello suivant exemple tooadd ou associer le sous-réseau de réseau virtuel tooa hello itinéraire table. Hello exemple ajoute hello itinéraire table « MyRouteTable » toohello intermédiaire et principaux sous-réseaux de VNet MultiTier-VNet.

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. Affectez un site par défaut pour le tunneling forcé. 

  Bonjour précédant l’étape, hello exemples applet de commande de script créé hello table de routage et associé hello itinéraire table tootwo des sous-réseaux du réseau virtuel hello. étape restante de Hello est tooselect un site local parmi les connexions de plusieurs sites hello du réseau virtuel de hello en tant que site par défaut de hello ou tunnel.

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a>Autres applets de commande PowerShell
### <a name="toodelete-a-route-table"></a>toodelete une table de routage

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a>toolist une table de routage

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a>toodelete un itinéraire à partir d’une table de routage

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a>tooremove un itinéraire à partir d’un sous-réseau

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a>table d’itinéraires hello toolist associée à un sous-réseau

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a>tooremove un site par défaut à partir d’une passerelle VPN du VNet

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```