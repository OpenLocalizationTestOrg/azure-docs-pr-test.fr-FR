---
title: "Connecter votre réseau local à un réseau virtuel Azure : VPN site à site : interface de ligne de commande | Microsoft Docs"
description: "Étapes de création d’une connexion IPsec entre votre réseau local et un réseau virtuel Azure via l’Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN de site à site à l’aide de l’interface de ligne de commande (CLI)."
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
ms.openlocfilehash: 019c5421dc470b18c9087417b93c241cc5730f77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de l’interface de ligne de commande

Cet article vous explique comment utiliser l’interface de ligne de commande Azure pour créer une connexion de passerelle VPN de site à site à partir de votre réseau local vers le réseau virtuel. Les étapes mentionnées dans cet article s’appliquent au modèle de déploiement Resource Manager. Vous pouvez également créer cette configuration à l’aide d’un autre outil ou modèle de déploiement en sélectionnant une option différente dans la liste suivante :<br>

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [INTERFACE DE LIGNE DE COMMANDE](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portail Azure (classique)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

Une connexion de passerelle VPN de site à site permet de connecter votre réseau local à un réseau virtuel Azure via un tunnel VPN IPsec/IKE (IKEv1 ou IKEv2). Ce type de connexion requiert un périphérique VPN local disposant d’une adresse IP publique exposée en externe. Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).

## <a name="before-you-begin"></a>Avant de commencer

Vérifiez que vous disposez des éléments ci-dessous avant de commencer votre configuration :

* Veillez à disposer d’un périphérique VPN compatible et à être entouré d’une personne en mesure de le configurer. Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).
* Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN. Cette adresse IP ne peut pas se trouver derrière un NAT.
* Si vous ne maîtrisez pas les plages d’adresses IP situées dans votre configuration de réseau local, vous devez contacter une personne en mesure de vous aider. Lorsque vous créez cette configuration, vous devez spécifier les préfixes des plages d’adresses IP qu’Azure acheminera vers votre emplacement local. Aucun des sous-réseaux de votre réseau local ne peut chevaucher les sous-réseaux du réseau virtuel auquel vous souhaitez vous connecter.
* Vérifiez que vous avez installé la dernière version des commandes CLI (versions 2.0 ou ultérieures). Pour plus d’informations sur l’installation des commandes CLI, consultez [Install Azure CLI 2.0](/cli/azure/install-azure-cli) (Installer l’interface de ligne de commande Azure 2.0) et [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) (Prise en main de l’interface de ligne de commande Azure 2.0).

### <a name="example"></a>Exemples de valeurs

Vous pouvez utiliser ces valeurs pour créer un environnement de test ou vous y référer pour mieux comprendre les exemples de cet article :

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

## <a name="Login"></a>1. Connexion à votre abonnement

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2. Créer un groupe de ressources

L’exemple suivant crée un groupe de ressources nommé « TestRG1 » à l’emplacement « eastus ». Si vous disposez déjà d’un groupe de ressources dans la région où vous souhaitez créer votre réseau virtuel, vous pouvez l’utiliser à la place de l’exemple donné.

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3. Créez un réseau virtuel

