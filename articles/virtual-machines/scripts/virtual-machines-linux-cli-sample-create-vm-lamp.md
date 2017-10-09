---
title: "aaaAzure exemple de Script CLI - déployer hello pile LAMP dans un ensemble d’échelle Balanced virtuel Ajouter | Documents Microsoft"
description: "Utiliser un toodeploy hello pile LAMP de script personnalisé extension dans une charge = en puissance des machines virtuelles à charge équilibrée sur Azure."
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
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Déployer la pile de feu hello dans un ensemble d’échelle équilibrage de la charge des machines virtuelles

Cet exemple crée un ensemble d’échelle de machine virtuelle et s’applique à une extension qui exécute une pile LAMP de script personnalisé toodeploy hello sur chaque ordinateur virtuel dans un ensemble d’échelle hello.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>Connecter

Utilisez cette toosee code comment tooconnect tooyour machines virtuelles et l’échelle définies.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant commande tooremove hello groupe de ressources, un ensemble d’échelle hello et machines virtuelles et toutes les ressources.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un groupe de ressources, machine virtuelle, haute disponibilité, équilibrage de charge et toutes les ressources. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az vmss create](https://docs.microsoft.com/cli/azure/vmss#create) | Crée un groupe de machines virtuelles identiques |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Ajouter un point de terminaison à charge équilibrée |
| [az vmss extension set](https://docs.microsoft.com/cli/azure/vmss/extension#set) | Créer une extension de hello qui exécute un script personnalisé hello sur le déploiement d’une machine virtuelle |
| [az vmss update-instances](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Exécuter un script personnalisé hello sur des instances de machine virtuelle hello qui ont été déployées avant l’application d’extension de hello toohello un ensemble d’échelle. |
| [az vmss scale](https://docs.microsoft.com/cli/azure/vmss#scale) | Monter en puissance hello en ajoutant d’autres instances de machine virtuelle. un script personnalisé Hello est exécuté sur ces lorsqu’ils sont déployés. |
| [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Obtenir les adresses IP de hello Hello machines virtuelles créées par exemple hello. |
| [az network lb show](https://docs.microsoft.com/cli/azure/network/lb#show) | Obtenir des ports utilisés par l’équilibrage de charge hello principal et serveur frontal de hello. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
