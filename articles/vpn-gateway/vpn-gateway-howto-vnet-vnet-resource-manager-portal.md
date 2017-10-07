---
title: "Se connecter à un réseau virtuel de tooanother réseau virtuel Azure : portail | Documents Microsoft"
description: "Créer une connexion de passerelle VPN entre réseaux virtuels à l’aide du Gestionnaire de ressources et hello portail Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a>Configurer une connexion de passerelle VPN de réseau virtuel à réseau virtuel à l’aide de hello portail Azure

Cet article vous montre comment toocreate une connexion de passerelle VPN entre les réseaux virtuels. Hello réseaux virtuels peuvent être hello identiques ou différentes régions, et à partir de hello identiques ou différents abonnements. Lors de la connexion des réseaux virtuels à partir de différents abonnements, les abonnements hello n’est pas nécessaire de toobe associé hello même client Active Directory. 

étapes Hello dans cet article s’appliquent toohello modèle de déploiement de gestionnaire de ressources et utilisent hello portail Azure. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interface de ligne de commande Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portail Azure (classique)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Connexions entre différents modèles de déploiement - Portail Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Connexions entre différents modèles de déploiement - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![Diagramme v2v](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

Connexion d’un réseau virtuel de réseau virtuel tooanother (au réseau) est tooconnecting comme emplacement d’un site réseau virtuel tooan local. Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE. Si vos réseaux virtuels sont Bonjour même région, vous souhaiterez peut-être tooconsider les connectant à l’aide de l’homologation de réseau virtuel. L’homologation de réseaux virtuels (ou VNet Peering) n’utilise pas de passerelle VPN. Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).

Vous pouvez combiner une communication de réseau virtuel à réseau virtuel avec des configurations multisites. Cela vous permet d’établir des topologies de réseau qui combinent une connectivité intersite de connectivité de réseau virtuel entre, comme indiqué dans hello suivant schéma :

![À propos des connexions](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "À propos des connexions")

### <a name="why-connect-virtual-networks"></a>Pourquoi connecter des réseaux virtuels ?

Vous souhaiterez peut-être les réseaux virtuels tooconnect pour hello suivant raisons :

* **Géo-redondance et présence géographique dans plusieurs régions**
  
  * Vous pouvez configurer la géo-réplication ou la synchronisation avec une connectivité sécurisée sans passer par les points de terminaison accessibles sur Internet.
  * Avec Traffic Manager et l’équilibreur de charge Azure, vous pouvez configurer une charge de travail hautement disponible avec la géo-redondance dans plusieurs régions Azure. Par exemple important, tooset des SQL Always On avec des groupes de disponibilité répartis dans plusieurs régions Azure.