Si vous n’avez pas de réseau virtuel, créez-en un à l’aide de la commande [az network vnet create](/cli/azure/network/vnet#create). Lorsque vous créez un réseau virtuel, vérifiez que les espaces d’adressage que vous spécifiez ne chevauchent pas les espaces d’adressage de votre réseau local.

L’exemple suivant permet de créer un réseau virtuel nommé « TestVNet1 » et un sous-réseau nommé « Subnet1 ».

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4. <a name="gwsub"></a>Créer le sous-réseau de passerelle

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

Pour cette configuration, vous avez également besoin d’un sous-réseau de passerelle. La passerelle de réseau virtuel utilise un sous-réseau de passerelle qui contient les adresses IP utilisées par les services de passerelle VPN. Le sous-réseau de passerelle doit être nommé « GatewaySubnet ». Si vous choisissez un autre nom, vous créez un sous-réseau, mais Azure ne le traitera pas comme un sous-réseau de passerelle.

La taille du sous-réseau de passerelle que vous spécifiez dépend de la configuration de la passerelle VPN que vous souhaitez créer. Bien qu’il soit possible de créer un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus vaste qui inclut un plus grand nombre d’adresses en sélectionnant /27 ou /28. En choisissant un sous-réseau de passerelle plus vaste, vous disposez de suffisamment d’adresses IP pour prendre en charge d’éventuelles configurations futures.

Utilisez la commande [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) pour créer le sous-réseau de passerelle.

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5. Créer la passerelle de réseau local

La passerelle de réseau local fait généralement référence à votre emplacement local. Donnez au site un nom auquel Azure pourra se référer, puis spécifiez l’adresse IP du périphérique VPN local vers lequel vous allez créer une connexion. Spécifiez également les préfixes d’adresses IP qui seront acheminés via la passerelle VPN vers le périphérique VPN. Les préfixes d’adresses que vous spécifiez sont les préfixes situés sur votre réseau local. Vous pouvez facilement mettre à jour ces préfixes si votre réseau local change.

Utilisez les valeurs suivantes :

* La valeur *--gateway-ip-address* est l’adresse IP de votre périphérique VPN local. Votre périphérique VPN ne peut pas se trouver derrière un NAT.
* La valeur *--local-address-prefixes* représente vos espaces d’adressage local.

Utilisez la commande [az network local-gateway create](/cli/azure/network/local-gateway#create) pour ajouter une passerelle de réseau local avec plusieurs préfixes d’adresses :

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6. Demander une adresse IP publique

Une passerelle VPN doit avoir une adresse IP publique. Vous commencez par demander la ressource d’adresse IP, puis vous y faites référence lors de la création de votre passerelle de réseau virtuel. L’adresse IP est affectée dynamiquement à la ressource lors de la création de la passerelle VPN. Actuellement, la passerelle VPN prend uniquement en charge l’allocation d’adresses IP publiques *dynamiques*. Vous ne pouvez pas demander d’affectation d’adresse IP publique statique. Toutefois, cela ne signifie pas que l’adresse IP change après son affectation à votre passerelle VPN. L’adresse IP publique change uniquement lorsque la passerelle est supprimée, puis recréée. Elle n’est pas modifiée lors du redimensionnement, de la réinitialisation ou des autres opérations de maintenance/mise à niveau internes de votre passerelle VPN.

Utilisez la commande [az network public-ip create](/cli/azure/network/public-ip#create) pour demander une adresse IP publique dynamique.

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7. Créer la passerelle VPN

Créez la passerelle VPN de réseau virtuel. La création d’une passerelle VPN peut prendre 45 minutes ou plus.

Utilisez les valeurs suivantes :

* Le paramètre *--gateway-type* pour une configuration de site à site est *Vpn*. Le type de passerelle dépend toujours de la configuration que vous implémentez. Pour plus d’informations, consultez [Types de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwtype).
* Le paramètre *--vpn-type* peut avoir pour valeur *RouteBased* (appelé passerelle dynamique dans certaines documentations) ou *PolicyBased* (appelé passerelle statique dans certaines documentations). Le paramètre est spécifique aux exigences du périphérique auquel vous vous connectez. Pour plus d’informations sur les types de passerelle VPN, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype).
* Sélectionnez la référence SKU de la passerelle que vous souhaitez utiliser. Des limites de configuration s’appliquent à certaines références (SKU). Pour plus d’informations, consultez l’article [Références (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

Créez la passerelle VPN à l’aide de la commande [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create). Si vous exécutez cette commande à l’aide du paramètre « --no-wait », vous ne voyez aucun commentaire ni sortie. Ce paramètre permet à la passerelle d’être créée en arrière-plan. La création d’une passerelle prend environ 45 minutes.

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8. Configuration de votre périphérique VPN

Les connexions site à site vers un réseau local nécessitent un périphérique VPN. Dans cette étape, vous configurez votre périphérique VPN. Pour configurer votre périphérique VPN, vous avez besoin des éléments suivants :

- Une clé partagée. Il s’agit de la clé partagée spécifiée lors de la création de la connexion VPN de site à site. Dans nos exemples, nous utilisons une clé partagée basique. Nous vous conseillons de générer une clé plus complexe.
- L’adresse IP publique de votre passerelle de réseau virtuel. Vous pouvez afficher l’adresse IP publique à l’aide du portail Azure, de PowerShell ou de l’interface de ligne de commande. Pour trouver l’adresse IP publique de votre passerelle de réseau virtuel, utilisez la commande [az network public-ip list](/cli/azure/network/public-ip#list). Pour faciliter la lecture, la sortie est mise en forme pour afficher la liste des adresses IP publiques sous forme de tableau.

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9. Créer la connexion VPN

Créez la connexion VPN de site à site entre votre passerelle de réseau virtuel et votre périphérique VPN local. Soyez particulièrement attentif à la valeur de clé partagée qui doit correspondre à la valeur de clé partagée configurée pour votre périphérique VPN.

Créez la connexion à l’aide de la commande [az network vpn-connection create](/cli/azure/network/vpn-connection#create).

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

Après un bref délai, la connexion sera établie.

## <a name="toverify"></a>10. Vérifier la connexion VPN

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

Si vous souhaitez utiliser une autre méthode pour vérifier votre connexion, consultez l’article [Vérifier une connexion de passerelle VPN](vpn-gateway-verify-connection-resource-manager.md).

## <a name="connectVM"></a>Se connecter à une machine virtuelle

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>Tâches courantes

Cette section contient des commandes courantes qui sont utiles lorsque vous travaillez avec des configurations de site à site. Pour obtenir la liste complète des commandes de mise en réseau CLI, consultez [Networking - az network](/cli/azure/network) (Mise en réseau - az network).

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>Étapes suivantes

* Une fois la connexion achevée, vous pouvez ajouter des machines virtuelles à vos réseaux virtuels. Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Pour plus d’informations sur le protocole BGP, consultez les articles [Vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [Comment configurer BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Pour plus d’informations sur le tunneling forcé, consultez [Configuration du tunneling forcé à l’aide du modèle de déploiement Azure Resource Manager](vpn-gateway-forced-tunneling-rm.md).
* Pour plus d’informations sur les connexions haut actif-actif, consultez [Configuration haute disponibilité pour la connectivité entre les réseaux locaux et la connectivité entre deux réseaux virtuels](vpn-gateway-highlyavailable.md).
* Pour obtenir la liste des commandes de mise en réseau de l’interface de ligne de commande Azure, consultez l’article [Interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/network).