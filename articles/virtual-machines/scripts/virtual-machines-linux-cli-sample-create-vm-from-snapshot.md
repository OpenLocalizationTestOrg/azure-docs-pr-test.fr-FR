---
title: "aaaAzure exemple de Script CLI - créer une machine virtuelle à partir d’un instantané | Documents Microsoft"
description: "Exemples de script Azure CLI - Créer une machine virtuelle à partir d’une capture instantanée"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a>Créer une machine virtuelle à partir d’une capture instantanée avec l’interface de ligne de commande

Ce script crée une machine virtuelle à partir d’une capture instantanée d’un disque de système d’exploitation.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un disque géré, l’ordinateur virtuel, et toutes les ressources associées. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Obtient une capture instantanée à l’aide d’un nom de capture instantanée et d’un nom de groupe de ressources. Propriété d’ID de hello retourné d’objet est utilisé toocreate un disque géré.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Crée des disques gérés à partir d’une capture instantanée en utilisant un ID de capture instantanée, un nom de disque, un type de stockage et une taille  |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crée une machine virtuelle à l’aide d’un disque de système d’exploitation géré |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
