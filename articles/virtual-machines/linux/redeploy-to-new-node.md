---
title: aaaRedeploy ordinateurs virtuels Linux dans Azure | Documents Microsoft
description: "Comment virtuels tooredeploy Linux dans la connexion SSH toomitigate Azure émet."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a>Redéployer toonew de machine virtuelle Linux nœud Azure
Si vous rencontrez des difficultés de résolution des problèmes de SSH ou accéder à application tooa Linux virtual machine (VM) dans Azure, redéploiement hello machine virtuelle peut aider. Lorsque vous redéployez un ordinateur virtuel, il déplace hello VM tooa nouveau nœud au sein de hello infrastructure Azure et donne sur toute sa puissance. Toutes les options de configuration et les ressources associées sont conservées. Cet article vous montre comment tooredeploy une machine virtuelle à l’aide d’Azure CLI ou hello portail Azure.

> [!NOTE]
> Une fois que vous redéployez un ordinateur virtuel, disque temporaire de hello est perdu et les adresses IP dynamiques associés à interface réseau virtuelle sont mis à jour. 

Vous pouvez redéployer une machine virtuelle à l’aide d’une des options suivantes de hello. Vous devez uniquement toochoose une option tooredeploy votre machine virtuelle :

- [Azure CLI 2.0](#azure-cli-20)
- [Azure CLI 1.0](#azure-cli-10)
- [Portail Azure](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a>Utilisez hello Azure CLI 2.0
Hello installation dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Redéployez votre machine virtuelle avec la commande [az vm redeploy](/cli/azure/vm#redeploy). Hello suivant redéploiements ultérieurs d’exemple hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a>Utilisez hello Azure CLI 1.0
Installer hello [dernière Azure CLI 1.0](../../cli-install-nodejs.md), connectez-vous à tooan compte Azure et vous assurer que vous êtes en mode de gestionnaire de ressources (`azure config mode arm`).

Hello suivant redéploiements ultérieurs d’exemple hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, vous trouverez une aide spécifique sur [dépannage des connexions SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [détaillée des étapes de dépannage de SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Vous pouvez également lire des informations sur les [problèmes de dépannage des applications](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) si vous ne pouvez pas accéder à une application exécutée sur votre machine virtuelle.

