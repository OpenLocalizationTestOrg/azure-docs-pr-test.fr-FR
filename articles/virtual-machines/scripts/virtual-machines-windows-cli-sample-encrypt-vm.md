---
title: aaaAzure exemple de Script CLI - chiffrer une machine virtuelle Windows | Documents Microsoft
description: "Exemple de script Azure CLI - Chiffrement d’une machine virtuelle Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 7a9928467f818cd5358d3d19bff5129d8fa21313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a>Chiffrer une machine virtuelle Windows dans Azure

Ce script crée une solution Key Vault sécurisée, des clés de chiffrement, un principal de service Azure Active Directory et une machine virtuelle Windows. Hello machine virtuelle est ensuite chiffrée à l’aide de la clé de chiffrement hello coffre de clés et les informations d’identification du principal de service.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant toocreate de commandes d’un ordinateur virtuel ressource groupe, le coffre de clés Azure, service principal, et toutes les ressources associées. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | Crée une coffre de clés Azure toostore sécuriser les données telles que des clés de chiffrement. |
| [az keyvault key create](https://docs.microsoft.com/cli/azure/keyvault/key#create) | Crée une clé de chiffrement dans Key Vault. |
| [az ad sp create-for-rbac](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | Crée un service Azure Active Directory toosecurely principal authentifier et contrôler les clés d’accès tooencryption. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Définit des autorisations sur hello coffre de clés toogrant hello service principal tooencryption clés d’accès. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau. Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.  |
| [az vm encryption enable](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | Active le chiffrement sur une machine virtuelle à l’aide des informations d’identification de hello service principal et la clé de chiffrement. |
| [az vm encryption show](https://docs.microsoft.com/cli/azure/vm/encryption#show) | Montre l’état hello Hello processus de chiffrement de machine virtuelle. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de Windows Azure VM](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).
