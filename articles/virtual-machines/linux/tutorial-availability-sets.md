---
title: "aaaAvailability définit le didacticiel pour les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Découvrez hello haute disponibilité pour les machines virtuelles Linux dans Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Comment à haute disponibilité de toouse


Dans ce didacticiel, vous allez apprendre comment la disponibilité de hello tooincrease et la fiabilité de vos solutions d’ordinateur virtuel sur Azure à l’aide d’une fonctionnalité appelée haute disponibilité. Haute disponibilité vous assurer que hello machines virtuelles que vous déployez sur Azure sont réparties entre plusieurs clusters matérielles isolées. Cela garantit que si une défaillance matérielle ou logicielle dans Azure se produit, qu’un ensemble sous-chemin de vos machines virtuelles est concerné et que votre solution globale resteront disponibles et opérationnels du point de vue hello de vos clients à l’utiliser.

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer un groupe à haute disponibilité
> * Créer une machine virtuelle dans un groupe à haute disponibilité
> * Vérifier les tailles de machines virtuelles disponibles


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Vue d’ensemble des groupes à haute disponibilité

Un ensemble de disponibilité d’est une fonctionnalité de regroupement logique que vous pouvez utiliser dans Azure tooensure que les ressources de machine virtuelle de hello que vous placez qu’il contient sont isolées des autres lorsqu’ils sont déployés dans un centre de données Azure. Azure garantit que machines virtuelles que vous placez dans un ensemble de disponibilité s’exécuter sur plusieurs serveurs physiques hello, le calcul des racks, les unités de stockage et les commutateurs de réseau. Cela garantit que dans le cas de hello d’un problème matériel ou logiciel d’Azure, uniquement un sous-ensemble de vos machines virtuelles est affecté, et continuer à et continuer toobe disponible tooyour clients de votre application globale. À l’aide de la haute disponibilité est une fonctionnalité essentielle de tooleverage toobuild les solutions de cloud fiable.

Prenons l’exemple d’une solution basée sur une machine virtuelle classique dans laquelle vous disposez de 4 serveurs web frontaux et utilisez 2 machines virtuelles principales hébergeant une base de données. Avec Azure, vous souhaiteriez toodefine deux groupes à haute disponibilité avant de déployer vos machines virtuelles : une disponibilité définie pour le niveau de « web » hello et une haute disponibilité pour le niveau de « base de données » hello. Lorsque vous créez une nouvelle machine virtuelle que vous pouvez ensuite spécifier hello groupe à haute disponibilité comme une machine virtuelle de paramètre toohello az Créer commande et Azure automatiquement garantit que machines virtuelles que vous créez au sein de hello disponible hello ensemble sont isolés sur plusieurs ressources de matériel physique. Cela signifie que si le matériel physique hello que votre serveur Web ou les machines virtuelles de serveur de base de données est en cours d’exécution sur a un problème, vous savez que hello autres instances de votre serveur Web et les machines virtuelles de base de données reste en cours d’exécution correctement, car ils sont sur un matériel différent.

Vous devez toujours utiliser des ensembles de disponibilité lorsque vous souhaitez toodeploy basée sur des ordinateurs virtuels des solutions fiables dans Azure.


## <a name="create-an-availability-set"></a>Créer un groupe à haute disponibilité

