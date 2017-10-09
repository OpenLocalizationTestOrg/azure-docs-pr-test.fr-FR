---
title: "aaaCreate réseau des groupes de sécurité - Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toocreate et déployer des groupes de sécurité réseau à l’aide de hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a>Créer des groupes de sécurité à l’aide de hello Azure CLI 2.0 réseau

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete 

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes : 

- [Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello 
- [Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

l’exemple Hello Azure CLI 2.0 les commandes suivantes attendent un simple environnement déjà créé en fonction de scénario hello précédent. 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a>Créer hello NSG pour hello `FrontEnd` sous-réseau

toocreate un groupe de sécurité réseau nommé *NSG-FrontEnd* selon le scénario hello précédent, procédez comme suit des étapes hello.

1. Si vous n’avez pas encore, installer et configurer hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login). 

2. Créer un groupe de sécurité réseau à l’aide de hello [az réseau nsg créer](/cli/azure/network/nsg#create) commande. 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    Paramètres :
   
   * `--resource-group`: Nom du groupe de ressources hello où hello NSG est créé. Pour notre scénario, *TestRG*.
   * `--location`: Région azure où hello nouveau groupe de sécurité réseau est créé. Pour notre scénario, *westus*.
   * `--name`: Nom hello nouveau groupe de sécurité réseau. Pour notre scénario, *NSG-FrontEnd*.

    Hello attendu de sortie reste un peu d’informations, y compris une liste de toutes les règles par défaut de hello. Hello suivant montre les règles par défaut hello à l’aide d’un filtre de requête JMESPATH avec hello `table` format de sortie :

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   Output:

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. Créer une règle qui autorise l’accès tooport 3389 (RDP) à partir de hello Internet avec hello [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) commande.

    > [!NOTE]
    > En fonction de l’interpréteur de commandes hello que vous utilisez, vous devrez peut-être toomodify hello `*` caractères dans les arguments hello suite de manière à ne pas l’argument hello tooexpand avant l’exécution.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    Sortie attendue :
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    Paramètres :

    * `--resource-group testrg`: hello toouse de groupe de ressources. Ce paramètre est sensible à la casse.
    * `--nsg-name NSG-FrontEnd`: Nom de groupe de sécurité réseau hello dans le hello règle est créée.
    * `--name rdp-rule`: Nom de la nouvelle règle de hello.
    * `--access Allow`: Niveau d’accès pour la règle hello (Deny ou autoriser).
    * `--protocol Tcp`: protocole (TCP, UDP ou *).
    * `--direction Inbound`: Direction de connexion hello (entrante ou sortante).
    * `--priority 100`: Priorité pour la règle de hello.
    * `--source-address-prefix Internet` : préfixe de l’adresse source dans CIDR ou à l’aide de balises par défaut.
    * `--source-port-range "*"` : port source ou plage de ports. Port ouvert hello connexion.
    * `--destination-address-prefix "*"` : préfixe de l’adresse de destination dans CIDR ou à l’aide de balises par défaut.
    * `--destination-port-range 3389` : port de destination ou plage de ports. Port qui reçoit la demande de connexion hello.



4. Créer une règle qui autorise l’accès tooport 80 (HTTP) à partir de hello Internet **créer de règle de groupe de sécurité réseau du réseau az** commande.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    Sortie attendue :
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. Lier hello NSG toohello **frontal** sous-réseau avec hello [mise à jour de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#update) commande.
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    Sortie attendue :
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a>Créer hello NSG pour hello `BackEnd` sous-réseau
toocreate un groupe de sécurité réseau nommé *principal de groupe de sécurité réseau* selon le scénario hello précédent, procédez comme suit des étapes hello.

1. Créer hello `NSG-BackEnd` NSG avec **az réseau nsg créer**.
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    Comme dans l’étape 2, précédent, hello attendue de sortie est volumineuse, y compris les règles par défaut.
   
2. Créer une règle qui autorise l’accès tooport 1433 (SQL) à partir de hello `FrontEnd` sous-réseau avec hello **créer de règle de groupe de sécurité réseau du réseau az** commande.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    Sortie attendue :

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. Créer une règle qui refuse l’accès toohello Internet en utilisant hello **créer de règle de groupe de sécurité réseau du réseau az** commande.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    Sortie attendue :
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. Lier hello NSG toohello `BackEnd` sous-réseau à l’aide de hello **ensemble de sous-réseau de réseau virtuel de réseau az** commande.
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    Sortie attendue :
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
