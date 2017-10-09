---
title: "aaaUse la résolution par hello Azure CLI 2.0 de noms DNS internes pour la machine virtuelle | Documents Microsoft"
description: "Comment les réseaux virtuels toocreate cartes d’interface et utiliser DNS interne pour la résolution de nom de machine virtuelle sur Azure avec hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a>Création de cartes d’interface réseau virtuelle et d’utilisation des DNS internes pour la résolution des noms de machine virtuelle sur Azure
Cet article explique comment tooset statique les noms DNS internes pour les machines virtuelles Linux à l’aide de virtual network cartes d’interface (cartes réseau) et les noms d’étiquette DNS avec hello Azure CLI 2.0. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Les noms DNS statiques sont utilisés pour les services d’infrastructure permanents comme un serveur de builds Jenkins, qui est utilisé pour ce document, ou un serveur Git.

spécifications de Hello sont :

* [un compte Azure](https://azure.microsoft.com/pricing/free-trial/)
* [des fichiers de clés SSH publiques et privées](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Commandes rapides
Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant la section Détails des commandes hello nécessaires. Plus d’informations et le contexte de chaque étape se trouvent dans le reste de hello du document de hello, [Démarrer ici](#detailed-walkthrough). tooperform ces étapes, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Conditions préalables : groupe de ressources, réseau virtuel et sous-réseau, groupe de sécurité réseau avec SSH entrant.

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a>Création d’une carte réseau virtuelle avec un nom DNS interne statique
Créer une carte réseau virtuelle de hello avec [créer des cartes réseau du réseau az](/cli/azure/network/nic#create). Hello `--internal-dns-name` CLI est pour le nom DNS paramètre hello, qui fournit un nom DNS statique hello pour une carte d’interface réseau virtuelle hello (vNic). Hello exemple suivant crée une carte réseau virtuelle nommée `myNic`, connecte toohello `myVnet` réseau virtuel et crée un enregistrement de nom DNS interne appelé `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a>Déployer un ordinateur virtuel et vous connecter à une carte réseau virtuelle hello
Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). Hello `--nics` indicateur connecte hello vNic toohello VM pendant hello déploiement tooAzure. Hello exemple suivant crée un ordinateur virtuel nommé `myVM` avec disques gérés d’Azure et hello attache une carte réseau virtuelle nommée `myNic` de hello précédant l’étape :

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas

Une intégration complète continue et un déploiement continu (CiCd) une infrastructure sur Azure requiert certains serveurs de toobe serveurs statique ou à long terme. Il est recommandé que les ressources Azure telles que hello des réseaux virtuels et des groupes de sécurité réseau sont statiques et longue durée de vie ressources qui sont rarement déployées. Une fois qu’un réseau virtuel a été déployé, il peut être réutilisé par nouveaux déploiements sans n’importe quelle infrastructure de toohello répercussions négatives. Vous pouvez ajouter ultérieurement un serveur de référentiel Git ou un serveur automation de Jenkins remet CiCd toothis de réseau virtuel pour vos environnements de développement ou de test.  

Les noms DNS internes ne peuvent être résolus qu’à l’intérieur d’un réseau virtuel Azure. Étant donné que les noms DNS hello sont internes, ils ne sont pas toohello pouvant être résolu en dehors d’internet, en fournissant l’infrastructure toohello de sécurité supplémentaire.

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Exemples de noms de paramètre : `myResourceGroup`, `myNic` et `myVM`.

## <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello
Commencez par créer le groupe de ressources hello avec [az groupe créer](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westus` emplacement :

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a>Créer le réseau virtuel de hello

étape suivante de Hello est toobuild un toolaunch de réseau virtuel hello des machines virtuelles dans. réseau virtuel de Hello contient un sous-réseau pour cette procédure pas à pas. Pour plus d’informations sur les réseaux virtuels Azure, consultez [créer un réseau virtuel à l’aide de hello CLI d’Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Créer le réseau virtuel hello [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create). Hello exemple suivant crée un réseau virtuel nommé `myVnet` et sous-réseau nommé `mySubnet`:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a>Créer un groupe de sécurité réseau de hello
Les groupes de sécurité réseau Azure sont pare-feu tooa équivalente à la couche réseau hello. Pour plus d’informations sur les groupes de sécurité réseau, consultez [comment les groupes de sécurité réseau toocreate dans hello CLI d’Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Créer le groupe de sécurité réseau hello avec [az réseau nsg créer](/cli/azure/network/nsg#create). Hello exemple suivant crée un groupe de sécurité réseau nommé `myNetworkSecurityGroup`:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a>Ajouter une règle de trafic entrant de tooallow SSH
Ajouter une règle de trafic entrant pour le groupe de sécurité réseau hello avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create). Hello exemple suivant crée une règle nommée `myRuleAllowSSH`:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a>Associez hello sous-réseau hello groupe de sécurité réseau
sous-réseau hello tooassociate hello groupe de sécurité réseau, utilisez [mise à jour de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#update). Hello exemple suivant associe un nom de sous-réseau hello `mySubnet` avec hello groupe de sécurité réseau nommé `myNetworkSecurityGroup`:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a>Créer une carte d’interface réseau virtuelle hello et des noms DNS statiques
Azure est très souple, mais toouse les noms DNS pour la résolution de nom de machine virtuelle, vous devez toocreate virtuel cartes d’interface réseau (cartes réseau) qui incluent un nom DNS. cartes réseau est importantes que vous puissiez les réutiliser en les connectant toodifferent VMs hello infrastructure du cycle de vie. Cette approche conserve une carte réseau virtuelle hello comme une ressource statique hello machines virtuelles peut être temporaire. À l’aide de DNS étiquetage sur une carte réseau virtuelle hello, nous sommes tooenable en mesure de résolution de nom simple à partir d’autres ordinateurs virtuels hello réseau virtuel. Noms pouvant être résolus grâce à autre serveur automation de machines virtuelles tooaccess hello par nom DNS hello `Jenkins` ou serveur hello Git `gitrepo`.  

Créer une carte réseau virtuelle de hello avec [créer des cartes réseau du réseau az](/cli/azure/network/nic#create). Hello exemple suivant crée une carte réseau virtuelle nommée `myNic`, connecte toohello `myVnet` réseau virtuel nommé `myVnet`et crée un enregistrement de nom DNS interne appelé `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Déployer hello VM dans l’infrastructure de réseau virtuel hello
Nous disposons désormais d’un réseau virtuel et un sous-réseau, un groupe de sécurité réseau agissant comme un tooprotect pare-feu notre sous-réseau en bloquant tout le trafic entrant, à l’exception de port 22 pour SSH et une carte réseau virtuelle. Vous pouvez maintenant déployer une machine virtuelle au sein de cette infrastructure réseau existante.

Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé `myVM` avec disques gérés d’Azure et hello attache une carte réseau virtuelle nommée `myNic` de hello précédant l’étape :

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

À l’aide de hello CLI indicateurs toocall les ressources existantes, nous indiquons hello toodeploy Azure VM à l’intérieur du réseau existant de hello. tooreiterate, une fois qu’un réseau virtuel et le sous-réseau ont été déployés, ils peuvent rester statiques ou permanentes des ressources à l’intérieur de votre région Azure.  

## <a name="next-steps"></a>Étapes suivantes
* [Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Création d’une machine virtuelle Linux sur Azure à l’aide de modèles](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