Vous pouvez créer un groupe à haute disponibilité à l’aide de la commande [az vm availability-set create](/cli/azure/vm/availability-set#create). Dans cet exemple, nous avons défini à la fois nombre hello domaines de mise à jour et d’erreur à *2* pour hello groupe à haute disponibilité nommée *myAvailabilitySet* Bonjour *myResourceGroupAvailability*groupe de ressources.

Créez un groupe de ressources.

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

Haute disponibilité permettre de tooisolate ressources entre domaines d’erreur « » et « domaines de mise à jour ». Un **domaine d’erreur** représente une collection isolée comportant un serveur, un réseau et des ressources de stockage. Bonjour précédent exemple, nous indiquent que nous souhaitons que notre disponibilité définie toobe distribué sur au moins deux domaines d’erreur lors de notre machines virtuelles sont déployées. Nous indiquons également que nous souhaitons que notre groupe à haute disponibilité soit réparti sur deux **domaines de mise à jour**.  Deux domaines de mise à jour respectent lorsque Azure effectue des mises à jour logicielles nos ressources d’ordinateur virtuel isolés, ce qui empêche tous les logiciels hello en cours d’exécution en dessous de la machine virtuelle à partir de la mise à jour à hello même temps.

## <a name="configure-virtual-network"></a>Configurer un réseau virtuel
Avant de déployer des machines virtuelles et tester votre programme d’équilibrage, créer hello prenant en charge des ressources du réseau virtuel. Pour plus d’informations sur les réseaux virtuels, consultez hello [gérer les réseaux virtuels Azure](tutorial-virtual-network.md) didacticiel.

### <a name="create-network-resources"></a>Créer des ressources réseau
Créez un réseau virtuel avec la commande [az network vnet create](/cli/azure/network/vnet#create). Hello exemple suivant crée un réseau virtuel nommé *myVnet* avec un sous-réseau nommé *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
Les cartes d’interface réseau virtuelles sont créées avec la commande [az network nic create](/cli/azure/network/nic#create). Hello exemple suivant crée trois cartes réseau virtuelles. (Une carte réseau virtuelle pour chaque ordinateur virtuel que vous créez pour votre application Bonjour suivant les étapes). Vous pouvez créer des cartes réseau virtuelles supplémentaires et des machines virtuelles à tout moment et ajoutez-les à équilibrage de charge toohello :

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a>Créer des machines virtuelles dans un groupe à haute disponibilité

Machines virtuelles doivent être créées dans hello disponibilité ensemble toomake qu’ils sont correctement distribués sur les matériels hello. Vous ne pouvez pas ajouter un groupe de machines virtuelles tooan disponibilité définie après sa création. 

Lorsque vous créez une machine virtuelle à l’aide de [az vm créer](/cli/azure/vm#create) vous spécifiez hello haute disponibilité via hello `--availability-set` toospecify hello nom hello à haute disponibilité.

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

Nous avons à présent deux machines virtuelles à l’intérieur du groupe à haute disponibilité que nous venons de créer. Parce qu’elles sont hello même groupe à haute disponibilité, Azure garantit que machines virtuelles hello et toutes leurs ressources (y compris les disques de données) sont distribués sur un matériel physique isolé. Cette distribution contribue à assurer une disponibilité sensiblement plus importante de notre solution globale de machine virtuelle.

Une chose que vous pouvez rencontrer lorsque vous ajoutez des machines virtuelles est qu’une taille de machine virtuelle particulière n’est plus disponible toouse au sein de votre jeu de disponibilité. Ce problème peut se produire si il n’est plus suffisamment tooadd capacité il tout en préservant la haute disponibilité de hello isolation règles hello impose. Vous pouvez vérifier toosee les tailles de machine virtuelle sont toouse disponible au sein d’un groupe de disponibilité à l’aide de hello `--availability-set list-sizes` paramètre.

## <a name="check-for-available-vm-sizes"></a>Vérifier les tailles de machines virtuelles disponibles 

Vous pouvez ajouter plusieurs machines virtuelles toohello haute disponibilité plus tard, mais vous devez tooknow les tailles de machine virtuelle sont disponibles sur le matériel de hello. Utilisez [az vm disponibilité liste-taille](/cli/azure/availability-set#list-sizes) toolist toutes les tailles disponibles hello sur du matériel de hello du cluster pour hello à haute disponibilité.

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Créer un groupe à haute disponibilité
> * Créer une machine virtuelle dans un groupe à haute disponibilité
> * Vérifier les tailles de machines virtuelles disponibles

Avance toohello toolearn de didacticiel suivant sur les machines virtuelles identiques.

> [!div class="nextstepaction"]
> [Créer un groupe de machines virtuelles identiques](tutorial-create-vmss.md)

