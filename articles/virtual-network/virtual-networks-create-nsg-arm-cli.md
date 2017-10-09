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
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="475eb-103">Créer des groupes de sécurité à l’aide de hello Azure CLI 2.0 réseau</span><span class="sxs-lookup"><span data-stu-id="475eb-103">Create network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="475eb-104">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="475eb-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="475eb-105">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="475eb-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="475eb-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello</span><span class="sxs-lookup"><span data-stu-id="475eb-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="475eb-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)</span><span class="sxs-lookup"><span data-stu-id="475eb-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="475eb-108">l’exemple Hello Azure CLI 2.0 les commandes suivantes attendent un simple environnement déjà créé en fonction de scénario hello précédent.</span><span class="sxs-lookup"><span data-stu-id="475eb-108">hello sample Azure CLI 2.0 commands following expect a simple environment already created based on hello scenario preceding.</span></span> 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a><span data-ttu-id="475eb-109">Créer hello NSG pour hello `FrontEnd` sous-réseau</span><span class="sxs-lookup"><span data-stu-id="475eb-109">Create hello NSG for hello `FrontEnd` subnet</span></span>

<span data-ttu-id="475eb-110">toocreate un groupe de sécurité réseau nommé *NSG-FrontEnd* selon le scénario hello précédent, procédez comme suit des étapes hello.</span><span class="sxs-lookup"><span data-stu-id="475eb-110">toocreate an NSG named *NSG-FrontEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="475eb-111">Si vous n’avez pas encore, installer et configurer hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="475eb-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="475eb-112">Créer un groupe de sécurité réseau à l’aide de hello [az réseau nsg créer](/cli/azure/network/nsg#create) commande.</span><span class="sxs-lookup"><span data-stu-id="475eb-112">Create an NSG using hello [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="475eb-113">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="475eb-113">Parameters:</span></span>
   
   * <span data-ttu-id="475eb-114">`--resource-group`: Nom du groupe de ressources hello où hello NSG est créé.</span><span class="sxs-lookup"><span data-stu-id="475eb-114">`--resource-group`: Name of hello resource group where hello NSG is created.</span></span> <span data-ttu-id="475eb-115">Pour notre scénario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="475eb-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="475eb-116">`--location`: Région azure où hello nouveau groupe de sécurité réseau est créé.</span><span class="sxs-lookup"><span data-stu-id="475eb-116">`--location`: Azure region where hello new NSG is created.</span></span> <span data-ttu-id="475eb-117">Pour notre scénario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="475eb-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="475eb-118">`--name`: Nom hello nouveau groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="475eb-118">`--name`: Name for hello new NSG.</span></span> <span data-ttu-id="475eb-119">Pour notre scénario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="475eb-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="475eb-120">Hello attendu de sortie reste un peu d’informations, y compris une liste de toutes les règles par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="475eb-120">hello expected output is quite a bit of information including a list of all hello default rules.</span></span> <span data-ttu-id="475eb-121">Hello suivant montre les règles par défaut hello à l’aide d’un filtre de requête JMESPATH avec hello `table` format de sortie :</span><span class="sxs-lookup"><span data-stu-id="475eb-121">hello following example shows hello default rules using a JMESPATH query filter with hello `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="475eb-122">Output:</span><span class="sxs-lookup"><span data-stu-id="475eb-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="475eb-123">Créer une règle qui autorise l’accès tooport 3389 (RDP) à partir de hello Internet avec hello [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) commande.</span><span class="sxs-lookup"><span data-stu-id="475eb-123">Create a rule that allows access tooport 3389 (RDP) from hello Internet with hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="475eb-124">En fonction de l’interpréteur de commandes hello que vous utilisez, vous devrez peut-être toomodify hello `*` caractères dans les arguments hello suite de manière à ne pas l’argument hello tooexpand avant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="475eb-124">Depending on hello shell you are using, you might need toomodify hello `*` character in hello arguments following so as not tooexpand hello argument before execution.</span></span>
   
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
   
    <span data-ttu-id="475eb-125">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="475eb-125">Expected output:</span></span>
   
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

    <span data-ttu-id="475eb-126">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="475eb-126">Parameters:</span></span>

    * <span data-ttu-id="475eb-127">`--resource-group testrg`: hello toouse de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="475eb-127">`--resource-group testrg`: hello resource group toouse.</span></span> <span data-ttu-id="475eb-128">Ce paramètre est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="475eb-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="475eb-129">`--nsg-name NSG-FrontEnd`: Nom de groupe de sécurité réseau hello dans le hello règle est créée.</span><span class="sxs-lookup"><span data-stu-id="475eb-129">`--nsg-name NSG-FrontEnd`: Name of hello NSG in which hello rule is created.</span></span>
    * <span data-ttu-id="475eb-130">`--name rdp-rule`: Nom de la nouvelle règle de hello.</span><span class="sxs-lookup"><span data-stu-id="475eb-130">`--name rdp-rule`: Name for hello new rule.</span></span>
    * <span data-ttu-id="475eb-131">`--access Allow`: Niveau d’accès pour la règle hello (Deny ou autoriser).</span><span class="sxs-lookup"><span data-stu-id="475eb-131">`--access Allow`: Access level for hello rule (Deny or Allow).</span></span>
    * <span data-ttu-id="475eb-132">`--protocol Tcp`: protocole (TCP, UDP ou *).</span><span class="sxs-lookup"><span data-stu-id="475eb-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="475eb-133">`--direction Inbound`: Direction de connexion hello (entrante ou sortante).</span><span class="sxs-lookup"><span data-stu-id="475eb-133">`--direction Inbound`: Direction of hello connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="475eb-134">`--priority 100`: Priorité pour la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="475eb-134">`--priority 100`: Priority for hello rule.</span></span>
    * <span data-ttu-id="475eb-135">`--source-address-prefix Internet` : préfixe de l’adresse source dans CIDR ou à l’aide de balises par défaut.</span><span class="sxs-lookup"><span data-stu-id="475eb-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="475eb-136">`--source-port-range "*"` : port source ou plage de ports.</span><span class="sxs-lookup"><span data-stu-id="475eb-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="475eb-137">Port ouvert hello connexion.</span><span class="sxs-lookup"><span data-stu-id="475eb-137">Port that opened hello connection.</span></span>
    * <span data-ttu-id="475eb-138">`--destination-address-prefix "*"` : préfixe de l’adresse de destination dans CIDR ou à l’aide de balises par défaut.</span><span class="sxs-lookup"><span data-stu-id="475eb-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="475eb-139">`--destination-port-range 3389` : port de destination ou plage de ports.</span><span class="sxs-lookup"><span data-stu-id="475eb-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="475eb-140">Port qui reçoit la demande de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="475eb-140">Port that receives hello connection request.</span></span>



