---
title: "Exemple de Script Azure CLI - Exporter/copier une capture instantanée en tant que VHD vers un compte de stockage dans une autre région | Microsoft Docs"
description: "Exemple de Script Azure CLI - Exporter/copier une capture instantanée en tant que VHD vers un compte de stockage dans un abonnement identique ou différent"
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
ms.openlocfilehash: fafb74af5f02f74036c770934c5e33f1b8a5593e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-cli"></a>Exporter/copier des captures instantanées managée en tant que VHD vers un compte de stockage dans une région différente avec l’interface de ligne de commande.

Ce script exporte une capture instantanée managée vers un compte de stockage dans une région différente. Il génère d’abord l’URI SAP de la capture instantanée et l’utilise ensuite pour copier celle-ci vers un compte de stockage dans une autre région. Ce script vous permet de conserver la sauvegarde de vos disques gérés dans une autre région en cas de récupération d’urgence. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copier une capture instantanée")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise les commandes suivantes afin de générer un URI SAS pour une capture instantanée gérée et copie cette dernière vers un compte de stockage à l’aide de l’URI SAS. Chaque commande du tableau renvoie à une documentation spécifique.

| Commande | Remarques |
|---|---|
| [az snapshot grant-access](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | Génère l’URI SAP en lecture seule qui est utilisé pour copier le fichier de VHD sous-jacent vers un compte de stockage ou le télécharger en local.  |
| [az storage blob copy start](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | Copie un objet blob de façon asynchrone à partir d’un compte de stockage vers un autre. |

## <a name="next-steps"></a>Étapes suivantes

[Créer un disque managé à partir d’un VHD](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[Créer une machine virtuelle à partir d’un disque managé](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle et de disques managés dans la [documentation relative aux machines virtuelles Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
