---
title: aaaHow tooresize un VM Linux avec hello Azure CLI 2.0 | Documents Microsoft
description: "Comment tooscale des ou mise à l’échelle vers le bas d’une machine virtuelle Linux, en modifiant hello taille de machine virtuelle."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a>Redimensionner une machine virtuelle Linux avec CLI 2.0

Une fois que vous configurez un ordinateur virtuel (VM), vous pouvez augmenter ou diminuer la hello machine virtuelle en modifiant hello [taille de machine virtuelle][vm-sizes]. Dans certains cas, vous devez libérer hello VM tout d’abord. Vous devez toodeallocate hello machine virtuelle si vous le souhaitez hello taille n’est pas disponible sur le cluster de matériel hello qui héberge hello machine virtuelle. Cet article décrit en détail comment tooresize un VM Linux avec hello Azure CLI 2.0. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="resize-a-vm"></a>Redimensionner une machine virtuelle
tooresize une machine virtuelle, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

1. Afficher la liste hello des ordinateurs virtuels disponibles sur le cluster de matériel hello où hello machine virtuelle est hébergée avec des tailles de [az vm-vm-resize-options de la liste](/cli/azure/vm#list-vm-resize-options). Hello exemple suivant répertorie les tailles de machine virtuelle pour hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello `myResourceGroup` région :
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. Si hello souhaité de taille de machine virtuelle est répertoriée, redimensionner hello machine virtuelle avec [az vm redimensionner](/cli/azure/vm#resize). Hello suivant redimensionne de l’exemple hello ordinateur virtuel nommé `myVM` toohello `Standard_DS3_v2` taille :
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    Hello machine virtuelle redémarre pendant ce processus. Après le redémarrage de hello, votre système d’exploitation existant et les disques de données sont remappés. Quoi que ce soit sur le disque temporaire de hello est perdu.

3. Si hello souhaité de taille de machine virtuelle n’est pas répertorié, vous devez toofirst désallouer hello machine virtuelle avec [az vm désallouer](/cli/azure/vm#deallocate). Ce processus autorise hello VM toothen être redimensionné tooany taille disponible qui prend en charge de la région de hello, puis démarré. Hello suit désallouer, redimensionner et puis démarrez hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > Hello désallocation de machine virtuelle libère aussi toutes les adresses IP dynamiques affectées toohello machine virtuelle. Hello du système d’exploitation et des disques de données ne sont pas affectées.

## <a name="next-steps"></a>Étapes suivantes
Pour une évolutivité supplémentaire, exécutez plusieurs instances de machine virtuelle et augmentez leur taille. Pour plus d’informations, consultez [Mise à l’échelle automatique des machines Linux dans un groupe de machines virtuelles à échelle identique][scale-set]. 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
