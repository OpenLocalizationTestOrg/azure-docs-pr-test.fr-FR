---
title: "aaaAzure exemple de Script CLI - créer une machine virtuelle avec un disque dur virtuel | Documents Microsoft"
description: "Exemple de script Azure CLI - Créez une machine virtuelle avec un disque dur virtuel (VHD)."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>Créer une machine virtuelle avec un disque dur virtuel (VHD)

Cet exemple crée une machine virtuelle à l’aide d’un disque dur virtuel (VHD).
Il crée un groupe de ressources, un compte de stockage et un conteneur, puis il crée une machine virtuelle en téléchargeant le conteneur de toohello de disque dur virtuel hello.
Il remplace hello ssh public de clé avec votre clé publique afin que vous ayez accès toohello machine virtuelle.

Vous devez disposer d’un VHD amorçable.
Vous pouvez télécharger hello VHD que nous avons utilisés à partir de https://azclisamples.blob.core.windows.net/vhds/sample.vhd, ou utiliser votre propre disque dur virtuel. script de Hello recherche `~/sample.vhd`.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un groupe de ressources, machine virtuelle, haute disponibilité, équilibrage de charge et toutes les ressources. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az storage account list](https://docs.microsoft.com/cli/azure/storage/account#list) | Répertorie les comptes de stockage |
| [az storage account check-name](https://docs.microsoft.com/cli/azure/storage/account#check-name) | Vérifie qu’un nom de compte de stockage est valide et qu’il n’existe pas déjà |
| [az storage account keys list](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | Répertorie les clés pour les comptes de stockage hello |
| [az storage blob exists](https://docs.microsoft.com/cli/azure/storage/blob#exists) | Vérifie l’existence d’un objet blob de hello |
| [az storage container create](https://docs.microsoft.com/cli/azure/storage/container#create) | Crée un conteneur dans un compte de stockage. |
| [az storage blob upload](https://docs.microsoft.com/cli/azure/storage/blob#upload) | Crée un objet blob dans le conteneur de hello par téléchargement hello de disque dur virtuel. |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | Utilisé avec `--query` vérifier si le nom d’ordinateur virtuel hello est en cours d’utilisation. | 
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Crée des machines virtuelles de hello. |
| [az vm access set-linux-user](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | Réinitialise hello SSH toogive clé hello actuel utilisateur accès toohello machine virtuelle. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Obtient l’adresse IP de hello Hello machine virtuelle qui a été créé. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
