---
title: "les adresses IP privées aaaConfigure pour les machines virtuelles - Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment les adresses IP privées tooconfigure pour les ordinateurs virtuels à l’aide de hello Azure interface de ligne de commande (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="8b8c2-103">Configurer des adresses IP privées pour un ordinateur virtuel à l’aide de hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8b8c2-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="8b8c2-104">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="8b8c2-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="8b8c2-105">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="8b8c2-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello</span><span class="sxs-lookup"><span data-stu-id="8b8c2-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="8b8c2-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)</span><span class="sxs-lookup"><span data-stu-id="8b8c2-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8b8c2-108">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="8b8c2-109">Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement classique hello](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8b8c2-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="8b8c2-110">Hello exemples Azure CLI 2.0 de commandes ci-dessous s’attendre à un environnement simple déjà créé.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="8b8c2-111">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello décrit dans [créer un réseau virtuel](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8b8c2-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="8b8c2-112">Spécifier une adresse IP privée statique lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8b8c2-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="8b8c2-113">toocreate un ordinateur virtuel nommé *DNS01* Bonjour *frontal* sous-réseau d’un réseau virtuel nommé *TestVNet* avec une adresse IP privée statique de *192.168.1.101*, Suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="8b8c2-114">Si vous n’avez pas encore, installer et configurer hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8b8c2-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="8b8c2-115">Créer une adresse IP publique pour hello VM par hello [az réseau public-ip créer](/cli/azure/network/public-ip#create) commande.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="8b8c2-116">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8b8c2-117">Vous voulez ou devez toouse des valeurs différentes pour que les arguments de cette et les étapes suivantes, en fonction de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="8b8c2-118">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-118">Expected output:</span></span>
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * <span data-ttu-id="8b8c2-119">`--resource-group`: Nom du groupe de ressources hello dans le toocreate hello adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="8b8c2-120">`--name`: Nom de l’adresse IP publique hello.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="8b8c2-121">`--location`: Région azure qui toocreate hello adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="8b8c2-122">Exécutez hello [créer des cartes réseau du réseau az](/cli/azure/network/nic#create) commande toocreate une carte réseau avec une adresse IP statique privée.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="8b8c2-123">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="8b8c2-124">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-124">Expected output:</span></span>
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    <span data-ttu-id="8b8c2-125">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-125">Parameters:</span></span>

    * <span data-ttu-id="8b8c2-126">`--private-ip-address`: Statique adresse IP privée pour hello carte réseau.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="8b8c2-127">`--vnet-name`: Nom de réseau virtuel de hello dans le toocreate hello carte réseau.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="8b8c2-128">`--subnet`: Nom de sous-réseau hello dans le hello toocreate carte réseau.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="8b8c2-129">Exécutez hello [créer de machine virtuelle azure](/cli/azure/vm/nic#create) commande toocreate hello machine virtuelle en utilisant l’adresse IP publique hello et la carte réseau créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="8b8c2-130">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-130">hello list shown after hello output explains hello parameters used.</span></span>
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    <span data-ttu-id="8b8c2-131">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-131">Expected output:</span></span>
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   <span data-ttu-id="8b8c2-132">Paramètres de base de hello [az vm créer](/cli/azure/vm#create) paramètres.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="8b8c2-133">`--nics`: Nom Hello de toowhich hello carte réseau virtuelle est attachée.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="8b8c2-134">Récupérer des informations d’adresse IP privée statique pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8b8c2-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="8b8c2-135">tooview hello adresse IP privée statique que vous avez créé, exécutez hello suivant commande CLI d’Azure et observer les valeurs hello pour *IP privée de la méthode d’allocation* et *adresse IP privée*:</span><span class="sxs-lookup"><span data-stu-id="8b8c2-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="8b8c2-136">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="8b8c2-137">toodisplay hello plus précisément les informations IP spécifiques de hello carte réseau pour cette machine virtuelle, hello de requête carte réseau :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="8b8c2-138">sortie de Hello est quelque chose comme :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="8b8c2-139">Supprimer une adresse IP privée statique d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8b8c2-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="8b8c2-140">Vous ne pouvez pas supprimer une adresse IP privée statique à partir d’une carte réseau dans l’interface Azure CLI des déploiements Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="8b8c2-141">Vous devez respecter les consignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-141">You must:</span></span>
- <span data-ttu-id="8b8c2-142">Créer une nouvelle carte réseau qui utilise une adresse IP dynamique</span><span class="sxs-lookup"><span data-stu-id="8b8c2-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="8b8c2-143">Définir hello NIC sur hello VM hello nouvellement créée de carte réseau.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="8b8c2-144">toochange hello NIC pour hello machine virtuelle utilisée dans les commandes hello ci-dessus, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="8b8c2-145">Exécutez hello **créer des cartes réseau du réseau azure** commande toocreate une nouvelle carte réseau à l’aide de l’allocation dynamique d’IP avec une nouvelle adresse IP.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="8b8c2-146">Notez que, car aucune adresse IP n’est spécifié, méthode d’allocation de hello est **dynamique**.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="8b8c2-147">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-147">Expected output:</span></span>

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. <span data-ttu-id="8b8c2-148">Exécutez hello **ensemble de la machine virtuelle azure** commande toochange hello carte réseau utilisée par hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="8b8c2-149">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8b8c2-149">Expected output:</span></span>
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > <span data-ttu-id="8b8c2-150">Si hello machine virtuelle est suffisante toohave plusieurs cartes réseau, exécutez hello **supprimer les cartes réseau du réseau azure** commande hello de toodelete ancien NIC.</span><span class="sxs-lookup"><span data-stu-id="8b8c2-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="8b8c2-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8b8c2-151">Next steps</span></span>
* <span data-ttu-id="8b8c2-152">En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="8b8c2-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="8b8c2-153">En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="8b8c2-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="8b8c2-154">Consultez hello [API REST de IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b8c2-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

