---
title: "Se connecter à votre tooan de réseau local sur le réseau virtuel Azure : VPN de Site à Site : CLI | Documents Microsoft"
description: "Toocreate étapes une connexion IPsec à partir de votre site réseau tooan réseau virtuel Azure sur hello Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN de site à site à l’aide de l’interface de ligne de commande (CLI)."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de l’interface de ligne de commande

Cet article vous explique comment toouse hello CLI d’Azure toocreate une connexion de passerelle VPN de Site à Site à partir de votre toohello de réseau sur site réseau virtuel. étapes de Hello dans cet article s’appliquent à modèle de déploiement du Gestionnaire de ressources toohello. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :<br>

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [INTERFACE DE LIGNE DE COMMANDE](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portail Azure (classique)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

Une connexion de passerelle VPN de Site à Site est utilisé tooconnect votre site réseau tooan réseau virtuel Azure via un tunnel VPN de IPsec/IKE (IKEv1 ou IKEv2). Ce type de connexion requiert un VPN périphérique local qui a un tooit d’adresse IP publique externe. Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).

## <a name="before-you-begin"></a>Avant de commencer

Vérifiez que vous avez rempli hello suivant des critères avant de commencer la configuration :

* Assurez-vous que vous disposez d’un périphérique VPN compatible et une personne qui est en mesure de tooconfigure il. Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).
* Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN. Cette adresse IP ne peut pas se trouver derrière un NAT.
* Si vous n’êtes pas familiarisé avec les plages d’adresses IP hello situés dans configuration du réseau de votre site, vous devez toocoordinate avec une personne qui peut fournir ces informations pour vous. Lorsque vous créez cette configuration, vous devez spécifier hello plage préfixes d’adresse que Azure achemine emplacement local de tooyour. Aucun des sous-réseaux hello de votre réseau local peuvent se chevauchant avec les sous-réseaux du réseau virtuel hello tooconnect à souhaitées sur.
* Vérifiez que vous avez installé la version la plus récente des commandes CLI de hello (version 2.0 ou version ultérieure). Pour plus d’informations sur l’installation des commandes CLI de hello, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli) et [prise en main Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).

### <a name="example"></a>Exemples de valeurs

Vous pouvez utiliser hello suivant de valeurs toocreate un environnement de test, ou consultez les valeurs toothese toobetter comprendre les exemples hello dans cet article :

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <a name="Login"></a>1. Se connecter tooyour abonnement

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2. Créer un groupe de ressources

Hello exemple suivant crée un groupe de ressources nommé 'TestRG1' dans l’emplacement de 'eastus' hello. Si vous avez déjà un groupe de ressources dans la région de hello que vous voulez toocreate votre réseau virtuel, vous pouvez utiliser qu’un à la place.

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3. Créez un réseau virtuel

Si vous n’avez pas encore un réseau virtuel, créez-le à l’aide de hello [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create) commande. Lorsque vous créez un réseau virtuel, assurez-vous que vous spécifiez des espaces d’adressage hello ne chevauchent pas hello d’espaces d’adressage que vous disposez sur votre réseau local.

Hello exemple suivant crée un réseau virtuel nommé « TestVNet1 » et un sous-réseau, 'Subnet1'.

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4. <a name="gwsub"></a>Créez le sous-réseau de passerelle hello

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

Pour cette configuration, vous avez également besoin d’un sous-réseau de passerelle. passerelle de réseau virtuel Hello utilise un sous-réseau de passerelle qui contient les adresses IP hello qui sont utilisés par les services de la passerelle VPN hello. Le sous-réseau de passerelle doit être nommé « GatewaySubnet ». Si vous choisissez un autre nom, vous créez un sous-réseau, mais Azure ne le traitera pas comme un sous-réseau de passerelle.

taille de Hello du sous-réseau de passerelle hello que vous spécifiez dépend de configuration de la passerelle VPN hello que vous souhaitez toocreate. Bien qu’il soit possible de toocreate un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus grand qui inclut plusieurs adresses en sélectionnant /27 ou /28. Permet à l’aide d’un sous-réseau de passerelle supérieure suffisamment IP adresses tooaccommodate futures configurations possibles.

