---
title: "aaaAzure exemple de Script CLI - créer un disque géré à partir d’un instantané | Documents Microsoft"
description: "Exemples de script Azure CLI - Créer un disque managé à partir d’une capture instantanée"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a>Créer un disque managé à partir d’une capture instantanée avec l’interface de ligne de commande

Ce script crée un disque managé à partir d’une capture instantanée. Utiliser toorestore une machine virtuelle à partir de clichés instantanés des disques du système d’exploitation et des données. Créez des disques managés de système d’exploitation et de données à partir des captures instantanées respectives, puis créez une machine virtuelle en joignant les disques managés. Vous pouvez également restaurer les disques de données d’une machine virtuelle existante en joignant les disques de données créés à partir de captures instantanées.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise à la suite de commandes toocreate un disque géré à partir d’un instantané. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Obtient toutes les propriétés hello d’un instantané à l’aide du nom de hello et les propriétés du groupe de ressources de l’instantané d’hello. Propriété ID est utilisé toocreate managé.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Crée un disque managé à l’aide de l’identifiant d’une capture instantanée managée. |

## <a name="next-steps"></a>Étapes suivantes

[Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Machine virtuelle supplémentaire et des exemples de scripts CLI de disques gérés sont accessibles dans hello [documentation de la machine virtuelle de Azure Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
