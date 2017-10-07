---
title: "aaaUsing la résolution sur Azure de noms DNS internes pour la machine virtuelle | Documents Microsoft"
description: "Utilisation de DNS interne pour la résolution de noms de machines virtuelles dans Azure."
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
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a>Utilisation de DNS interne pour la résolution de noms de machines virtuelles dans Azure

Cet article explique comment tooset DNS interne statique des noms pour les machines virtuelles Linux à l’aide de cartes d’interface réseau virtuelle (VNic) et les noms DNS en une partie. Les noms DNS statiques sont utilisés pour les services d’infrastructure permanents comme un serveur de builds Jenkins, qui est utilisé pour ce document, ou un serveur Git.

spécifications de Hello sont :

* [un compte Azure](https://azure.microsoft.com/pricing/free-trial/)
* [des fichiers de clés SSH publiques et privées](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello


## <a name="quick-commands"></a>Commandes rapides

Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant la section Détails des commandes hello nécessaires. Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#detailed-walkthrough).  

Configuration requise : groupe de ressources, réseau virtuel, groupe de sécurité réseau avec SSH entrant, sous-réseau.

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a>Créer une carte réseau virtuelle avec un nom DNS interne statique

Hello `-r` cli indicateur est pour le nom DNS paramètre hello, qui fournit un nom DNS statique hello pour hello une carte réseau virtuelle.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a>Déployer la machine virtuelle de hello en hello réseau virtuel, le groupe de sécurité réseau et, à connecter hello VNic

Hello `-N` se connecte hello VNic toohello nouvelle machine virtuelle pendant hello déploiement tooAzure.

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas

Une intégration complète continue et un déploiement continu (CiCd) une infrastructure sur Azure requiert certains serveurs de toobe serveurs statique ou à long terme.  Il est recommandé que les ressources Azure telles que hello de réseaux virtuels (réseaux virtuels) et les groupes de sécurité réseau (NSG), doit être statiques et longue durée de vie ressources qui sont rarement déployées.  Une fois qu’un réseau virtuel a été déployé, il peut être réutilisé par nouveaux déploiements sans n’importe quelle infrastructure de toohello répercussions négatives.  Ajout de réseau statique de toothis un Git serveur de référentiel et un serveur automation de Jenkins remet CiCd tooyour les environnements de développement ou de test.  

Les noms DNS internes ne peuvent être résolus qu’à l’intérieur d’un réseau virtuel Azure.  Étant donné que les noms DNS hello sont internes, ils ne sont pas toohello pouvant être résolu en dehors d’internet, en fournissant l’infrastructure toohello de sécurité supplémentaire.

_Remplacez les exemples par votre propre attribution de noms._

## <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello

Un groupe de ressources est tooorganize nécessaire tout ce dont nous créons cette procédure pas à pas.  Pour plus d’informations sur les groupes de ressources Azure, consultez l’article [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a>Créer hello réseau virtuel

première étape de Hello est toobuild un toolaunch de réseau virtuel hello des machines virtuelles dans.  Hello réseau virtuel contient un sous-réseau pour cette procédure pas à pas.  Pour plus d’informations sur des réseaux virtuels Azure, consultez [créer un réseau virtuel à l’aide de hello CLI d’Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a>Créer hello NSG

Hello sous-réseau repose derrière un groupe de sécurité réseau existant afin de nous hello NSG hello sous-réseau avant de le générer.  Groupes de sécurité réseau Azure sont pare-feu tooa équivalente à la couche réseau hello.  Pour plus d’informations sur les groupes de sécurité réseau Azure, consultez [comment les groupes de sécurité réseau toocreate dans hello CLI d’Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Ajouter une règle d’autorisation SSH entrante

Hello Linux VM a besoin d’accéder à partir de hello internet pour une règle autorisant le port entrant 22 trafic toobe transmises via le réseau de hello tooport 22 sur hello Linux VM est nécessaire.

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Ajouter un sous-réseau de toohello réseau virtuel

Machines virtuelles au sein de hello réseau virtuel doivent se trouver dans un sous-réseau.  Chaque réseau virtuel peut présenter plusieurs sous-réseaux.  Créer des sous-réseaux de hello et associez hello sous-réseau hello NSG tooadd un sous-réseau toohello de pare-feu.

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

Hello sous-réseau est désormais ajouté à l’intérieur du réseau virtuel de hello et associé hello NSG et règle de groupe de sécurité réseau hello.

## <a name="creating-static-dns-names"></a>Création de noms DNS statiques

Azure est très souple, mais toouse les noms DNS pour la résolution de noms d’ordinateurs virtuels, vous devez toocreate en tant que virtuel cartes (cartes réseau) à l’aide de DNS étiquetage de réseau.  Cartes réseau est importantes que vous puissiez les réutiliser en les connectant toodifferent les machines virtuelles, ce qui maintient hello VNic comme une ressource statique hello machines virtuelles peut être temporaire.  À l’aide de DNS étiquetage sur une carte réseau virtuelle de hello, nous sommes tooenable en mesure de résolution de nom simple à partir d’autres ordinateurs virtuels hello réseau virtuel.  Noms pouvant être résolus grâce à autre serveur automation de machines virtuelles tooaccess hello par nom DNS hello `Jenkins` ou serveur hello Git `gitrepo`.  Créer une carte réseau virtuelle et l’associer à hello que sous-réseau créé à l’étape précédente de hello.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Déployer hello VM dans hello réseau virtuel et le groupe de sécurité réseau

Nous disposons désormais d’un réseau virtuel, un sous-réseau à l’intérieur de ce réseau virtuel et un groupe de sécurité réseau agissant comme un tooprotect pare-feu notre sous-réseau en bloquant tout le trafic entrant, à l’exception de port 22 pour SSH.  Hello machine virtuelle peut désormais être déployé à l’intérieur de cette infrastructure réseau existante.

À l’aide de hello CLI d’Azure et hello `azure vm create` hello Linux VM est déployé toohello existante du groupe de ressources Azure, du réseau virtuel, sous-réseau et une carte réseau virtuelle de la commande.  Pour plus d’informations sur l’utilisation de hello CLI toodeploy une machine virtuelle complète, consultez [créer un environnement complet de Linux à l’aide de hello CLI d’Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

À l’aide de hello CLI indicateurs toocall les ressources existantes, nous indiquons hello toodeploy Azure VM à l’intérieur du réseau existant de hello.  tooreiterate, une fois qu’un réseau virtuel et le sous-réseau ont été déployés, ils peuvent rester statiques ou permanentes des ressources à l’intérieur de votre région Azure.  

## <a name="next-steps"></a>Étapes suivantes
* [Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Création d’une machine virtuelle Linux sur Azure à l’aide de modèles](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
