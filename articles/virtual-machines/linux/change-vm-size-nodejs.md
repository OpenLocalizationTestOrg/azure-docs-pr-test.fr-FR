---
title: aaaHow tooresize un VM Linux avec hello Azure CLI 1.0 | Documents Microsoft
description: "Comment tooscale des ou mise à l’échelle vers le bas d’une machine virtuelle Linux, en modifiant hello taille de machine virtuelle."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a>Redimensionner une machine virtuelle Linux avec Azure CLI 1.0

## <a name="overview"></a>Vue d'ensemble

Une fois que vous configurez un ordinateur virtuel (VM), vous pouvez augmenter ou diminuer la hello machine virtuelle en modifiant hello [taille de machine virtuelle][vm-sizes]. Dans certains cas, vous devez libérer hello VM tout d’abord. Cela peut se produire si la nouvelle taille de hello n’est pas disponible sur le cluster de matériel hello qui héberge hello machine virtuelle.

Cet article explique comment tooresize un VM Linux à l’aide de hello [CLI d’Azure][azure-cli].

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#resize-a-linux-vm) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello


## <a name="resize-a-linux-vm"></a>Redimensionner une machine virtuelle Linux
tooresize une machine virtuelle, effectuez hello comme suit.

1. Exécutez hello suivant commande CLI. Cette commande répertorie les tailles de machine virtuelle hello qui sont disponibles sur le cluster de matériel hello où hello ordinateur virtuel est hébergé.
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. Si hello souhaité est indiquée, exécutez hello suivant commande tooresize hello machine virtuelle.
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    Hello machine virtuelle va redémarrer pendant ce processus. Après le redémarrage de hello, votre système d’exploitation existant et les disques de données seront remappés. Quoi que ce soit sur le disque temporaire de hello seront perdu.
   
    Hello d’utilisation `--enable-boot-diagnostics` option active [diagnostics de démarrage][boot-diagnostics], toolog tout toostartup connexes d’erreurs.
3. Dans le cas contraire, si hello souhaité de taille n’est pas répertoriée, exécutez hello suivant les commandes toodeallocate hello VM, redimensionner et redémarrez hello machine virtuelle.
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > Hello désallocation de machine virtuelle libère aussi toutes les adresses IP dynamiques affectées toohello machine virtuelle. Hello du système d’exploitation et des disques de données ne sont pas affectées.
   > 
   > 

## <a name="next-steps"></a>Étapes suivantes
Pour une évolutivité supplémentaire, exécutez plusieurs instances de machine virtuelle et augmentez leur taille. Pour plus d’informations, consultez [Mise à l’échelle automatique des machines Linux dans un groupe de machines virtuelles à échelle identique][scale-set]. 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
