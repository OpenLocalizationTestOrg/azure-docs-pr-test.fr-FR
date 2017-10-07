---
title: "un réseau virtuel à l’aide d’aaaCreate hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment un réseau virtuel à l’aide de toocreate hello Azure CLI 1.0 | Gestionnaire de ressources."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a>Créer un réseau virtuel à l’aide de hello CLI d’Azure

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure propose deux modèles de déploiement : Azure Resource Manager et classique. Microsoft recommande de créer des ressources via le modèle de déploiement du Gestionnaire de ressources hello. toolearn en savoir plus sur hello différences entre hello deux modèles, lire hello [modèles de déploiement Azure de comprendre](../azure-resource-manager/resource-manager-deployment-model.md) l’article.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello
- [Azure CLI 1.0](#create-a-virtual-network) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>Créez un réseau virtuel

un réseau virtuel à l’aide de toocreate hello CLI d’Azure, hello complète comme suit :

1. Installer et configurer hello CLI d’Azure par hello suivant les étapes dans hello [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) l’article.

2. Créez un réseau virtuel et un sous-réseau :

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    Sortie attendue :
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    Paramètres utilisés :

   * **--vnet**. Nom de hello toobe de réseau virtuel créé. Pour notre scénario, *TestVNet*
   * **-e (ou --address-space)**. Espace d'adressage du réseau virtuel. Pour notre scénario, *192.168.0.0*
   * **-i (ou -cidr)**. Masque de réseau au format CIDR. Pour notre scénario, *16*.
   * **-n (ou --subnet-name**). Nom du sous-réseau de première hello. Pour notre scénario, *FrontEnd*.
   * **-p (ou --subnet-start-ip)**. Adresse IP de début pour le sous-réseau, ou espace d'adressage du sous-réseau. Pour notre scénario, *192.168.1.0*.
   * **-r (ou --subnet-cidr)**. Masque de réseau au format CIDR pour le sous-réseau. Pour notre scénario, *24*.
   * **-l (ou --location)**. Région Azure où hello réseau virtuel est créé. Pour notre scénario, *Centre des États-Unis*.

3. Créez un sous-réseau :

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    Sortie attendue :

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    Paramètres utilisés :

   * **-t (ou --vnet-name**. Nom de hello réseau virtuel où le sous-réseau de hello doit être créé. Pour notre scénario, *TestVNet*.
   * **-n (ou --name)**. Nom du sous-réseau hello. Pour notre scénario, *BackEnd*.
   * **-a (ou --address-prefix)**. Bloc CIDR de sous-réseau. Pour notre scénario, *192.168.2.0/24*.
   
4. propriétés de hello tooview de hello nouveau réseau virtuel :

    ```azurecli
    azure network vnet show
    ```
   
    Sortie attendue :
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooconnect :

- Un réseau virtuel tooa de machine virtuelle (VM) en lisant hello [créer un VM Linux](../virtual-machines/linux/quick-create-cli.md) l’article. Au lieu de créer un réseau virtuel et un sous-réseau dans les étapes de hello d’articles de hello, vous pouvez sélectionner un réseau virtuel existant et le sous-réseau tooconnect une machine virtuelle.
- Hello des réseaux virtuels tooother de réseau virtuel en lisant hello [connecter des réseaux virtuels](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) l’article.
- Hello réseau virtuel tooan réseau local à l’aide d’un réseau privé virtuel (VPN) site à site ou un circuit ExpressRoute. Découvrez comment en lecture hello [connecter un réseau local de tooan de réseau virtuel à l’aide d’un VPN de site à site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) et [lier un circuit ExpressRoute de tooan réseau virtuel](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
