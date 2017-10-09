---
title: "Exemple de Script CLI - disque de système d’exploitation de montage d’aaaAzure | Documents Microsoft"
description: "Exemple de script Azure CLI - Monter un disque de système d’exploitation"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a>Résoudre les problèmes liés au disque du système d’exploitation de machines virtuelles

Ce script monte le disque du système d’exploitation hello d’un ordinateur virtuel a échoué ou problématique comme données disque tooa deuxième machine virtuelle. Cette procédure peut s’avérer utile lors de la résolution de problèmes de disque ou la récupération de données. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az vm show](https://docs.microsoft.com/cli/azure/vm#show) | Renvoie la liste des machines virtuelles. Dans ce cas, l’option de requête hello est disque de système d’exploitation de machine virtuelle de hello tooreturn utilisé. Cette valeur est ensuite ajoutée tooa nom de la variable « uri ». |
| [az vm delete](https://docs.microsoft.com/cli/azure/vm#delete) | Supprime une machine virtuelle. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crée une machine virtuelle.  |
| [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) | Joint un ordinateur virtuel de tooa disque. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Retourne hello des adresses IP d’un ordinateur virtuel. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
