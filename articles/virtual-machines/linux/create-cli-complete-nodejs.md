---
title: aaaCreate un environnement Linux complet avec hello Azure CLI 1.0 | Documents Microsoft
description: "Créer des stockage, un VM Linux, un réseau virtuel et du sous-réseau, un équilibreur de charge, une carte réseau, une adresse IP publique et un groupe de sécurité réseau, tous les à partir de hello d’arrière-plan à l’aide de hello Azure CLI 1.0."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a>Créer un environnement de Linux complète avec hello Azure CLI 1.0
Dans cet article, nous créons un réseau simple avec un équilibreur de charge et deux machines virtuelles à des fins de développement et de calcul simple. Nous Guide de processus de hello par commande, jusqu'à ce que vous avez deux, sécurisez toowhich les machines virtuelles Linux que vous pouvez vous connecter à partir de n’importe où sur hello Internet. Ensuite, vous pouvez déplacer sur les environnements et les réseaux complexes toomore.

Le long de la façon de hello, vous allez découvrir la hiérarchie des dépendances hello que modèle de déploiement du Gestionnaire de ressources hello offre, et sur la quantité d’énergie il. Une fois que vous voyez comment le système de hello est créée, vous pouvez reconstruire il beaucoup plus rapidement à l’aide de [modèles Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). En outre, une fois que vous coordination des parties hello de votre environnement, la création de modèles tooautomate les devient plus facile.

environnement de Hello contient :

* Deux machines virtuelles dans un groupe à haute disponibilité.
* Un équilibreur de charge avec une règle d’équilibrage de charge sur le port 80.
* Les règles de groupe de sécurité réseau (NSG) tooprotect votre machine virtuelle à partir d’un trafic indésirable.

