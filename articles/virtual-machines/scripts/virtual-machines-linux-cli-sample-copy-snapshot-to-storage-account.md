---
title: "aaaAzure exemple de Script CLI - instantané/copie de l’exportation en tant que compte de stockage de disque dur virtuel tooa dans autre région | Documents Microsoft"
description: "Exemple de Script CLI Azure - instantané/copie de l’exportation en tant que compte de stockage de disque dur virtuel tooa dans l’abonnement identique ou différent"
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
ms.openlocfilehash: 945f83d2ed715642156ca7b252af08559c652b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a>Exportation ou copier des instantanés gérés en tant que compte de stockage de disque dur virtuel tooa dans autre région avec l’interface CLI

Ce script exporte un compte de stockage géré instantané tooa dans autre région. Il génère d’abord hello URI SAS d’instantané de hello et utilise ensuite toocopy il compte de stockage tooa dans autre région. Utilisez cette sauvegarde toomaintain de script de vos disques gérés dans autre région pour la récupération d’urgence. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise suivante commandes toogenerate URI SAS pour un Bonjour de capture instantanée ni copie managé d’instantané tooa compte de stockage à l’aide de l’URI SAS. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az snapshot grant-access](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | Génère les associations de sécurité en lecture seule qui sont utilisé toocopy sous-jacent du compte de stockage de tooa de fichier de disque dur virtuel ou le télécharger tooon local  |
| [az storage blob copy start](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | Copie un objet blob de façon asynchrone à partir d’un tooanother de compte de stockage |

## <a name="next-steps"></a>Étapes suivantes

[Créer un disque managé à partir d’un VHD](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[Créer une machine virtuelle à partir d’un disque géré](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Machine virtuelle supplémentaire et des exemples de scripts CLI de disques gérés sont accessibles dans hello [documentation de la machine virtuelle de Azure Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
