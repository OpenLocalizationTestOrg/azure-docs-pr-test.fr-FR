---
title: aaaOpen ports tooa VM Linux avec Azure CLI 1.0 | Documents Microsoft
description: "Découvrez comment tooopen un port / créer un point de terminaison de tooyour Linux VM à l’aide de déploiement du Gestionnaire de ressources Azure hello modéliser et hello Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>Ouvrir les ports et les points de terminaison tooa Linux VM dans Azure à l’aide hello Azure CLI 1.0
Vous ouvrez un port ou créer un point de terminaison, tooa machine virtuelle (VM) dans Azure en créant un filtre de réseau sur un sous-réseau ou une interface réseau de machine virtuelle. Vous placez ces filtres, qui contrôlent le trafic entrant et sortant, sur une ressource de toohello de groupe de sécurité réseau associé qui reçoit le trafic de hello. Nous allons utiliser un exemple courant de trafic web sur le port 80. Cet article vous montre comment une machine virtuelle tooa port à l’aide de tooopen hello Azure CLI 1.0.


## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](nsg-quickstart.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello


## <a name="quick-commands"></a>Commandes rapides
toocreate un groupe de sécurité réseau et des règles [hello Azure CLI 1.0](../../cli-install-nodejs.md) installé et utilise le mode Gestionnaire de ressources :

```azurecli
azure config mode arm
```

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les exemples de noms de paramètre comprennent *myResourceGroup*, *myNetworkSecurityGroup* et *myVMnet*.

Créez votre groupe de sécurité réseau en entrant votre nom et votre emplacement en conséquence. Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup* Bonjour *eastus* emplacement :

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Ajouter un serveur Web de règle tooallow HTTP trafic tooyour (ou ajuster pour votre propre scénario, tel que de la connectivité de base de données ou de l’accès SSH). Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRule* tooallow TCP du trafic sur le port 80 :

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

Hello groupe de sécurité réseau associé disposant d’interface réseau (NIC) de votre machine virtuelle. exemple Hello associe une carte réseau nommée *myNic* avec hello groupe de sécurité réseau nommé *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

Vous pouvez également associer votre groupe de sécurité réseau avec un sous-réseau de réseau virtuel plutôt que simplement toohello interface de réseau sur une seule machine virtuelle. exemple Hello associe un sous-réseau existant nommé *mySubnet* Bonjour *myVnet* réseau virtuel avec hello groupe de sécurité réseau nommé *myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>En savoir plus sur les groupes de sécurité réseau
Hello rapide commandes vous permettent de tooget haut et en cours d’exécution avec tooyour de flux de trafic VM. Groupes de sécurité réseau fournissent de nombreuses fonctionnalités et granularité pour contrôler les ressources tooyour accès. Découvrez plus d’informations sur la [création d’un groupe de sécurité réseau et de règles de liste de contrôle d’accès ici](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).

Vous pouvez définir des groupes de sécurité réseau et des règles de liste de contrôle d’accès dans le cadre de modèles Azure Resource Manager. En savoir plus sur la [création de groupes de sécurité réseau avec des modèles](../../virtual-network/virtual-networks-create-nsg-arm-template.md).

Si vous avez besoin de réacheminement de port de toouse toomap un unique externe tooan port interne sur votre machine virtuelle, utilisez un équilibrage de charge et les règles de traduction d’adresses réseau (NAT). Par exemple, vous pouvez tooexpose le port TCP 8080 en externe et souhaitez le trafic est dirigé tooTCP port 80 sur un ordinateur virtuel. En savoir plus sur [la création d'un équilibreur de charge accessible sur Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple, vous avez créé un trafic de tooallow HTTP règle simple. Vous trouverez des informations sur la création d’environnements plus Bonjour suivant des articles :

* [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Présentation du groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md)
* [Présentation d’Azure Resource Manager](../../load-balancer/load-balancer-arm.md)