toocreate cet environnement personnalisé, vous devez hello dernières [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en mode de gestionnaire de ressources (`azure config mode arm`). Vous avez également besoin d’un outil d’analyse JSON. Cet exemple utilise [jq](https://stedolan.github.io/jq/).


## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello


## <a name="quick-commands"></a>Commandes rapides
Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant hello de détails section tooupload des commandes de base un tooAzure de machine virtuelle. Plus d’informations et le contexte de chaque étape se trouvent dans le reste de hello du document hello, en commençant [ici](#detailed-walkthrough).

Assurez-vous que vous avez [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) connecté et l’utilisation du mode de gestionnaire de ressources :

```azurecli
azure config mode arm
```

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.

Créer un groupe de ressources hello. Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westeurope` emplacement :

```azurecli
azure group create -n myResourceGroup -l westeurope
```

Vérifiez le groupe de ressources hello en utilisant l’analyseur JSON hello :

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Créer un compte de stockage hello. Hello exemple suivant crée un compte de stockage nommé `mystorageaccount`. (nom de compte de stockage hello doit être unique, par conséquent, fournissez votre propre nom unique).

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

Vérifiez le compte de stockage hello en utilisant l’analyseur JSON hello :

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

Créer un réseau virtuel de hello. Hello exemple suivant crée un réseau virtuel nommé `myVnet`:

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

Créez un sous-réseau. Hello exemple suivant crée un sous-réseau nommé `mySubnet`:

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

Vérifiez que hello réseau et sous-réseau virtuels en utilisant l’analyseur JSON hello :

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Créez une adresse IP publique. Hello exemple suivant crée une adresse IP publique nommée `myPublicIP` portant le nom DNS de hello de `mypublicdns`. (nom DNS de hello doit être unique, par conséquent, fournissez votre propre nom unique).

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

Créer un équilibreur de charge hello. Hello exemple suivant crée un équilibreur de charge nommé `myLoadBalancer`:

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

Créer un pool IP frontal pour l’équilibrage de charge hello et associer l’adresse IP publique hello. Hello exemple suivant crée un pool IP frontal nommé `mySubnetPool`:

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

Créer un pool d’IP hello principal pour l’équilibrage de charge hello. Hello exemple suivant crée un pool d’IP principal nommé `myBackEndPool`:

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

Permet de créer des règles de translation (NAT) d’adresse pour l’équilibrage de charge hello de réseau entrant de SSH. Hello exemple suivant crée deux règles d’équilibrage de charge, `myLoadBalancerRuleSSH1` et `myLoadBalancerRuleSSH2`:

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

Créer hello web règles NAT de trafic entrant pour hello l’équilibrage de charge. Hello exemple suivant crée une règle d’équilibreur de charge nommée `myLoadBalancerRuleWeb`:

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

Créez la sonde d’intégrité d’équilibrage de charge hello. Hello exemple suivant crée une sonde TCP nommée `myHealthProbe`:

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

Vérifiez hello équilibrage de charge, pools d’adresses IP et les règles NAT à l’aide d’analyseur JSON hello :

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

Créer hello première carte d’interface réseau (NIC). Remplacez hello `#####-###-###` sections avec votre propre ID d’abonnement Azure. Votre abonnement ID est indiqué dans la sortie de hello de **jq** lorsque vous examinez les ressources hello vous créez. Vous pouvez également afficher votre ID d’abonnement avec `azure account list`.

Hello exemple suivant crée une carte réseau nommée `myNic1`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

Créer hello seconde carte réseau. Hello exemple suivant crée une carte réseau nommée `myNic2`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

Vérifiez que hello deux cartes d’interface réseau en utilisant l’analyseur JSON hello :

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

Créer un groupe de sécurité réseau hello. Hello exemple suivant crée un groupe de sécurité réseau nommé `myNetworkSecurityGroup`:

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

Ajoutez deux règles de trafic entrant pour le groupe de sécurité réseau hello. Hello exemple suivant crée deux règles, `myNetworkSecurityGroupRuleSSH` et `myNetworkSecurityGroupRuleHTTP`:

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

Vérifiez le groupe de sécurité réseau hello et les règles de trafic entrant à l’aide d’analyseur JSON hello :

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

Liaison de sécurité réseau hello toohello deux cartes d’interface réseau de groupe :

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

Créer un groupe à haute disponibilité hello. Hello exemple suivant crée un groupe à haute disponibilité nommée `myAvailabilitySet`:

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

Créer hello première Linux VM. Hello exemple suivant crée un ordinateur virtuel nommé `myVM1`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Créer hello deuxième Linux VM. Hello exemple suivant crée un ordinateur virtuel nommé `myVM2`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Utilisez hello JSON analyseur tooverify que tout ce qui a été créé :

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

Exporter votre nouvel environnement tooa modèle tooquickly nouvelle création de nouvelles instances :

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas
Hello détaillées étapes qui suivent expliquent ce que chaque commande fait pendant la génération de votre environnement. Ces concepts sont utiles lorsque vous créez vos propres environnements personnalisés pour le développement ou la production.

Assurez-vous que vous avez [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) connecté et l’utilisation du mode de gestionnaire de ressources :

```azurecli
azure config mode arm
```

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.

## <a name="create-resource-groups-and-choose-deployment-locations"></a>Créer des groupes de ressources et choisir les emplacements de déploiement
Groupes de ressources Azure sont des entités logiques de déploiement qui contiennent des informations et des métadonnées tooenable hello logique gestion de la configuration des déploiements de ressources. Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westeurope` emplacement :

```azurecli
azure group create --name myResourceGroup --location westeurope
```

Output:

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a>Créez un compte de stockage.
Vous avez besoin de comptes de stockage pour vos disques de machine virtuelle et les disques de données supplémentaires que vous souhaitez tooadd. Vous créez des comptes de stockage presque immédiatement après avoir créé des groupes de ressources.

Nous utilisons ici hello `azure storage account create` de commande, en passant emplacement hello du compte hello, groupe de ressources hello qui contrôle et le type hello de prise en charge de stockage souhaité. Hello exemple suivant crée un compte de stockage nommé `mystorageaccount`:

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

Output:

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

tooexamine notre ressource de groupe à l’aide de hello `azure group show` de commande, nous allons utiliser hello [jq](https://stedolan.github.io/jq/) outil avec hello `--json` option de CLI d’Azure. (Vous pouvez utiliser **jsawk** ou n’importe quelle bibliothèque de langue que vous préférez tooparse hello JSON.)

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Output:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

le compte de stockage tooinvestigate hello à l’aide de hello CLI, vous devez tout d’abord clés et les noms de compte tooset hello. Remplacez le nom hello hello du compte de stockage Bonjour avec un nom que vous choisissez l’exemple suivant :

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

Vous pouvez alors visualiser facilement vos informations de stockage :

```azurecli
azure storage container list
```

Output:

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a>Créer un réseau virtuel et un sous-réseau
Ensuite vous allez tooneed toocreate un réseau virtuel en cours d’exécution dans Azure et un sous-réseau dans lequel vous pouvez créer vos machines virtuelles. Hello exemple suivant crée un réseau virtuel nommé `myVnet` avec hello `192.168.0.0/16` préfixe d’adresse :

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

Output:

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

Là encore, nous allons opter hello--json de `azure group show` et `jq` toosee comment nous mettons nos ressources. Nous disposons maintenant d’une ressource `storageAccounts` et d’une ressource `virtualNetworks`.  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Output:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

Maintenant nous allons créer un sous-réseau Bonjour `myVnet` réseau virtuel dans le hello machines virtuelles sont déployées. Nous utilisons hello `azure network vnet subnet create` commande, ainsi que des ressources hello, nous avons déjà créé : hello `myResourceGroup` groupe de ressources et hello `myVnet` réseau virtuel. Bonjour l’exemple suivant, nous ajoutons sous-réseau hello nommé `mySubnet` avec un préfixe d’adresse de sous-réseau hello `192.168.1.0/24`:

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

Output:

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

Étant donné que le sous-réseau de hello est logiquement à l’intérieur du réseau virtuel de hello, nous allons pour plus d’informations de sous-réseau hello avec une commande légèrement différente. Nous utilisons la commande Hello est `azure network vnet show`, mais nous continuons la sortie JSON hello tooexamine à l’aide de `jq`.

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Output:

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a>Créer une adresse IP publique
Maintenant nous allons créer hello adresse IP publique (PIP) que nous affectons d’équilibrage de charge tooyour. Il vous permet de tooconnect tooyour machines virtuelles à partir de hello Internet à l’aide de hello `azure network public-ip create` commande. Étant donné que l’adresse par défaut de hello est dynamique, nous créons une entrée DNS nommée Bonjour **cloudapp.azure.com** domaine à l’aide de hello `--domain-name-label` option. Hello exemple suivant crée une adresse IP publique nommée `myPublicIP` portant le nom DNS de hello de `mypublicdns`. Étant donné que le nom DNS de hello doit être unique, vous fournissez votre propre nom DNS unique :

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

Output:

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

Bonjour adresse IP publique est également une ressource de niveau supérieur, afin de voir avec `azure group show`.

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Output:

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

Vous pouvez rechercher plus d’informations de ressources, notamment le nom de domaine complet (FQDN) hello du sous-domaine de hello, à l’aide de hello complète `azure network public-ip show` commande. ressource d’adresse IP publique Hello a été allouée logiquement, mais une adresse spécifique n’a pas encore été assignée. tooobtain une adresse IP, vous allez tooneed un équilibreur de charge, nous n’avons pas encore créé.

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

Output:

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a>Créer un équilibreur de charge et des pools d’adresses IP
Lorsque vous créez un équilibreur de charge, il vous permet de toodistribute du trafic entre plusieurs machines virtuelles. Il fournit également l’application tooyour de redondance en exécutant plusieurs machines virtuelles qui répondent toouser des demandes dans l’événement hello de maintenance ou de lourdes charges. Hello exemple suivant crée un équilibreur de charge nommé `myLoadBalancer`:

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

Output:

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

Notre équilibreur de charge est relativement vide. Nous allons donc créer des pools d’adresses IP. Nous souhaitons toocreate deux pools d’adresses IP pour notre programme d’équilibrage de charge, un serveur frontal hello et un pour le back-end hello. pool d’adresses IP frontal Hello est visible publiquement. Il est également toowhich d’emplacement hello que nous affectons hello PIP que nous avons créés précédemment. Puis nous utiliser hello principal comme un emplacement pour notre tooconnect de machines virtuelles à. De cette façon, hello circulent via toohello équilibrage de charge hello machines virtuelles.

Commençons tout d’abord par créer notre pool d’adresses IP frontal. Hello exemple suivant crée un pool frontal nommé `myFrontEndPool`:

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

Output:

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

Notez comment nous avons utilisé hello `--public-ip-name` commutateur toopass Bonjour `myPublicIP` que nous avons créé précédemment. Affectation d’adresse IP publique hello équilibrage de charge adresse toohello vous permet de tooreach vos machines virtuelles entre hello Internet.

Nous allons maintenant créer notre deuxième pool d’adresses IP pour le trafic principal. Hello exemple suivant crée un pool principal nommé `myBackEndPool`:

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

Output:

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

Nous pouvons voir faire de notre programme d’équilibrage de charge en consultant avec `azure network lb show` et en examinant la sortie JSON hello :

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

Output:

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a>Créer des règles NAT d’équilibreur de charge
tout trafic tooget via notre programme d’équilibrage de charge, nous avons besoin de règles toocreate réseau adresse translation (NAT) qui spécifient les actions entrantes ou sortantes. Vous pouvez spécifier hello protocole toouse, puis mapper les ports de toointernal des ports externes comme vous le souhaitez. Pour notre environnement, nous allons créer des règles qui autorisent SSH via notre tooour d’équilibrage de charge machines virtuelles. Nous avons configuré le port TCP ports 4222 et 4223 toodirect tooTCP 22 sur nos machines virtuelles (ce qui nous créer ultérieurement). Hello exemple suivant crée une règle nommée `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22 :

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

Output:

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

Répétez la procédure de hello pour votre deuxième règle NAT pour SSH. Hello exemple suivant crée une règle nommée `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22 :

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

Nous allons également continuer et créer une règle NAT pour le port TCP 80 pour le trafic web, raccorder les règle hello tooour pools d’adresses IP. Si nous raccorder hello règle tooan de pool IP, au lieu de raccorder hello règle tooour machines virtuelles individuellement, nous pouvons ajouter ou supprimer des machines virtuelles à partir du pool d’adresses IP hello. équilibrage de charge Hello ajuste automatiquement le flux hello du trafic. Hello exemple suivant crée une règle nommée `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80 :

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

Output:

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a>Créer une sonde d’intégrité d’équilibreur de charge
Un contrôle d’intégrité de sonde périodiquement les vérifications sur hello machines virtuelles qui se trouvent derrière notre toomake d’équilibrage de charge que leur date d’exploitation et de répondre toorequests tel que défini. Si non, ils sont supprimés de tooensure opération que les utilisateurs ne sont pas en cours dirigé toothem. Vous pouvez définir des contrôles personnalisés pour la sonde d’intégrité hello, ainsi que les intervalles et les valeurs de délai d’attente. Pour plus d'informations sur les sondes d’intégrité, consultez [Sondes d’équilibreur de charge](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hello exemple suivant crée un TCP intégrité détectés nommée `myHealthProbe`:

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

Output:

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

Ici, nous avons spécifié un intervalle de 15 secondes pour nos contrôles d’intégrité. Nous pouvons ne pas conforme à un maximum de quatre sondes (une minute) avant de l’équilibrage de charge hello considère que cet hôte hello ne fonctionne plus.

## <a name="verify-hello-load-balancer"></a>Vérifiez l’équilibrage de charge hello
Configuration d’équilibrage de charge de hello est maintenant terminée. Voici les étapes hello que vous avez suivies :

1. Vous avez créé un équilibrage de charge.
2. Vous créé un pool IP frontal et affecté un tooit IP public.
3. Vous avez créé un pool d’adresses IP principal auquel les machines virtuelles peuvent se connecter.
4. Vous avez créé des règles NAT qui autorisent les machines virtuelles toohello SSH pour la gestion, ainsi que d’une règle qui autorise le port TCP 80 pour notre application web.
5. Vous avez ajouté un Bonjour de vérification d’intégrité sonde tooperiodically machines virtuelles. Cette sonde d’intégrité permet de s’assurer que les utilisateurs n’essaient pas tooaccess une machine virtuelle qui n’est plus fonctionne ni héberger un contenu.

Regardons maintenant à quoi ressemble votre équilibreur de charge :

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

Output:

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a>Créer une carte réseau toouse avec hello Linux VM
Cartes réseau est disponibles par programme, car vous pouvez appliquer des règles tootheir utilisation. Vous pouvez également avoir plusieurs cartes. Suivant de hello `azure network nic create` de commande, vous raccordez le pool d’adresses IP hello NIC toohello charge principal et l’associez à hello NAT règle toopermit SSH du trafic.

Remplacez hello `#####-###-###` sections avec votre propre ID d’abonnement Azure. Votre abonnement ID est indiqué dans la sortie de hello de `jq` lorsque vous examinez les ressources hello vous créez. Vous pouvez également afficher votre ID d’abonnement avec `azure account list`.

Hello exemple suivant crée une carte réseau nommée `myNic1`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

Output:

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

Vous pouvez afficher les détails de hello en examinant les ressources hello directement. Vous examinez les ressources hello à l’aide de hello `azure network nic show` commande :

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

Output:

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

Maintenant nous créons hello seconde carte réseau, raccorder à nouveau dans le pool d’adresses IP tooour back-end. Cette règle NAT hello deuxième autorise le trafic SSH. Hello exemple suivant crée une carte réseau nommée `myNic2`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a>Créer un groupe de sécurité réseau et les règles associées
Désormais nous créer un groupe de sécurité réseau, hello des règles de trafic entrant qui régissent l’accès toohello carte Un groupe de sécurité réseau peut être appliqué tooa carte réseau ou sous-réseau. Vous définissez un flux de hello toocontrol de règles de trafic vers et depuis vos machines virtuelles. Hello exemple suivant crée un groupe de sécurité réseau nommé `myNetworkSecurityGroup`:

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

Vous allez ajouter la règle de trafic entrant hello pour hello NSG tooallow connexions sur le port 22 (toosupport SSH) entrantes. Hello exemple suivant crée une règle nommée `myNetworkSecurityGroupRuleSSH` tooallow TCP sur le port 22 :

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

Maintenant vous allez ajouter la règle de trafic entrant hello pour hello NSG tooallow connexions sur le port 80 (trafic web de toosupport) entrantes. Hello exemple suivant crée une règle nommée `myNetworkSecurityGroupRuleHTTP` tooallow TCP sur le port 80 :

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> règle de trafic entrant Hello est un filtre pour les connexions réseau entrantes. Dans cet exemple, nous lions hello NSG toohello machines virtuelles carte réseau virtuelle, ce qui signifie que n’importe quel tooport demande 22 est passée via toohello carte réseau sur votre machine virtuelle. Cette règle de trafic entrant concerne une connexion réseau, et non à un point de terminaison, comme dans le cas de déploiements classiques. tooopen un port, vous devez laisser hello `--source-port-range` défini trop '\*' (valeur par défaut de hello) tooaccept les demandes d’entrantes **n’importe quel** port de demande. Ces ports sont généralement dynamiques.
>
>

## <a name="bind-toohello-nic"></a>Lier toohello carte réseau
Lier hello NSG toohello cartes réseau. Nous avons besoin de ses cartes réseau tooconnect à notre groupe de sécurité réseau. Exécutez les deux commandes, toohook des deux de ses cartes réseau :

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a>Créer un groupe à haute disponibilité
Les groupes à haute disponibilité aident à diffuser vos machines virtuelles sur des domaines d’erreur et des domaines de mise à niveau. Nous allons maintenant voir comment créer un groupe à haute disponibilité pour vos machines virtuelles. Hello exemple suivant crée un groupe à haute disponibilité nommée `myAvailabilitySet`:

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

Les domaines d’erreur désignent un groupe de machines virtuelles partageant une source d’alimentation et un commutateur réseau communs. Par défaut, hello virtuels qui sont configurés au sein de votre jeu de disponibilité sont séparées à travers des domaines d’erreur toothree. Hello est qu’un problème matériel dans un de ces domaines d’erreur n’affecte pas de chaque machine virtuelle qui exécute votre application. Azure distribue automatiquement les machines virtuelles entre les domaines d’erreur hello lorsque vous les placez dans un ensemble de disponibilité.

Indiquent les domaines de mise à niveau des ordinateurs virtuels et le matériel physique sous-jacent qui peut être redémarré à hello même temps. commande Hello dans lequel les domaines de mise à niveau sont redémarrés peut ne pas être séquentiel pendant les maintenances, mais la mise à niveau qu’un seul est redémarré à la fois. Cette fois encore, Azure distribue automatiquement vos machines virtuelles entre les domaines de mise à niveau lorsque vous les placez dans un site de disponibilité.

En savoir plus sur [gestion de la disponibilité de hello de machines virtuelles](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="create-hello-linux-vms"></a>Créer des machines virtuelles Linux hello
Vous avez créé des ressources de stockage et réseau hello machines virtuelles de toosupport accessible via Internet. Créons maintenant ces machines virtuelles et sécurisons-les avec une clé SSH sans mot de passe. Dans ce cas, nous allons toocreate une VM Ubuntu selon hello LTS plus récente. Nous recherchons les informations de cette image en utilisant `azure vm image list`, comme décrit dans [Recherche d’images de machine virtuelle Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Nous avons sélectionné une image à l’aide de commande hello `azure vm image list westeurope canonical | grep LTS`. Dans ce cas, nous utilisons `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`. Pour le dernier champ de hello, nous passons `latest` afin que dans les futures hello, nous obtenons toujours build la plus récente hello. (nous utilisons la chaîne hello est `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).

Cette étape est familier tooanyone qui a déjà créé un ssh rsa publique et privée paire de clés sur Linux ou Mac à l’aide de **ssh-keygen - t rsa -b 2048**. Si vous ne disposez pas de toutes les paires de clés de certificat dans votre répertoire `~/.ssh` , vous pouvez les créer ainsi :

* Automatiquement, à l’aide de hello `azure vm create --generate-ssh-keys` option.
* Manuellement, à l’aide [hello instructions toocreate les vous-même](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Vous pouvez également utiliser hello `--admin-password` méthode tooauthenticate vos connexions SSH après hello machine virtuelle est créée. Cette méthode est généralement moins sécurisée.

Nous créons hello machine virtuelle en rassemblant tous nos ressources et informations avec hello `azure vm create` commande :

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Output:

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

Vous pouvez connecter tooyour VM immédiatement à l’aide de vos clés SSH par défaut. Assurez-vous que vous spécifiez le port approprié de hello dans la mesure où nous transmettons via l’équilibrage de charge hello. (Pour notre premier ordinateur virtuel, nous configurons hello NAT règle tooforward port 4222 tooour machine virtuelle.)

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

Output:

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

Pour commencer, créez votre deuxième machine virtuelle Bonjour même manière :

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Et vous pouvez maintenant utiliser hello `azure vm show myResourceGroup myVM1` commande tooexamine à ce que vous avez créé. À ce stade, vous exécutez vos machines virtuelles Ubuntu derrière un équilibreur de charge dans Azure auquel vous pouvez uniquement vous connecter avec votre paire de clés SSH (car les mots de passe sont désactivés). Vous pouvez installer nginx ou httpd, déployer une application web et voir hello trafic circule tooboth d’équilibrage de charge hello de machines virtuelles de hello.

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

Output:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a>Environnement de hello d’exportation en tant que modèle
Maintenant que vous avez créé à cet environnement, que se passe-t-il si vous souhaitez toocreate à un environnement de développement supplémentaire avec hello mêmes paramètres, ou un environnement de production qui lui correspond ? Le Gestionnaire de ressources utilise des modèles JSON qui définissent tous les paramètres de hello pour votre environnement. Vous créez des environnements entiers en faisant référence à ce modèle JSON. Vous pouvez [créer manuellement des modèles JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exporter un modèle JSON environnement toocreate hello existant pour vous :

```azurecli
azure group export --name myResourceGroup
```

Cette commande crée hello `myResourceGroup.json` fichier dans votre répertoire de travail actuel. Lorsque vous créez un environnement à partir de ce modèle, vous êtes invité pour tous les noms de ressource hello, y compris les noms de hello pour l’équilibrage de charge hello, les interfaces réseau ou les machines virtuelles. Vous pouvez remplir ces noms dans votre fichier de modèle en ajoutant hello `-p` ou `--includeParameterDefaultValue` paramètre toohello `azure group export` commande qui a été indiqué précédemment. Modifier les noms de ressources JSON modèle toospecify hello, ou [créer un fichier parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) qui spécifie les noms de ressources hello.

toocreate un environnement à partir de votre modèle :

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

Vous souhaiterez peut-être tooread [plus sur la façon toodeploy à partir de modèles](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Découvrez comment tooincrementally les environnements de mise à jour, utilisez le fichier de paramètres hello et accéder aux modèles à partir d’un emplacement de stockage unique.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt toobegin utilisation de plusieurs composants réseau et les machines virtuelles. Vous pouvez utiliser cette toobuild d’environnement exemple votre application à l’aide de composants hello introduits ici.
