---
title: "aaaConfigure un réseau virtuel et une passerelle pour ExpressRoute dans hello portail classique | Documents Microsoft"
description: "Cet article vous guide dans la configuration d’un réseau virtuel pour ExpressRoute à l’aide du modèle de déploiement classique hello et du portail classique de hello."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 688817d9-51c8-4372-9af8-33fa098c7c5a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/20/2016
ms.author: cherylmc
ms.openlocfilehash: dd1f6c5e85dbb3ad0a53ecd81c13b4d3f5c06e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-for-expressroute-in-hello-classic-portal"></a>Créer un réseau virtuel pour ExpressRoute dans le portail classique de hello
étapes Hello dans cet article vous guidera dans la configuration d’un réseau virtuel et une passerelle de réseau virtuel pour une utilisation avec ExpressRoute à l’aide du modèle de déploiement classique hello et du portail classique de hello.

Si vous cherchez des instructions pour le modèle de déploiement du Gestionnaire de ressources hello, vous pouvez utiliser hello suivant articles : [créer un réseau virtuel à l’aide de PowerShell](../virtual-network/virtual-networks-create-vnet-arm-ps.md) et [ajouter un gestionnaire de ressources du VNet de tooa passerelle VPN pour ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**À propos des modèles de déploiement Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="create-a-classic-vnet-and-gateway"></a>Créer un réseau virtuel classique et une passerelle
Hello les étapes suivantes créent un réseau virtuel classique et une passerelle de réseau virtuel. Si vous disposez déjà d’un réseau virtuel classique, consultez hello [configurer un réseau classique existante](#config) dans cet article.

1. Connectez-vous à toohello [portail Azure classic](http://manage.windowsazure.com).
2. Dans hello coin inférieur gauche de l’écran hello, cliquez sur **nouveau**. Dans le volet de navigation hello, cliquez sur **Services réseau**, puis cliquez sur **réseau virtuel**. Cliquez sur **création personnalisée** Assistant de configuration toobegin hello.
3. Sur hello **détails du réseau virtuel** page, entrez hello suivante :
   
   * **Nom** : nommez votre réseau virtuel. Vous utiliserez ce nom de réseau virtuel lorsque vous déployez vos machines virtuelles et instances PaaS, vous pouvez donc pas nom de hello toomake trop compliqué.
   * **Emplacement** – emplacement de hello est directement lié toohello physique emplacement (région) où votre tooreside de ressources (machines virtuelles). Par exemple, si vous souhaitez que les machines virtuelles hello que vous déployez toothis toobe de réseau virtuel résident physiquement dans est des États-Unis, sélectionnez cet emplacement. Vous ne pouvez pas modifier la région hello associée à votre réseau virtuel après que l’avoir créée.
4. Sur hello **serveurs DNS et connectivité VPN** page, entrez hello informations suivantes, puis cliquez sur hello suivant sur flèche hello en bas à droite. 
   
   * **Serveurs DNS** : entrez le nom du serveur DNS hello et l’adresse IP, ou sélectionnez un serveur DNS précédemment enregistré à partir du menu contextuel de hello. Ce paramètre n’entraîne pas la création de serveur DNS. Il vous permet de serveurs DNS de toospecify hello que vous souhaitez toouse pour la résolution de nom pour ce réseau virtuel.
   * **Connectivité de site à Site** : sélectionnez hello case à cocher pour **configurer un VPN de site à site**.
   * **ExpressRoute** – sélectionnez hello case à cocher **utiliser ExpressRoute**. Cette option apparaît uniquement si vous avez sélectionné **Configurer un réseau VPN de site à site**.
   * **Réseau local** -vous êtes toohave requis un site réseau local pour ExpressRoute. Toutefois, dans le cas de hello d’une connexion ExpressRoute, les préfixes d’adresse hello spécifié pour hello local site réseau sera ignoré. Au lieu de cela, les préfixes d’adresse hello publiés tooMicrosoft via hello circuit ExpressRoute sera utilisé pour le routage.<BR>Si vous disposez déjà d’un réseau local est créé pour votre connexion ExpressRoute, vous pouvez le sélectionner à partir de la liste déroulante de hello. Si vous ne disposez pas d’un réseau local, sélectionnez **Spécifier un nouveau réseau local**.
5. Hello **connectivité de Site à Site** page s’affiche si vous avez sélectionné toospecify un nouveau réseau local à l’étape précédente de hello. tooconfigure votre réseau local, entrez hello informations suivantes et puis cliquez sur la flèche suivant de hello. 
   
   * **Nom** -hello nom toocall votre site de réseau (local).
   * **Espace d’adressage** : inclut l’adresse IP de départ et le nombre d’adresses (CIDR). Vous pouvez spécifier n’importe quelle plage adresse tant qu’il ne chevauche la plage d’adresses hello pour votre réseau virtuel. En règle générale, cela serait spécifier les plages d’adresses hello pour vos réseaux locaux, mais dans le cas de hello d’ExpressRoute, ces paramètres ne sont pas utilisés. Toutefois, ce paramètre est requis dans le réseau local de commande toocreate hello lorsque vous utilisez le portail classique de hello.
   * **Ajouter un espace d’adressage** : ce paramètre ne s’applique pas à ExpressRoute.
6. Sur hello **espaces d’adressage de réseau virtuel** page et entrez hello informations suivantes, puis cliquez sur coche hello sur hello tooconfigure de droite inférieure à votre réseau. 
   
   * **Espace d’adressage** : inclut l’adresse IP de départ et le nombre d’adresses. Vérifiez que vous spécifiez des espaces d’adressage hello ne chevauchent hello d’espaces d’adressage que vous disposez sur votre réseau local.
   * **Ajouter un sous-réseau** : inclut l’adresse IP de départ et le nombre d’adresses. Il est inutile d’ajouter des sous-réseaux supplémentaires.
   * **Ajouter un sous-réseau de passerelle** -cliquez sur le sous-réseau de passerelle tooadd hello. sous-réseau de passerelle Hello est utilisé uniquement pour la passerelle de réseau virtuel hello et est requis pour cette configuration.<BR>Hello sous-réseau CIDR (nombre d’adresses) de la passerelle pour ExpressRoute doit être/28 ou supérieure (/ 27/26 etc..). Cela permet suffisamment d’adresses IP dans ce toowork de configuration de sous-réseau tooallow hello. Dans le portail classique hello, si vous avez sélectionné la case à cocher de hello toouse ExpressRoute, le portail de hello spécifie un sous-réseau de passerelle avec /28.  Vous ne pouvez pas ajuster le nombre d’adresses CIDR hello dans le portail classique de hello. sous-réseau de passerelle Hello apparaît sous la forme **passerelle** dans le portail classique hello, bien que hello nom réel de sous-réseau de passerelle hello créé est réellement **GatewaySubnet**. Vous pouvez afficher ce nom à l’aide de PowerShell ou Bonjour portail Azure.
7. Cliquez sur hello coche bas hello de page de hello et toocreate de votre réseau virtuel commence. Quand elle est terminée, vous verrez **créé** répertoriés sous **état** sur hello **réseaux** page du portail classique de hello.

## <a name="gw"></a>Créer une passerelle de hello
1. Sur hello **réseaux** , cliquez sur réseau virtuel hello que vous venez de créer, puis cliquez sur **tableau de bord** en hello haut hello.
2. Sous hello hello **tableau de bord** , cliquez sur **créer une passerelle** et sélectionnez **routage dynamique**. Cliquez sur **Oui** tooconfirm que vous souhaitez toocreate une passerelle.
3. Lors de la passerelle de hello lance la création, vous verrez un message pour vous informer que passerelle hello a été démarrée. Cela peut prendre jusqu'à minutes too45 hello passerelle toocreate.
4. Liez votre circuit tooa de réseau. Suivez les instructions de hello dans l’article de hello [comment toolink réseaux virtuels tooExpressRoute circuits](expressroute-howto-linkvnet-classic.md).

## <a name="config"></a>Configurer un réseau virtuel classique existant pour ExpressRoute
Si vous disposez déjà d’un réseau virtuel classique, vous pouvez configurer tooconnect tooExpressRoute dans portail classique de hello. paramètres de Hello sont même hello sous forme de sections hello ci-dessus, afin d’en lecture via ces toobecome sections familiarisé avec hello les paramètres requis. Si vous souhaitez toocreate une connexion de coexistence ExpressRoute/Site à Site, consultez [cet article](expressroute-howto-coexist-classic.md) pour connaître les étapes hello. Elles sont différentes de celles hello les étapes de cet article.

1. Vous avez besoin de réseau local de hello toocreate avant de mettre à jour rest hello de vos paramètres de réseau virtuel. Cliquez sur un nouveau réseau local, ce qui est nécessaire lors de la configuration ExpressRoute via le portail classique de hello, de toocreate **nouveau**  **>**  **Services réseau**  **>**  **Réseau virtuel**  **>**  **réseau local d’ajouter**. Suivez les hello Assistant étapes toocreate hello réseau local.
2. Utilisez **configurer** page reste hello tooupdate paramètres hello pour votre réseau virtuel et tooassociate hello réseau virtuel toohello réseau local.
3. Après avoir configuré les paramètres de hello, accédez à toohello [créer une passerelle hello](#gw) section de cette passerelle de hello toocreate l’article.

## <a name="next-steps"></a>Étapes suivantes
* Si vous souhaitez que le réseau virtuel du tooyour tooadd machines virtuelles, consultez [virtuels cursus](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/).
* Si vous souhaitez toolearn plus d’informations sur ExpressRoute, consultez hello [présentation ExpressRoute](expressroute-introduction.md).

