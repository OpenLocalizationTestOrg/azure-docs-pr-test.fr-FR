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
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a>Gérer des groupes de sécurité réseau à l’aide de hello Azure CLI 2.0

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete 

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes : 

- [Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello 
- [Azure CLI 2.0](#View-existing-NSGs) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a>Configuration requise
Si vous n’avez pas encore, installer et configurer hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login). 


## <a name="view-existing-nsgs"></a>Afficher les groupes de sécurité réseau existants
liste de hello tooview de groupes de sécurité réseau dans un groupe de ressources spécifique, exécutez hello [liste de groupe de sécurité réseau réseau az](/cli/azure/network/nsg#list) avec un `-o table` format de sortie :

```azurecli
az network nsg list -g RG-NSG -o table
```

Sortie attendue :

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a>Répertorier toutes les règles pour un groupe de sécurité réseau
règles de hello tooview d’un groupe de sécurité réseau nommé **NSG-FrontEnd**, hello exécutez [az réseau nsg afficher](/cli/azure/network/nsg#show) à l’aide de la commande une [filtre de requête JMESPATH](/cli/azure/query-az-cli2) et hello `-o table` format de sortie :

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

Sortie attendue :

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
> Vous pouvez également utiliser [liste de règles du groupe de sécurité réseau az réseau](/cli/azure/network/nsg/rule#list) toolist uniquement hello règles personnalisées à partir d’un groupe de sécurité réseau.
>

## <a name="view-nsg-associations"></a>Afficher les associations de groupes de sécurité réseau

tooview hello de quelles ressources **NSG-FrontEnd** groupe de sécurité réseau est hello associez, exécutez `az network nsg show` commande comme indiqué ci-dessous. 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

Recherchez hello **networkInterfaces** et **sous-réseaux** propriétés comme indiqué ci-dessous :

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

Dans l’exemple hello ci-dessus, hello groupe de sécurité réseau n’est pas associé tooany les interfaces réseau (NIC), et il s’agit de sous-réseau associé tooa nommé **frontal**.

## <a name="add-a-rule"></a>Ajouter une règle
tooadd une règle autorisant **entrant** trafic tooport **443** à partir de n’importe quel ordinateur toohello **NSG-FrontEnd** groupe de sécurité réseau, entrez hello de commande suivante :

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

Sortie attendue :

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

## <a name="change-a-rule"></a>Modifier une règle
règle de hello toochange créé ci-dessus tooallow le trafic entrant provenance hello **Internet** uniquement, exécutez hello [mise à jour des règles nsg réseau az](/cli/azure/network/nsg/rule#update) commande :

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

Sortie attendue :

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

## <a name="delete-a-rule"></a>Supprimer une règle
règle de hello toodelete créé ci-dessus, exécutez hello de commande suivante :

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a>Associer un groupe de sécurité réseau de tooa carte réseau
tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** carte réseau, utilisez hello [mise à jour de la carte réseau az réseau](/cli/azure/network/nic#update) commande :

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

Sortie attendue :

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

## <a name="dissociate-an-nsg-from-a-nic"></a>Dissocier un groupe de sécurité réseau d’une carte réseau

toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **TestNICWeb1** carte réseau, exécutez hello [mise à jour des règles nsg réseau az](/cli/azure/network/nsg/rule#update) réexécutez la commande, mais remplacez hello `--network-security-group` argument avec une chaîne vide (`""`).

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

Dans la sortie de hello, hello `networkSecurityGroup` clé a la valeur toonull.

## <a name="dissociate-an-nsg-from-a-subnet"></a>Dissocier un groupe de sécurité réseau d’un sous-réseau
toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **frontal** sous-réseau, exécutez à nouveau les hello [mise à jour des règles nsg réseau az](/cli/azure/network/nsg/rule#update) réexécutez la commande, mais remplacez hello `--network-security-group` argument avec une chaîne vide (`""`).

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

Dans la sortie de hello, hello `networkSecurityGroup` clé a la valeur toonull.

## <a name="associate-an-nsg-tooa-subnet"></a>Associez un sous-réseau de tooa du groupe de sécurité réseau
tooassociate hello **NSG-FrontEnd** NSG toohello **frontal** sous-réseau exécuter à nouveau, hello de commande suivante :

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

Dans la sortie de hello, hello `networkSecurityGroup` clé a quelque chose de similaire pour la valeur de hello :

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

## <a name="delete-an-nsg"></a>Suppression d'un groupe de sécurité réseau
Vous ne pouvez supprimer un groupe de sécurité réseau si elle n’est pas associé à tooany ressource. toodelete un groupe de sécurité réseau, suivez les étapes de hello ci-dessous.

1. ressources de hello toocheck associés tooan NSG, exécutez hello `azure network nsg show` comme indiqué dans [associations de groupes de sécurité réseau vue](#View-NSGs-associations).
2. Si hello NSG est associé tooany cartes réseau, exécutez hello `azure network nic set` comme indiqué dans [dissocier un groupe de sécurité réseau à partir d’une carte réseau](#Dissociate-an-NSG-from-a-NIC) pour chaque carte réseau. 
3. Si hello NSG est associé tooany sous-réseau, exécutez hello `azure network vnet subnet set` comme indiqué dans [dissocier un groupe de sécurité réseau à partir d’un sous-réseau](#Dissociate-an-NSG-from-a-subnet) pour chaque sous-réseau.
4. toodelete hello NSG, exécutez hello de commande suivante :

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a>Étapes suivantes
* [Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.

