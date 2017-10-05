---
title: "Exemple de script Azure CLI - Copier (déplacer) la capture instantanée d’un disque managé vers un abonnement identique ou différent avec l’interface de ligne de commande | Microsoft Docs"
description: "Exemple de script Azure CLI - Copier (déplacer) la capture instantanée d’un disque managé vers un abonnement identique ou différent avec l’interface de ligne de commande"
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
ms.openlocfilehash: 0127e342bd0c3afbe9de775399f5510814bff499
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a>Copier la capture instantanée d’un disque managé vers un abonnement identique ou différent avec l’interface de ligne de commande

Ce script copie la capture instantanée d’un disque managé vers un abonnement identique ou différent. Utilisez ce script pour déplacer une capture instantanée vers un abonnement différent dans la même région que la capture instantanée parente.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copier une capture instantanée")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise les commandes suivantes pour créer une capture instantanée dans l’abonnement cible à l’aide de l’ID de la capture instantanée source. Chaque commande du tableau renvoie à une documentation spécifique.

| Commande | Remarques |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Obtient toutes les propriétés d’une capture instantanée en utilisant les propriétés de nom et de groupe de ressources de la capture instantanée. La propriété de l’identifiant est utilisée pour copier la capture instantanée vers un autre abonnement.  |
| [az snapshot create](https://docs.microsoft.com/cli/azure/snapshot#create) | Copie une capture instantanée en créant une capture instantanée dans un abonnement différent à l’aide de l’identifiant et du nom de la capture instantanée parente.  |

## <a name="next-steps"></a>Étapes suivantes

[Créer une machine virtuelle à partir d’une capture instantanée](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle et de disques managés dans la [documentation relative aux machines virtuelles Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
