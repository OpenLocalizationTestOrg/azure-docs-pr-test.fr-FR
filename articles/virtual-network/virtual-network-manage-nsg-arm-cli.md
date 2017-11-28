---
title: "aaaManage réseau des groupes de sécurité - Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment les groupes de sécurité réseau toomanage à l’aide de hello Azure interface de ligne de commande (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="ce3a5-103">Gérer des groupes de sécurité réseau à l’aide de hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ce3a5-103">Manage network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ce3a5-104">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="ce3a5-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="ce3a5-105">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="ce3a5-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello</span><span class="sxs-lookup"><span data-stu-id="ce3a5-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="ce3a5-107">[Azure CLI 2.0](#View-existing-NSGs) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)</span><span class="sxs-lookup"><span data-stu-id="ce3a5-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for hello resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ce3a5-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ce3a5-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ce3a5-109">Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="ce3a5-110">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="ce3a5-110">Prerequisite</span></span>
<span data-ttu-id="ce3a5-111">Si vous n’avez pas encore, installer et configurer hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ce3a5-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="ce3a5-112">Afficher les groupes de sécurité réseau existants</span><span class="sxs-lookup"><span data-stu-id="ce3a5-112">View existing NSGs</span></span>
<span data-ttu-id="ce3a5-113">liste de hello tooview de groupes de sécurité réseau dans un groupe de ressources spécifique, exécutez hello [liste de groupe de sécurité réseau réseau az](/cli/azure/network/nsg#list) avec un `-o table` format de sortie :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-113">tooview hello list of NSGs in a specific resource group, run hello [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="ce3a5-114">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="ce3a5-115">Répertorier toutes les règles pour un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ce3a5-115">List all rules for an NSG</span></span>
<span data-ttu-id="ce3a5-116">règles de hello tooview d’un groupe de sécurité réseau nommé **NSG-FrontEnd**, hello exécutez [az réseau nsg afficher](/cli/azure/network/nsg#show) à l’aide de la commande une [filtre de requête JMESPATH](/cli/azure/query-az-cli2) et hello `-o table` format de sortie :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and hello `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="ce3a5-117">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="ce3a5-118">Vous pouvez également utiliser [liste de règles du groupe de sécurité réseau az réseau](/cli/azure/network/nsg/rule#list) toolist uniquement hello règles personnalisées à partir d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) toolist only hello custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="ce3a5-119">Afficher les associations de groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ce3a5-119">View NSG associations</span></span>

<span data-ttu-id="ce3a5-120">tooview hello de quelles ressources **NSG-FrontEnd** groupe de sécurité réseau est hello associez, exécutez `az network nsg show` commande comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="ce3a5-121">Recherchez hello **networkInterfaces** et **sous-réseaux** propriétés comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-121">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

<span data-ttu-id="ce3a5-122">Dans l’exemple hello ci-dessus, hello groupe de sécurité réseau n’est pas associé tooany les interfaces réseau (NIC), et il s’agit de sous-réseau associé tooa nommé **frontal**.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-122">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="ce3a5-123">Ajouter une règle</span><span class="sxs-lookup"><span data-stu-id="ce3a5-123">Add a rule</span></span>
<span data-ttu-id="ce3a5-124">tooadd une règle autorisant **entrant** trafic tooport **443** à partir de n’importe quel ordinateur toohello **NSG-FrontEnd** groupe de sécurité réseau, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="ce3a5-125">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a><span data-ttu-id="ce3a5-126">Modifier une règle</span><span class="sxs-lookup"><span data-stu-id="ce3a5-126">Change a rule</span></span>
<span data-ttu-id="ce3a5-127">règle de hello toochange créé ci-dessus tooallow le trafic entrant provenance hello **Internet** uniquement, exécutez hello [mise à jour des règles nsg réseau az](/cli/azure/network/nsg/rule#update) commande :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-127">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="ce3a5-128">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a><span data-ttu-id="ce3a5-129">Supprimer une règle</span><span class="sxs-lookup"><span data-stu-id="ce3a5-129">Delete a rule</span></span>
<span data-ttu-id="ce3a5-130">règle de hello toodelete créé ci-dessus, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-130">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="ce3a5-131">Associer un groupe de sécurité réseau de tooa carte réseau</span><span class="sxs-lookup"><span data-stu-id="ce3a5-131">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="ce3a5-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** carte réseau, utilisez hello [mise à jour de la carte réseau az réseau](/cli/azure/network/nic#update) commande :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, use hello [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="ce3a5-133">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-133">Expected output:</span></span>

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="ce3a5-134">Dissocier un groupe de sécurité réseau d’une carte réseau</span><span class="sxs-lookup"><span data-stu-id="ce3a5-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="ce3a5-135">toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **TestNICWeb1** carte réseau, exécutez hello [mise à jour des règles nsg réseau az](/cli/azure/network/nsg/rule#update) réexécutez la commande, mais remplacez hello `--network-security-group` argument avec une chaîne vide (`""`).</span><span class="sxs-lookup"><span data-stu-id="ce3a5-135">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="ce3a5-136">Dans la sortie de hello, hello `networkSecurityGroup` clé a la valeur toonull.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-136">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="ce3a5-137">Dissocier un groupe de sécurité réseau d’un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="ce3a5-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="ce3a5-138">toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **frontal** sous-réseau, exécutez à nouveau les hello [mise à jour des règles nsg réseau az](/cli/azure/network/nsg/rule#update) réexécutez la commande, mais remplacez hello `--network-security-group` argument avec une chaîne vide (`""`).</span><span class="sxs-lookup"><span data-stu-id="ce3a5-138">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, again run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="ce3a5-139">Dans la sortie de hello, hello `networkSecurityGroup` clé a la valeur toonull.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-139">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="ce3a5-140">Associez un sous-réseau de tooa du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ce3a5-140">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="ce3a5-141">tooassociate hello **NSG-FrontEnd** NSG toohello **frontal** sous-réseau exécuter à nouveau, hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-141">tooassociate hello **NSG-FrontEnd** NSG toohello **FrontEnd** subnet again, run hello following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="ce3a5-142">Dans la sortie de hello, hello `networkSecurityGroup` clé a quelque chose de similaire pour la valeur de hello :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-142">In hello output, hello `networkSecurityGroup` key has something similar for hello value:</span></span>

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a><span data-ttu-id="ce3a5-143">Suppression d'un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ce3a5-143">Delete an NSG</span></span>
<span data-ttu-id="ce3a5-144">Vous ne pouvez supprimer un groupe de sécurité réseau si elle n’est pas associé à tooany ressource.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-144">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="ce3a5-145">toodelete un groupe de sécurité réseau, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-145">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="ce3a5-146">ressources de hello toocheck associés tooan NSG, exécutez hello `azure network nsg show` comme indiqué dans [associations de groupes de sécurité réseau vue](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="ce3a5-146">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="ce3a5-147">Si hello NSG est associé tooany cartes réseau, exécutez hello `azure network nic set` comme indiqué dans [dissocier un groupe de sécurité réseau à partir d’une carte réseau](#Dissociate-an-NSG-from-a-NIC) pour chaque carte réseau.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-147">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="ce3a5-148">Si hello NSG est associé tooany sous-réseau, exécutez hello `azure network vnet subnet set` comme indiqué dans [dissocier un groupe de sécurité réseau à partir d’un sous-réseau](#Dissociate-an-NSG-from-a-subnet) pour chaque sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-148">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="ce3a5-149">toodelete hello NSG, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ce3a5-149">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="ce3a5-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ce3a5-150">Next steps</span></span>
* <span data-ttu-id="ce3a5-151">[Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="ce3a5-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

