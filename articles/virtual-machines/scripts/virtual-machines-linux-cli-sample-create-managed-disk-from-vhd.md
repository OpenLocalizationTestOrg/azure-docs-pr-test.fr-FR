---
title: "aaaAzure exemple de Script CLI - créer un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage Bonjour même abonnement | Documents Microsoft"
description: "Le Script CLI Azure exemple : création d’un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage Bonjour même abonnement"
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a>Créer un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage Bonjour même abonnement avec l’interface CLI

Ce script crée un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage Bonjour même abonnement. Utilisez cette tooimport script un spécialisé toocreate (pas généralisé/préparée avec Sysprep) disque dur virtuel toomanaged du système d’exploitation disque un ordinateur virtuel. Ou bien, utilisez-la tooimport un disque de données toomanaged données disque dur virtuel. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise à la suite de commandes toocreate un disque géré à partir d’un disque dur virtuel. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Crée un disque géré à l’aide de l’URI d’un disque dur virtuel dans un compte de stockage hello même abonnement |

## <a name="next-steps"></a>Étapes suivantes

[Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Machine virtuelle supplémentaire et des exemples de scripts CLI de disques gérés sont accessibles dans hello [documentation de la machine virtuelle de Azure Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
