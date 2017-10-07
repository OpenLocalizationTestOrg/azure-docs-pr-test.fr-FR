---
title: aaaOpen ports tooa VM Linux avec Azure CLI 2.0 | Documents Microsoft
description: "Découvrez comment tooopen un port / créer un point de terminaison de tooyour Linux VM à l’aide de déploiement du Gestionnaire de ressources Azure hello modéliser et hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a>Ouvrir les ports et les points de terminaison tooa Linux VM avec hello CLI d’Azure
Vous ouvrez un port ou créer un point de terminaison, tooa machine virtuelle (VM) dans Azure en créant un filtre de réseau sur un sous-réseau ou une interface réseau de machine virtuelle. Vous placez ces filtres, qui contrôlent le trafic entrant et sortant, sur une ressource de toohello de groupe de sécurité réseau associé qui reçoit le trafic de hello. Nous allons utiliser un exemple courant de trafic web sur le port 80. Cet article vous explique comment tooopen un tooa port VM par hello Azure CLI 2.0. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).


## <a name="quick-commands"></a>Commandes rapides
Groupe de sécurité réseau toocreate et règles, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *myNetworkSecurityGroup* et *myVMnet*.

Créer le groupe de sécurité réseau hello avec [az réseau nsg créer](/cli/azure/network/nsg#create). Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup* Bonjour *eastus* emplacement :

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Ajouter une règle avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) tooallow HTTP tooyour webserver du trafic (ou l’ajuster pour votre propre scénario, tel que de la connectivité de base de données ou de l’accès SSH). Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRule* tooallow TCP du trafic sur le port 80 :

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

Associer hello groupe de sécurité réseau avec l’interface de réseau de votre machine virtuelle (NIC) [mise à jour de la carte réseau az réseau](/cli/azure/network/nic#update). exemple Hello associe une carte réseau nommée *myNic* avec hello groupe de sécurité réseau nommé *myNetworkSecurityGroup*:

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

Ou bien, vous pouvez associer votre groupe de sécurité réseau avec un sous-réseau de réseau virtuel avec [mise à jour de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#update) plutôt que de simplement toohello interface de réseau sur une seule machine virtuelle. exemple Hello associe un sous-réseau existant nommé *mySubnet* Bonjour *myVnet* réseau virtuel avec hello groupe de sécurité réseau nommé *myNetworkSecurityGroup*:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a>En savoir plus sur les groupes de sécurité réseau
Hello rapide commandes vous permettent de tooget haut et en cours d’exécution avec tooyour de flux de trafic VM. Groupes de sécurité réseau fournissent de nombreuses fonctionnalités et granularité pour contrôler les ressources tooyour accès. Découvrez plus d’informations sur la [création d’un groupe de sécurité réseau et de règles de liste de contrôle d’accès ici](tutorial-virtual-network.md#secure-network-traffic).

Pour les applications Web hautement disponibles, vous devez placer vos machines virtuelles derrière un équilibreur de charge Azure. équilibrage de charge Hello distribue tooVMs le trafic, avec un groupe de sécurité réseau qui fournit un filtrage du trafic. Pour plus d’informations, consultez [comment le solde tooload Linux virtual machines dans Azure toocreate une application hautement disponible](tutorial-load-balancer.md).

## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple, vous avez créé un trafic de tooallow HTTP règle simple. Vous trouverez des informations sur la création d’environnements plus Bonjour suivant des articles :

* [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Présentation du groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md)
