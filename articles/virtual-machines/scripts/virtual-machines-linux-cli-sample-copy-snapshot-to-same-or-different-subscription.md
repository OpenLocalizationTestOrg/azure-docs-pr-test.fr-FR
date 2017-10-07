---
title: "Exemple de Script CLI - instantané copie (déplacer) d’un disque géré toosame ou un autre abonnement avec l’interface CLI d’aaaAzure | Documents Microsoft"
description: "Exemple de Script CLI Azure - instantané copie (déplacer) d’un disque géré toosame ou un autre abonnement avec l’interface CLI"
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
ms.openlocfilehash: f214ab1fc1cb2cb42479d82e455f20a8cc55c83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a>Copier la capture instantanée d’un disque géré toosame ou un autre abonnement avec l’interface CLI

Ce script copie un instantané d’un disque géré toosame ou un autre abonnement. Utilisez cette toomove script un abonnement aux instantanés toodifferent Bonjour même région que l’instantané de hello parent.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise suivante commandes toocreate un instantané à l’aide d’abonnement cible hello hello Id d’instantané de source de hello. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Obtient toutes les propriétés hello d’un instantané à l’aide du nom de hello et les propriétés du groupe de ressources de l’instantané d’hello. Propriété ID est utilisé toocopy hello instantané toodifferent abonnement.  |
| [az snapshot create](https://docs.microsoft.com/cli/azure/snapshot#create) | Copie d’un instantané en créant un instantané à l’aide de l’autre abonnement hello Id et nom du hello instantané parent.  |

## <a name="next-steps"></a>Étapes suivantes

[Créer une machine virtuelle à partir d’une capture instantanée](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Machine virtuelle supplémentaire et des exemples de scripts CLI de disques gérés sont accessibles dans hello [documentation de la machine virtuelle de Azure Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