4. <span data-ttu-id="475eb-141">Créer une règle qui autorise l’accès tooport 80 (HTTP) à partir de hello Internet **créer de règle de groupe de sécurité réseau du réseau az** commande.</span><span class="sxs-lookup"><span data-stu-id="475eb-141">Create a rule that allows access tooport 80 (HTTP) from hello Internet **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="475eb-142">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="475eb-142">Expected putput:</span></span>
   
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

5. <span data-ttu-id="475eb-143">Lier hello NSG toohello **frontal** sous-réseau avec hello [mise à jour de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#update) commande.</span><span class="sxs-lookup"><span data-stu-id="475eb-143">Bind hello NSG toohello **FrontEnd** subnet with hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="475eb-144">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="475eb-144">Expected output:</span></span>
   
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

## <a name="create-hello-nsg-for-hello-backend-subnet"></a><span data-ttu-id="475eb-145">Créer hello NSG pour hello `BackEnd` sous-réseau</span><span class="sxs-lookup"><span data-stu-id="475eb-145">Create hello NSG for hello `BackEnd` subnet</span></span>
<span data-ttu-id="475eb-146">toocreate un groupe de sécurité réseau nommé *principal de groupe de sécurité réseau* selon le scénario hello précédent, procédez comme suit des étapes hello.</span><span class="sxs-lookup"><span data-stu-id="475eb-146">toocreate an NSG named *NSG-BackEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="475eb-147">Créer hello `NSG-BackEnd` NSG avec **az réseau nsg créer**.</span><span class="sxs-lookup"><span data-stu-id="475eb-147">Create hello `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="475eb-148">Comme dans l’étape 2, précédent, hello attendue de sortie est volumineuse, y compris les règles par défaut.</span><span class="sxs-lookup"><span data-stu-id="475eb-148">As in step 2, preceding, hello expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="475eb-149">Créer une règle qui autorise l’accès tooport 1433 (SQL) à partir de hello `FrontEnd` sous-réseau avec hello **créer de règle de groupe de sécurité réseau du réseau az** commande.</span><span class="sxs-lookup"><span data-stu-id="475eb-149">Create a rule that allows access tooport 1433 (SQL) from hello `FrontEnd` subnet with hello **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="475eb-150">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="475eb-150">Expected output:</span></span>

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

3. <span data-ttu-id="475eb-151">Créer une règle qui refuse l’accès toohello Internet en utilisant hello **créer de règle de groupe de sécurité réseau du réseau az** commande.</span><span class="sxs-lookup"><span data-stu-id="475eb-151">Create a rule that denies access toohello Internet using hello **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="475eb-152">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="475eb-152">Expected putput:</span></span>
   
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

4. <span data-ttu-id="475eb-153">Lier hello NSG toohello `BackEnd` sous-réseau à l’aide de hello **ensemble de sous-réseau de réseau virtuel de réseau az** commande.</span><span class="sxs-lookup"><span data-stu-id="475eb-153">Bind hello NSG toohello `BackEnd` subnet using hello **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="475eb-154">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="475eb-154">Expected output:</span></span>
   
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
