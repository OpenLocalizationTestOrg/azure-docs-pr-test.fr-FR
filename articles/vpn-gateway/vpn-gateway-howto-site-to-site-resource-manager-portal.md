---
title: "Se connecter à votre tooan de réseau local sur le réseau virtuel Azure : VPN de Site à Site : portail | Documents Microsoft"
description: "Toocreate étapes une connexion IPsec à partir de votre site réseau tooan réseau virtuel Azure sur hello Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN Site à Site entre différents locaux à l’aide du portail de hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Créer une connexion de Site à Site dans hello portail Azure

Cet article vous explique comment toouse hello toocreate portail Azure, une connexion de passerelle VPN de Site à Site à partir de votre toohello de réseau sur site réseau virtuel. étapes de Hello dans cet article s’appliquent à modèle de déploiement du Gestionnaire de ressources toohello. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [INTERFACE DE LIGNE DE COMMANDE](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portail Azure (classique)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Une connexion de passerelle VPN de Site à Site est utilisé tooconnect votre site réseau tooan réseau virtuel Azure via un tunnel VPN de IPsec/IKE (IKEv1 ou IKEv2). Ce type de connexion requiert un VPN périphérique local qui a un tooit d’adresse IP publique externe. Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).

![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Avant de commencer

Vérifiez que vous avez rempli hello suivant des critères avant de commencer votre configuration :

* Assurez-vous que vous disposez d’un périphérique VPN compatible et une personne qui est en mesure de tooconfigure il. Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).
* Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN. Cette adresse IP ne peut pas se trouver derrière un NAT.
* Si vous n’êtes pas familiarisé avec les plages d’adresses IP hello situés dans configuration du réseau de votre site, vous devez toocoordinate avec une personne qui peut fournir ces informations pour vous. Lorsque vous créez cette configuration, vous devez spécifier hello plage préfixes d’adresse que Azure achemine emplacement local de tooyour. Aucun des sous-réseaux hello de votre réseau local peuvent se chevauchant avec les sous-réseaux du réseau virtuel hello tooconnect à souhaitées sur. 

### <a name="values"></a>Exemples de valeurs

exemples de Hello dans cet article utilisent hello valeurs suivantes. Vous pouvez utiliser ces valeurs de toocreate un environnement de test, ou consultez toothem toobetter comprendre les exemples hello dans cet article.

* **Nom du réseau virtuel :** TestVNet1
* **Espace d’adressage :** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (facultatif pour cet exercice)
* **Sous-réseaux :**
  * FrontEnd : 10.11.0.0/24
  * BackEnd : 10.12.0.0/24 (facultatif pour cet exercice)
* **Sous-réseau de passerelle :** 10.11.255.0/27
* **Groupe de ressources :** TestRG1
* **Emplacement :** États-Unis de l’Est
* **Serveur DNS**  Facultatif. adresse IP de Hello de votre serveur DNS.
* **Nom de passerelle de réseau virtuel :** VNet1GW
* **Adresse IP publique :** VNet1GWIP
* **Type de VPN :** Route-based
* **Type de connexion :** Site-to-site (IPsec)
* **Type de passerelle :** VPN
* **Nom de passerelle de réseau local :** Site2
* **Nom de connexion :** VNet1toSite2

## <a name="CreatVNet"></a>1. Créez un réseau virtuel

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. Spécifier un serveur DNS

DNS n’est pas requis toocreate un Site à Site connexion. Toutefois, si vous souhaitez toohave la résolution de noms pour les ressources qui sont déployés tooyour des réseaux virtuels, vous devez spécifier un serveur DNS. Ce paramètre vous permet de spécifier le serveur DNS hello que vous souhaitez toouse pour la résolution de nom pour ce réseau virtuel. Il n'entraîne pas la création d'un serveur DNS. Pour plus d’informations sur la résolution de noms pour les machines virtuelles, consultez [Résolution de noms pour les machines virtuelles et instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Créez le sous-réseau de passerelle hello

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Créer une passerelle VPN de hello

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Créer une passerelle de réseau local hello

passerelle de réseau local Hello fait généralement référence d’emplacement de site tooyour. Vous attribuez un nom par lequel Azure permettre faire référence tooit, puis spécifier l’adresse IP de hello au site de hello de toowhich de périphérique VPN hello localement, vous allez créer une connexion. Vous spécifiez également préfixes d’adresses IP hello qui doivent être routés via le périphérique VPN toohello hello VPN gateway. vous spécifiez les préfixes d’adresse Hello sont des préfixes hello situés sur votre réseau local. Si vos modifications de réseau local, ou vous avez besoin d’adresse IP publique de toochange hello pour le périphérique VPN de hello, vous pouvez facilement mettre à jour les valeurs hello plus tard.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. Configuration de votre périphérique VPN

Réseau local de tooan connexions site à Site requièrent un périphérique VPN. Dans cette étape, vous configurez votre périphérique VPN. Lorsque vous configurez votre périphérique VPN, vous devez suivant de hello :

- Une clé partagée. Cela est hello même partagé clé que vous spécifiez lors de la création de votre connexion VPN de Site à Site. Dans nos exemples, nous utilisons une clé partagée basique. Nous conseillons de générer un toouse de clé plus complexe.
- Hello adresse IP publique de votre passerelle de réseau virtuel. Vous pouvez afficher l’adresse IP publique de hello à l’aide de hello portail Azure, PowerShell ou CLI. toofind hello adresse IP publique de votre passerelle VPN à l’aide de hello portail Azure, accédez trop**les passerelles de réseau virtuel**, puis cliquez sur nom hello de votre passerelle.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Créer la connexion VPN de hello

Créer un réseau VPN hello Site à Site entre votre passerelle de réseau virtuel et votre périphérique VPN sur site.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Vérifiez la connexion VPN de hello

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>machine virtuelle de tooa tooconnect

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>Comment tooreset une passerelle VPN

La réinitialisation d’une passerelle VPN Azure est utile si vous perdez la connectivité VPN entre différents locaux sur un ou plusieurs tunnels VPN de site à site. Dans ce cas, vos périphériques VPN sur site sont tous les fonctionne correctement, mais sont tooestablish n’a pas pu les tunnels IPsec avec les passerelles VPN Azure hello. Pour obtenir la procédure, consultez [Réinitialiser une passerelle VPN](vpn-gateway-resetgw-classic.md).

## <a name="resize"></a>Comment toochange une passerelle de référence (SKU) (redimensionner une passerelle)

Les étapes de hello toochange une référence (SKU) de la passerelle, consultez [SKU de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur BGP, consultez hello [vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [comment tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Pour plus d’informations sur le tunneling forcé, consultez [Configuration du tunneling forcé à l’aide du modèle de déploiement classique](vpn-gateway-forced-tunneling-rm.md).
* Pour plus d’informations sur les connexions haut actif-actif, consultez [Configuration haute disponibilité pour la connectivité entre les réseaux locaux et la connectivité entre deux réseaux virtuels](vpn-gateway-highlyavailable.md).
