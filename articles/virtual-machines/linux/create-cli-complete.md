---
title: aaaCreate un environnement Linux avec hello Azure CLI 2.0 | Documents Microsoft
description: "Créer des stockage, un VM Linux, un réseau virtuel et du sous-réseau, un équilibreur de charge, une carte réseau, une adresse IP publique et un groupe de sécurité réseau, tous les à partir de hello d’arrière-plan à l’aide de hello Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a>Créer une machine virtuelle de Linux complète avec hello CLI d’Azure
tooquickly créer un ordinateur virtuel (VM) dans Azure, vous pouvez utiliser une seule commande CLI d’Azure qui utilise toocreate de valeurs par défaut tout requis prenant en charge des ressources. Les ressources telles que le réseau virtuel, l’adresse IP publique et les règles de groupe de sécurité réseau sont automatiquement créées. Pour plus de contrôle de votre environnement de production, utilisez, vous pouvez créer ces ressources à l’avance et puis ajoutez votre toothem de machines virtuelles. Cet article vous guide tout au long de la toocreate une machine virtuelle et à chacun des hello une par une des ressources de support.

Assurez-vous que vous avez installé hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et le compte connecté tooan Azure avec [ouverture de session az](/cli/azure/#login).

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.

## <a name="create-resource-group"></a>Créer un groupe de ressources
Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. Un groupe de ressources doit être créé avant la machine virtuelle et les ressources de réseau virtuel associées. Créer le groupe de ressources hello avec [az groupe créer](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az group create --name myResourceGroup --location eastus
```

Par défaut, la sortie de hello des commandes CLI d’Azure est au format JSON (JavaScript Object Notation). liste de tooa sortie toochange hello par défaut ou une table, par exemple, utilisez [az configurer--sortie](/cli/azure/#configure). Vous pouvez également ajouter `--output` commande tooany pour une seule fois modifier dans le format de sortie. Hello suivant montre la sortie JSON hello de hello `az group create` commande :

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a>Créer un réseau virtuel et un sous-réseau
Ensuite, vous créez un réseau virtuel dans Azure et un sous-réseau dans toowhich, vous pouvez créer vos machines virtuelles. Utilisez [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create) toocreate un réseau virtuel nommé *myVnet* avec hello *192.168.0.0/16* préfixe d’adresse. Ajoutez un sous-réseau nommé *mySubnet* avec le préfixe d’adresse de hello *192.168.1.0/24*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

sortie de Hello montre sous-réseau hello comme logiquement créé à l’intérieur du réseau virtuel de hello :

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a>Créer une adresse IP publique
Créons à présent une adresse IP publique avec la commande [az network public-ip create](/cli/azure/network/public-ip#create). Cette adresse IP publique permet de vous tooconnect tooyour machines virtuelles à partir de hello Internet. Comme adresse par défaut de hello est dynamique, nous avons également créer une entrée DNS nommée avec hello `--domain-name-label` option. Hello exemple suivant crée une adresse IP publique nommée *myPublicIP* portant le nom DNS de hello de *mypublicdns*. Étant donné que le nom DNS de hello doit être unique, fournir votre propre nom DNS unique :

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

Output:

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a>Créer un groupe de sécurité réseau
flux de hello toocontrol du trafic vers et depuis vos machines virtuelles, créez un groupe de sécurité réseau. Un groupe de sécurité réseau peut être appliqué tooa carte réseau ou sous-réseau. Hello exemple suivant utilise [az réseau nsg créer](/cli/azure/network/nsg#create) toocreate un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

Vous définissez des règles qui autorisent ou refusent un trafic spécifique hello. tooallow les connexions entrantes sur le port 22 (toosupport SSH), créez une règle de trafic entrant pour le groupe de sécurité réseau hello avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create). Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

tooallow les connexions entrantes sur le port 80 (trafic web de toosupport), ajoutez une autre règle de groupe de sécurité réseau. Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRuleHTTP*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

Examiner le groupe de sécurité réseau hello et les règles avec [az réseau nsg afficher](/cli/azure/network/nsg#show):

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

Output:

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooInternet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a>Créer une carte d’interface réseau virtuelle
Cartes d’interface réseau virtuelle (NIC) sont disponibles par programme, car vous pouvez appliquer des règles tootheir utilisation. Vous pouvez également avoir plusieurs cartes. Suivant de hello [créer des cartes réseau du réseau az](/cli/azure/network/nic#create) de commande, vous créez une carte réseau nommée *myNic* et l’associer à un groupe de sécurité réseau hello. adresse IP publique de Hello *myPublicIP* est également associé de la carte réseau virtuelle de hello.

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

Output:

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a>Créer un groupe à haute disponibilité
Les groupes à haute disponibilité aident à diffuser vos machines virtuelles sur des domaines d’erreur et des domaines de mise à jour. Même si vous créez uniquement une machine virtuelle dès maintenant, il s’agit des meilleures pratiques toouse disponibilité jeux toomake il plus facile tooexpand Bonjour futures. 

Les domaines d’erreur désignent un groupe de machines virtuelles partageant une source d’alimentation et un commutateur réseau communs. Par défaut, hello virtuels qui sont configurés au sein de votre jeu de disponibilité sont séparées à travers des domaines d’erreur toothree. En cas de problème matériel dans l’un de ces domaines d’erreur, toutes les machines virtuelles exécutant votre application ne sont pas affectées.

Indiquent les domaines de mise à jour des ordinateurs virtuels et le matériel physique sous-jacent qui peut être redémarré à hello même temps. Pendant les maintenances, commande hello dans la mise à jour des domaines sont redémarrés n’est peut-être pas séquentiel, mais une mise à jour qu’un seul domaine est redémarré à la fois.

Azure distribue automatiquement les machines virtuelles entre les domaines d’erreur et la mise à jour de hello lorsque vous les placez dans un ensemble de disponibilité. Pour plus d’informations, consultez [gestion de la disponibilité de hello de machines virtuelles](manage-availability.md).

Créez un groupe à haute disponibilité pour votre machine virtuelle avec la commande [az vm availability-set create](/cli/azure/vm/availability-set#create). Hello exemple suivant crée un groupe à haute disponibilité nommée *myAvailabilitySet*:

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

Hello sortie notes des domaines d’erreur et domaines de mise à jour :

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-hello-linux-vms"></a>Créer des machines virtuelles Linux hello
Vous avez créé toosupport de ressources réseau hello machines virtuelles accessibles sur Internet. Maintenant, créez une machine virtuelle et sécurisez-la avec une clé SSH. Dans ce cas, nous allons toocreate une VM Ubuntu selon hello LTS plus récente. Vous pouvez trouver des images supplémentaires avec la commande [az vm image list](/cli/azure/vm/image#list), comme décrit dans l’article sur la [recherche d’images de machine virtuelle Azure](cli-ps-findimage.md).

Nous avons également spécifier un toouse clé SSH pour l’authentification. Si vous ne disposez pas d’une paire de clés publiques SSH, vous pouvez [créez-les](mac-create-ssh-keys.md) ou utilisez hello `--generate-ssh-keys` paramètre toocreate pour vous. Si vous utilisez déjà une paire de clés, ce paramètre utilise les clés existantes dans `~/.ssh`.

Créer hello machine virtuelle en rassemblant tous nos ressources et informations avec hello [az vm créer](/cli/azure/vm#create) commande. Hello exemple suivant crée un ordinateur virtuel nommé *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour machine virtuelle avec hello entrée DNS que vous avez fourni lorsque vous avez créé l’adresse IP publique de hello. Cela `fqdn` est indiqué dans la sortie de hello lorsque vous créez votre machine virtuelle :

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Output:

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

Vous pouvez installer NGINX et toohello de flux de trafic hello machine virtuelle. Installez NGINX comme suit :

```bash
sudo apt-get install -y nginx
```

site NGINX toosee hello par défaut en action, ouvrez votre navigateur web, puis entrez votre nom de domaine complet :

![Site NGINX par défaut sur votre machine virtuelle](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a>Exporter en tant que modèle
Que se passe-t-il si vous souhaitez maintenant toocreate un environnement de développement supplémentaire avec hello mêmes paramètres, ou un environnement de production qui lui correspond ? Le Gestionnaire de ressources utilise des modèles JSON qui définissent tous les paramètres de hello pour votre environnement. Vous créez des environnements entiers en faisant référence à ce modèle JSON. Vous pouvez [créer manuellement des modèles JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exporter un modèle JSON environnement toocreate hello existant pour vous. Utilisez [exportation de groupe az](/cli/azure/group#export) tooexport votre ressource de groupe comme suit :

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

Cette commande crée hello `myResourceGroup.json` fichier dans votre répertoire de travail actuel. Lorsque vous créez un environnement à partir de ce modèle, vous êtes invité pour tous les noms de ressource hello. Vous pouvez remplir ces noms dans votre fichier de modèle en ajoutant hello `--include-parameter-default-value` paramètre toohello `az group export` commande. Modifier les noms de ressources JSON modèle toospecify hello, ou [créer un fichier parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) qui spécifie les noms de ressources hello.

toocreate un environnement à partir de votre modèle, utilisez [créer de déploiement de groupe az](/cli/azure/group/deployment#create) comme suit :

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

Vous souhaiterez peut-être tooread [plus sur la façon toodeploy à partir de modèles](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Découvrez comment tooincrementally les environnements de mise à jour, utilisez le fichier de paramètres hello et accéder aux modèles à partir d’un emplacement de stockage unique.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt toobegin utilisation de plusieurs composants réseau et les machines virtuelles. Vous pouvez utiliser cette toobuild d’environnement exemple votre application à l’aide de composants hello introduits ici.