Hello d’utilisation [créer de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#create) sous-réseau de passerelle commande toocreate hello.

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5. Créer une passerelle de réseau local hello

passerelle de réseau local Hello fait généralement référence d’emplacement de site tooyour. Vous attribuez un nom par lequel Azure permettre faire référence tooit, puis spécifier l’adresse IP de hello au site de hello de toowhich de périphérique VPN hello localement, vous allez créer une connexion. Vous spécifiez également préfixes d’adresses IP hello qui doivent être routés via le périphérique VPN toohello hello VPN gateway. vous spécifiez les préfixes d’adresse Hello sont des préfixes hello situés sur votre réseau local. Si votre réseau local change, vous pouvez facilement mettre à jour les préfixes hello.

Utilisez hello valeurs suivantes :

* Hello *---adresse ip de passerelle* est l’adresse IP de hello de votre périphérique VPN sur site. Votre périphérique VPN ne peut pas se trouver derrière un NAT.
* Hello *--préfixes d’adresse locale* est des espaces d’adressage de votre site.

Hello d’utilisation [az réseau local-passerelle créer](/cli/azure/network/local-gateway#create) commande tooadd une passerelle de réseau local avec plusieurs préfixes d’adresses :

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6. Demander une adresse IP publique

Une passerelle VPN doit avoir une adresse IP publique. Votre ressource d’adresse IP hello d’abord demander, puis consultez tooit lors de la création de votre passerelle de réseau virtuel. adresse IP de Hello est attribué dynamiquement les ressources toohello lors de la création de la passerelle VPN de hello. Actuellement, la passerelle VPN prend uniquement en charge l’allocation d’adresses IP publiques *dynamiques*. Vous ne pouvez pas demander d’affectation d’adresse IP publique statique. Toutefois, cela ne signifie pas que l’adresse IP de hello change après que qu’elle a été affectée passerelle VPN de tooyour. Hello seule fois changements d’adresses IP publiques hello est hello lorsque la passerelle est supprimé et recréé. Elle n’est pas modifiée lors du redimensionnement, de la réinitialisation ou des autres opérations de maintenance/mise à niveau internes de votre passerelle VPN.

Hello d’utilisation [az réseau public-ip créer](/cli/azure/network/public-ip#create) commande toorequest une adresse IP publique dynamique.

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7. Créer une passerelle VPN de hello

Créer la passerelle VPN de réseau virtuel hello. Création d’une passerelle VPN peut prendre jusqu'à too45 minutes ou plus toocomplete.

Utilisez hello valeurs suivantes :

* Hello *--type de passerelle* pour un Site à Site est configuration *Vpn*. type de passerelle Hello est toujours configuration toohello spécifique que vous implémentez. Pour plus d’informations, consultez [Types de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwtype).
* Hello *--vpn-type* peut être *RouteBased* (appelée tooas une passerelle dynamique dans certains documents), ou *basée sur des stratégies* (appelée tooas une passerelle statique dans certains documentation). Hello est toorequirements spécifique du périphérique hello que vous êtes connecté. Pour plus d’informations sur les types de passerelle VPN, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype).
* Sélectionnez hello SKU de passerelle que vous souhaitez toouse. Des limites de configuration s’appliquent à certaines références (SKU). Pour plus d’informations, consultez l’article [Références (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

Créer une passerelle VPN de hello à l’aide de hello [créer de passerelle de réseau virtuel de réseau az](/cli/azure/network/vnet-gateway#create) commande. Si vous exécutez cette commande à l’aide de hello '--aucune - attente' paramètre, vous ne voyez pas vos commentaires ou la sortie. Ce paramètre permet de hello passerelle toocreate en arrière-plan de hello. Il prend environ 45 minutes toocreate une passerelle.

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8. Configuration de votre périphérique VPN

Réseau local de tooan connexions site à Site requièrent un périphérique VPN. Dans cette étape, vous configurez votre périphérique VPN. Lorsque vous configurez votre périphérique VPN, vous devez suivant de hello :

- Une clé partagée. Cela est hello même partagé clé que vous spécifiez lors de la création de votre connexion VPN de Site à Site. Dans nos exemples, nous utilisons une clé partagée basique. Nous conseillons de générer un toouse de clé plus complexe.
- Hello adresse IP publique de votre passerelle de réseau virtuel. Vous pouvez afficher l’adresse IP publique de hello à l’aide de hello portail Azure, PowerShell ou CLI. toofind hello adresse IP publique de votre passerelle de réseau virtuel, utilisez hello [liste public-ip de réseau az](/cli/azure/network/public-ip#list) commande. Pour faciliter la lecture, la sortie de hello est liste de hello toodisplay mis en forme des adresses IP publiques au format de table.

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9. Créer la connexion VPN de hello

Créer un réseau VPN hello Site à Site entre votre passerelle de réseau virtuel et votre périphérique VPN sur site. Payer une attention toute particulière toohello partagé valeur de clé, qui doit correspondre à hello configuré partagé valeur de clé de votre périphérique VPN.

Créer la connexion hello à l’aide de hello [créer de connexion de vpn de réseau az](/cli/azure/network/vpn-connection#create) commande.

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

Après quelques instants, hello connexion sera établie.

## <a name="toverify"></a>10. Vérifiez la connexion VPN de hello

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

Si vous souhaitez une autre méthode tooverify toouse votre connexion, consultez [vérifier une connexion de passerelle VPN](vpn-gateway-verify-connection-resource-manager.md).

## <a name="connectVM"></a>machine virtuelle de tooa tooconnect

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>Tâches courantes

Cette section contient des commandes courantes qui sont utiles lorsque vous travaillez avec des configurations de site à site. Pour hello une liste complète des commandes de mise en réseau CLI, consultez [CLI d’Azure - mise en réseau](/cli/azure/network).

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>Étapes suivantes

* Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Pour plus d’informations sur BGP, consultez hello [vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [comment tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Pour plus d’informations sur le tunneling forcé, consultez [Configuration du tunneling forcé à l’aide du modèle de déploiement classique](vpn-gateway-forced-tunneling-rm.md).
* Pour plus d’informations sur les connexions haut actif-actif, consultez [Configuration haute disponibilité pour la connectivité entre les réseaux locaux et la connectivité entre deux réseaux virtuels](vpn-gateway-highlyavailable.md).
* Pour obtenir la liste des commandes de mise en réseau de l’interface de ligne de commande Azure, consultez l’article [Interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/network).