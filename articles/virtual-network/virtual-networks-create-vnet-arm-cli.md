---
title: "aaaCreate un réseau virtuel - Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment un réseau virtuel à l’aide de toocreate hello Azure CLI 2.0."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a>Créer un réseau virtuel à l’aide de hello Azure CLI 2.0

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure propose deux modèles de déploiement : Azure Resource Manager et classique. Microsoft recommande de créer des ressources via le modèle de déploiement du Gestionnaire de ressources hello. toolearn en savoir plus sur hello différences entre hello deux modèles, lire hello [modèles de déploiement Azure de comprendre](../azure-resource-manager/resource-manager-deployment-model.md) l’article.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello
- [Azure CLI 2.0](#create-a-virtual-network) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)'
 
    Vous pouvez également créer un réseau virtuel via le Gestionnaire de ressources à l’aide d’autres outils ou créer un réseau virtuel via le modèle de déploiement classique hello en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [INTERFACE DE LIGNE DE COMMANDE](virtual-networks-create-vnet-arm-cli.md)
> * [Modèle](virtual-networks-create-vnet-arm-template-click.md)
> * [Portail (classique)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (classique)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [Interface de ligne de commande (classique)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a>Créez un réseau virtuel

un réseau virtuel à l’aide de toocreate hello Azure CLI 2.0, hello complète comme suit :

1. Installer et configurer hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

2. Créer un groupe de ressources pour votre réseau virtuel à l’aide de hello [création de groupe de az](/cli/azure/group#create) avec hello `--name` et `--location` arguments :

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. Créez un réseau virtuel et un sous-réseau :

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    Sortie attendue :
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    Paramètres utilisés :

    - `--name TestVNet`: Nom de hello toobe de réseau virtuel créé.
    - `--resource-group TestRG`: # hello nom groupe de ressources qui contrôle les ressources hello. 
    - `--location centralus`: hello emplacement dans le toodeploy.
    - `--address-prefix 192.168.0.0/16`: hello préfixe d’adresse et de bloc.  
    - `--subnet-name FrontEnd`: nom hello du sous-réseau de hello.
    - `--subnet-prefix 192.168.1.0/24`: hello préfixe d’adresse et de bloc.

    toolist hello des informations de base toouse Bonjour suivant de commande, vous pouvez interroger à l’aide du réseau virtuel hello un [filtre de requête](/cli/azure/query-az-cli2):

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    Ce qui donne hello suivant de sortie :

        Where      Name      Group

        centralus  TestVNet  TestRG

4. Créez un sous-réseau :

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    Sortie attendue :

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    Paramètres utilisés :

    - `--address-prefix 192.168.2.0/24` : bloc CIDR de sous-réseau.
    - `--name BackEnd`: Nom de sous-réseau hello.
    - `--resource-group TestRG`: groupe de ressources hello.
    - `--vnet-name TestVNet`: nom hello Hello propriétaire du réseau virtuel.

5. Propriétés de la requête hello de hello nouveau réseau virtuel :

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    Sortie attendue :

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. Interroger les propriétés de hello de sous-réseaux de hello :

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    Sortie attendue :

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooconnect :

- Un réseau virtuel tooa de machine virtuelle (VM) en lisant hello [créer un VM Linux](../virtual-machines/linux/quick-create-cli.md) l’article. Au lieu de créer un réseau virtuel et un sous-réseau dans les étapes de hello d’articles de hello, vous pouvez sélectionner un réseau virtuel existant et le sous-réseau tooconnect une machine virtuelle.
- Hello des réseaux virtuels tooother de réseau virtuel en lisant hello [connecter des réseaux virtuels](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) l’article.
- Hello réseau virtuel tooan réseau local à l’aide d’un réseau privé virtuel (VPN) site à site ou un circuit ExpressRoute. Découvrez comment en lecture hello [connecter un réseau local de tooan de réseau virtuel à l’aide d’un VPN de site à site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) et [lier un circuit ExpressRoute de tooan réseau virtuel](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
