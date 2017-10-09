---
title: "aaaAzure exemple de Script CLI - redémarrer les machines virtuelles | Documents Microsoft"
description: "Exemple de script Azure CLI - Redémarrer des machines virtuelles par balise et ID"
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
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>Redémarrer les machines virtuelles

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

Cet exemple montre deux façons tooget certaines machines virtuelles et les redémarrer.

Hello redémarre tout d’abord tous les ordinateurs virtuels de hello dans le groupe de ressources hello.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

deuxième obtient hello Hello marqué à l’aide de machines virtuelles `az resouce list` filtre toohello les ressources qui sont des machines virtuelles et redémarre ces machines virtuelles.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

Cet exemple fonctionne dans une interface d’interpréteur de commandes Bash. Pour les options sur l’exécution de scripts CLI d’Azure sur le client Windows, consultez [hello CLI d’Azure en cours d’exécution dans Windows](../windows/cli-options.md).


## <a name="sample-script"></a>Exemple de script

exemple Hello possède trois scripts.
Bonjour tout d’abord un approvisionne les ordinateurs virtuels hello.
Utilise hello non-wait option commande hello retourne sans attendre sur chaque toobe de machine virtuelle configurée.
Hello attend ensuite toobe de machines virtuelles hello entièrement configuré.
script de tiers Hello redémarre tous les ordinateurs virtuels hello qui ont été configurés, et puis hello simplement marquées des machines virtuelles.

### <a name="provision-hello-vms"></a>Configurer des machines virtuelles de hello

Ce script crée un groupe de ressources, puis il crée trois machines virtuelles toorestart.
Deux présentent un indicateur.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>Wait

Ce script vérifie hello toutes les 20 secondes jusqu'à ce que tous les trois machines virtuelles sont configurés, ou un d’eux échoue tooprovision état de préparation.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>Redémarrez les ordinateurs virtuels de hello

Ce script redémarre tous les ordinateurs virtuels de hello dans le groupe de ressources hello, puis il redémarre simplement machines virtuelles hello marquée.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Après exécution de l’exemple de script hello, hello commande suivante peut être utilisé tooremove hello les groupes de ressources, de machines virtuelles et de toutes les ressources.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un groupe de ressources, machine virtuelle, haute disponibilité, équilibrage de charge et toutes les ressources. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Crée des machines virtuelles de hello.  |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | Utilisé avec `--query` tooensure hello machines virtuelles sont configurés avant de les redémarrer, et puis tooget hello ID de hello machines virtuelles toorestart les. |
| [az resource list](https://docs.microsoft.com/cli/azure/vm#list) | Utilisé avec `--query` tooget hello ID des machines virtuelles de hello à l’aide de la balise de hello. |
| [az vm restart](https://docs.microsoft.com/cli/azure/vm#list) | Redémarre les machines virtuelles de hello. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
