---
title: "aaaSet d’Azure Key Vault pour les machines virtuelles Linux | Documents Microsoft"
description: "Comment tooset configuration coffre de clés pour une utilisation avec une machine virtuelle de Azure Resource Manager avec hello CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a>Comment tooset configuration coffre de clés pour les ordinateurs virtuels avec hello Azure CLI 2.0

Dans la pile du Gestionnaire de ressources Azure hello, secrets/certificats sont modélisées en tant que ressources qui sont fournies par le coffre de clés. toolearn en savoir plus sur le coffre de clés Azure, consultez [Nouveautés d’Azure Key Vault ?](../../key-vault/key-vault-whatis.md) Dans l’ordre pour toobe de coffre de clés utilisée avec les machines virtuelles du Gestionnaire de ressources Azure, hello *EnabledForDeployment* tootrue doit être définie à la propriété sur le coffre de clés. Cet article explique comment tooset configuration coffre de clés pour une utilisation avec des machines virtuelles (VM) à l’aide de hello Azure CLI 2.0. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

tooperform ces étapes, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

## <a name="create-a-key-vault"></a>Créer un coffre de clés
Créer un coffre de clés et d’attribuer la stratégie de déploiement hello [az keyvault créer](/cli/azure/keyvault#create). Hello exemple suivant crée un coffre de clés nommé `myKeyVault` Bonjour `myResourceGroup` groupe de ressources :

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a>Mettre à jour un coffre de clés pour l’utiliser avec des machines virtuelles
Définir la stratégie de déploiement de hello sur un coffre de clés existant avec [mise à jour du paramètre keyvault az](/cli/azure/keyvault#update). mises à jour suivantes Hello hello coffre de clés nommé `myKeyVault` Bonjour `myResourceGroup` groupe de ressources :

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a>Tooset de modèles d’utilisation de coffre de clés
Lorsque vous utilisez un modèle, vous devez tooset hello `enabledForDeployment` propriété trop`true` pour la ressource du coffre de clés hello comme suit :

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a>Étapes suivantes
Pour connaître les autres options que vous pouvez configurer lorsque vous créez un coffre de clés à l’aide de modèles, consultez la rubrique [Créer un coffre de clés](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
