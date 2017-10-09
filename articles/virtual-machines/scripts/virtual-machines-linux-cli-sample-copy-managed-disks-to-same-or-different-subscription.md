---
title: "aaaAzure exemple de Script CLI - copie (déplacer) géré toosame de disques ou d’un autre abonnement | Documents Microsoft"
description: "Exemple de Script CLI Azure - Copy (déplacer) gérés disques toosame ou autre abonnement"
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
ms.openlocfilehash: b1fa207bd6e05d7094be08855e7823e3b7686013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>Copier les disques gérés toosame ou autre abonnement avec l’interface CLI

Ce script copie un disque géré toosame ou un autre abonnement, mais dans hello même région. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise suivante commandes toocreate un nouveau disque géré à l’aide d’abonnement cible hello hello Id de source de hello gérés disque. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#show) | Obtient toutes les propriétés de hello d’un disque géré à l’aide des propriétés du groupe hello nom et les ressources de disque géré de hello. Propriété ID est utilisé toocopy hello géré disque toodifferent abonnement.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Copie d’un disque géré en créant un nouveau disque géré dans un autre abonnement à l’aide d’Id et nom du parent de hello gérés disque.  |

## <a name="next-steps"></a>Étapes suivantes

[Créer une machine virtuelle à partir d’un disque géré](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Machine virtuelle supplémentaire et des exemples de scripts CLI de disques gérés sont accessibles dans hello [documentation de la machine virtuelle de Azure Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