* **Applications multiniveaux régionales avec une limite d’isolement ou administrative**
  
  * Dans hello même région, vous pouvez définir des applications à plusieurs niveaux avec plusieurs réseaux virtuels interconnectés tooisolation ou exigences administratives.

Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez hello [FAQ sur le réseau à](#faq) à fin hello de cet article. Notez que si vos réseaux virtuels sont dans différents abonnements, vous ne peut pas créer de connexion de hello dans le portail de hello. Vous pouvez utiliser [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) ou [l’interface de ligne de commande (CLI)](vpn-gateway-howto-vnet-vnet-cli.md).

### <a name="values"></a>Exemples de paramètres

Lorsque vous utilisez ces étapes en guise d’exercice, vous pouvez utiliser les valeurs des paramètres exemple hello. À titre d’exemple, nous utilisons plusieurs espaces d’adressage pour chaque réseau virtuel. Toutefois, les configurations de réseau virtuel à réseau virtuel ne nécessitent pas plusieurs espaces d’adressage.

**Valeurs pour TestVNet1 :**

* Nom du réseau virtuel : TestVNet1
* Espace d’adressage : 10.11.0.0/16
  * Nom du sous-réseau : FrontEnd
  * Plage d’adresses de sous-réseau : 10.11.0.0/24
* Groupe de ressources : TestRG1
* Emplacement : Est des États-Unis
* Espace d’adressage : 10.12.0.0/16
  * Nom du sous-réseau : BackEnd
  * Plage d’adresses de sous-réseau : 10.12.0.0/24
* Nom de sous-réseau de passerelle : GatewaySubnet (Ceci va remplissage automatique dans le portail de hello)
  * Plage d’adresses de sous-réseau de passerelle : 10.11.255.0/27
* Serveur DNS : Utiliser l’adresse IP de hello de votre serveur DNS
* Nom de passerelle de réseau virtuel : TestVNet1GW
* Type de passerelle : VPN
* Type de VPN : Route-based
* Référence (SKU) : Sélectionnez hello référence passerelle toouse
* Nom de l’adresse IP publique : TestVNet1GWIP
* Valeurs de connexion :
  * Nom : TestVNet1toTestVNet4
  * Clé partagée : vous pouvez créer vous-même le clé partagée de hello. Pour cet exemple, nous allons utiliser abc123. Hello est important lorsque vous créez la connexion hello entre hello réseaux virtuels, valeur de hello doit correspondre.

**Valeurs pour TestVNet4 :**

* Nom du réseau virtuel : TestVNet4
* Espace d’adressage : 10.41.0.0/16
  * Nom du sous-réseau : FrontEnd
  * Plage d’adresses de sous-réseau : 10.41.0.0/24
* Groupe de ressources : TestRG1
* Emplacement : États-Unis de l’Ouest
* Espace d’adressage : 10.42.0.0/16
  * Nom du sous-réseau : BackEnd
  * Plage d’adresses de sous-réseau : 10.42.0.0/24
* Nom de GatewaySubnet : GatewaySubnet (Ceci va remplissage automatique dans le portail de hello)
  * Plage d’adresses de GatewaySubnet : 10.41.255.0/27
* Serveur DNS : Utiliser l’adresse IP de hello de votre serveur DNS
* Nom de passerelle de réseau virtuel : TestVNet4GW
* Type de passerelle : VPN
* Type de VPN : Route-based
* Référence (SKU) : Sélectionnez hello référence passerelle toouse
* Nom de l’adresse IP publique : TestVNet4GWIP
* Valeurs de connexion :
  * Nom : TestVNet4toTestVNet1
  * Clé partagée : vous pouvez créer vous-même le clé partagée de hello. Pour cet exemple, nous allons utiliser abc123. Hello est important lorsque vous créez la connexion hello entre hello réseaux virtuels, valeur de hello doit correspondre.

## <a name="CreatVNet"></a>1. Créer et configurer TestVNet1
Si vous disposez déjà d’un réseau virtuel, vérifiez que les paramètres de hello sont compatibles avec votre conception de passerelle VPN. Accordez une attention particulière aux sous-réseaux tooany peuvent se chevaucher avec d’autres réseaux. Si vos sous-réseaux se chevauchent, votre connexion ne fonctionnera pas correctement. Si votre réseau virtuel est configuré avec les paramètres corrects hello, vous pouvez commencer les étapes hello Bonjour [spécifier un serveur DNS](#dns) section.

### <a name="toocreate-a-virtual-network"></a>toocreate un réseau virtuel
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="subnets"></a>2. Ajouter des espaces d’adressage supplémentaires et créer des sous-réseaux
Vous pouvez ajouter des espaces d’adressage supplémentaires et créer des sous-réseaux pour votre réseau virtuel une fois qu’il a été créé.

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <a name="gatewaysubnet"></a>3. Créer un sous-réseau de passerelle
Avant de connecter votre passerelle tooa de réseau virtuel, vous devez d’abord sous-réseau de passerelle hello toocreate toowhich de réseau virtuel hello vous voulez tooconnect. Si possible, il est meilleure toocreate un sous-réseau de passerelle à l’aide d’un bloc CIDR de /28 ou /27 dans l’ordre tooprovide suffisamment IP adresses tooaccommodate futures de configuration supplémentaires requises.

Si vous créez cette configuration en guise d’exercice, consultez toothese [exemples de paramètres](#values) lors de la création de votre sous-réseau de passerelle.

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a>toocreate un sous-réseau de passerelle
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <a name="dns"></a>4. Spécifier un serveur DNS (facultatif)
Aucun DNS n’est nécessaire pour les connexions entre des réseaux virtuels. Toutefois, si vous souhaitez toohave la résolution de noms pour les ressources qui sont déployés tooyour des réseaux virtuels, vous devez spécifier un serveur DNS. Ce paramètre vous permet de spécifier le serveur DNS hello que vous souhaitez toouse pour la résolution de nom pour ce réseau virtuel. Il n'entraîne pas la création d'un serveur DNS.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="VNetGateway"></a>5. Créer une passerelle de réseau virtuel
Dans cette étape, vous créez passerelle de réseau virtuel hello pour votre réseau virtuel. Création d’une passerelle peut souvent prendre entre 45 minutes ou plus, selon la passerelle sélectionnée de hello référence (SKU). Si vous créez cette configuration en guise d’exercice, vous pouvez faire référence à toohello [exemples de paramètres](#values).

### <a name="toocreate-a-virtual-network-gateway"></a>toocreate une passerelle de réseau virtuel
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <a name="CreateTestVNet4"></a>6. Créer et configurer TestVNet4
Une fois que vous avez configuré TestVNet1, créez TestVNet4 en répétant les étapes précédentes hello, en remplaçant les valeurs hello avec ceux du TestVNet4. Vous n’avez pas besoin toowait jusqu'à ce que la passerelle de réseau virtuel hello pour TestVNet1 a terminé la création avant de configurer TestVNet4. Si vous utilisez vos propres valeurs, assurez-vous que les espaces d’adressage hello ne se chevauchent pas avec les hello que vous souhaitez tooconnect à des réseaux virtuels.

## <a name="TestVNet1Connection"></a>7. Configurer la connexion de hello TestVNet1
Quand les passerelles de réseau virtuel hello pour TestVNet1 et TestVNet4 sont terminées, vous pouvez créer votre réseau virtuel de connexions de la passerelle. Dans cette section, vous allez créer une connexion à partir de VNet1 tooVNet4. Ces étapes ne fonctionnent que pour les réseaux virtuels Bonjour même abonnement. Si vos réseaux virtuels sont dans différents abonnements, vous devez utiliser la connexion de hello toomake PowerShell. Consultez hello [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) l’article.

1. Dans **toutes les ressources**, accédez de passerelle de réseau virtuel toohello pour votre réseau virtuel. Par exemple, **TestVNet1GW**. Cliquez sur **TestVNet1GW** Panneau de passerelle de réseau virtuel de hello tooopen.
   
    ![Panneau Connexions](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Panneau Connexions")
2. Cliquez sur **+ ajouter** tooopen hello **ajouter une connexion** panneau.
3. Sur hello **ajouter une connexion** panneau, dans le champ de nom hello, tapez un nom pour votre connexion. Par exemple, **TestVNet1toTestVNet4**.
   
    ![Nom de la connexion](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Nom de la connexion")
4. Pour **Type de connexion**. Sélectionnez **réseau à** à partir de la liste déroulante de hello.
5. Hello **première passerelle de réseau virtuel** valeur de champ est renseignée automatiquement, car vous créez cette connexion à partir de la passerelle de réseau virtuel spécifié hello.
6. Hello **seconde passerelle de réseau virtuel** champ est la passerelle de réseau virtuel hello Hello réseau virtuel que vous souhaitez que toocreate une connexion. Cliquez sur **choisissez une autre passerelle de réseau virtuel** tooopen hello **passerelle de réseau virtuel choisir** panneau.
   
    ![Ajouter une connexion](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Ajouter une connexion")
7. Vue hello virtuel passerelles de réseau qui sont répertoriés dans ce panneau. Notez que seules les passerelles de réseau virtuel incluses dans votre abonnement sont répertoriées. Si vous souhaitez la passerelle de réseau virtuel tooa tooconnect qui n’est pas dans votre abonnement, utilisez hello [PowerShell article](vpn-gateway-vnet-vnet-rm-ps.md). 
8. Cliquez sur passerelle de réseau virtuel hello tooconnect à souhaitées.
9. Bonjour **clé partagée** , tapez une clé partagée pour votre connexion. Vous pouvez générer ou créer cette clé vous-même. Dans une connexion site à site, clé hello que vous utilisez serait être exactement hello même pour votre appareil local et votre connexion de passerelle de réseau virtuel. concept de Hello est similaire, à ceci près qu’au lieu de l’appareil de VPN tooa connexion, vous vous connectez passerelle de réseau virtuel tooanother.
   
    ![Clé partagée](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Clé partagée")
10. Cliquez sur **OK** à hello bas de hello panneau toosave vos modifications.

## <a name="TestVNet4Connection"></a>8. Configurer la connexion de hello TestVNet4
Ensuite, créez une connexion de TestVNet4 tooTestVNet1. Utilisez hello même méthode que vous avez utilisé connexion hello toocreate TestVNet1 tooTestVNet4. Assurez-vous que vous utilisez hello même clé partagée.

## <a name="VerifyConnection"></a>9. Vérifier votre connexion
Vérifiez la connexion de hello. Pour chaque passerelle de réseau virtuel, procédez comme hello suivant :

1. Recherchez le panneau hello pour la passerelle de réseau virtuel hello. Par exemple, **TestVNet4GW**. 
2. Dans le panneau de passerelle de réseau virtuel hello, cliquez sur **connexions** Panneau de connexions tooview hello pour la passerelle de réseau virtuel hello.

Afficher les connexions hello et vérifier l’état de hello. Une fois la connexion de hello est créée, vous verrez **Succeeded** et **connecté** comme hello des valeurs d’état.

![Réussite](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Réussite")

Vous pouvez double-cliquer sur chaque connexion séparément tooview plus d’informations sur la connexion de hello.

![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")

## <a name="faq"></a>Forum Aux Questions sur l’interconnexion de réseaux virtuels
Afficher les détails de hello Forum aux questions pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel.

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Étapes suivantes
Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Consultez hello [documentation de Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) pour plus d’informations.
