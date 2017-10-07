---
title: "aaaDeploy les machines virtuelles Linux sur un réseau existant avec le portail Azure | Documents Microsoft"
description: "Déployer un VM Linux dans un réseau virtuel Azure existant à l’aide du portail de hello."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a>Comment toodeploy une machine virtuelle de Linux dans un réseau virtuel Azure existant avec hello portail Azure

Cet article vous explique comment toodeploy un ordinateur virtuel (VM) dans un réseau virtuel (VNet). Les ressources Azure telles que les réseaux virtuels et les groupes de sécurité réseau doivent être des ressources statiques et durables qui sont rarement déployées. Une fois qu’un réseau virtuel a été déployé, il peut être réutilisé par redéploiements constantes sans n’importe quelle infrastructure de toohello répercussions négatives. Vous réfléchissez à un réseau virtuel comme étant une traditionnelle commutateur de réseau de matériel – vous n’avez pas tooconfigure basculer d’un nouveau matériel à chaque déploiement.  

Avec un réseau virtuel configuré correctement, vous pouvez poursuivre toodeploy nouveaux serveurs dans ce réseau virtuel apportant peu, le cas échéant, de modifications nécessaires pendant toute la durée hello Hello réseau virtuel.

## <a name="create-hello-resource-group"></a>Créer le groupe de ressources hello

Commencez par créer un tooorganize de groupe de ressources tout ce que vous créez dans cette procédure pas à pas. Pour plus d’informations sur les groupes de ressources Azure, consultez la [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a>Créer hello réseau virtuel

Ensuite, générez un Bonjour toolaunch de réseau virtuel pour les machines virtuelles dans. Hello réseau virtuel contient un sous-réseau et est associé au groupe de sécurité réseau hello à ce sous-réseau dans une étape ultérieure.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a>Ajouter un sous-réseau toohello de carte réseau virtuelle

Les cartes réseau virtuelles (cartes réseau) sont importantes que vous pouvez vous connecter les machines virtuelles de toodifferent. Cette approche conserve hello VNic comme une ressource statique hello machines virtuelles peut être temporaire. Créer une carte réseau virtuelle et l’associer à sous-réseau hello créé à l’étape précédente de hello.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a>Créer un groupe de sécurité réseau hello

Groupes de sécurité réseau Azure sont pare-feu tooa équivalente à la couche réseau hello. Pour plus d’informations sur les groupes de sécurité réseau Azure, consultez [Présentation du groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md).

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Ajouter une règle d’autorisation SSH entrante

Hello machine virtuelle a besoin d’accéder à partir de hello internet, pour une règle autorisant le port entrant 22 trafic toobe transmises via le réseau de hello tooport 22 sur hello machine virtuelle est créée.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a>Associer hello NSG sous-réseau de hello

Avec hello réseau virtuel et un sous-réseau hello créé, associez un groupe de sécurité réseau hello sous-réseau de hello. Les groupes de sécurité réseau peuvent être associés à un sous-réseau entier ou à une carte réseau virtuelle individuelle. Avec le pare-feu hello filtrage du trafic au niveau du sous-réseau hello, toutes les cartes réseau et hello machines virtuelles au sein du sous-réseau de hello sont protégés par le groupe de sécurité réseau hello. Hello autre approche est hello groupe de sécurité réseau sont associées à une seule carte réseau virtuelle et la protection qu’une seule machine virtuelle.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Déployer hello VM dans hello réseau virtuel et le groupe de sécurité réseau

À l’aide de hello portail Azure, hello Linux VM est déployé toohello existante du groupe de ressources Azure, du réseau virtuel, sous-réseau et une carte réseau virtuelle.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

À l’aide des ressources existantes hello toochoose portail, vous indiquez à toodeploy Azure hello machine virtuelle à l’intérieur du réseau existant de hello. Lorsqu’un réseau virtuel et un sous-réseau ont été déployés, ils peuvent être conservés en tant que ressources statiques ou permanentes à l’intérieur de votre région Azure.  

## <a name="next-steps"></a>Étapes suivantes

* [Utilisez un toocreate de modèle Azure Resource Manager un déploiement spécifique](../windows/cli-deploy-templates.md)
* [Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement](create-cli-complete.md)
* [Création d’une machine virtuelle Linux sur Azure à l’aide de modèles](create-ssh-secured-vm-from-template.md)
