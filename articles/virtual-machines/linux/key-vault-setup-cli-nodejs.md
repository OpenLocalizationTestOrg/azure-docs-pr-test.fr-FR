---
title: "aaaSet de coffre de clés pour les machines virtuelles Linux avec hello Azure CLI 1.0 | Documents Microsoft"
description: "Comment tooset configuration coffre de clés pour une utilisation avec une machine virtuelle de Azure Resource Manager avec Bonjour Azure CLI 1.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a>Configurer le coffre de clés pour les machines virtuelles dans Azure Resource Manager par hello Azure CLI 1.0
Dans la pile du Gestionnaire de ressources Azure hello, secrets/certificats sont modélisées en tant que ressources qui sont fournies par le fournisseur de ressources hello de coffre de clés. toolearn en savoir plus sur le coffre de clés Azure, consultez [Nouveautés d’Azure Key Vault ?](../../key-vault/key-vault-whatis.md) Dans l’ordre pour toobe de coffre de clés utilisée avec les machines virtuelles Azure Resource Manager, hello *EnabledForDeployment* tootrue doit être définie à la propriété sur le coffre de clés. Vous pouvez le faire dans différents clients. Cet article vous montre comment tooset configuration coffre de clés pour une utilisation avec des Machines virtuelles Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez terminer la tâche hello à l’aide de hello CLI versions suivantes

- [Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

## <a name="use-cli-10-tooset-up-key-vault"></a>Utilisez tooset CLI 1.0 Configuration coffre de clés
toocreate un coffre de clés à l’aide d’une interface de ligne hello (CLI), consultez [gérer le coffre de clés à l’aide de CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

CLI 1.0, vous disposez de coffre de clés toocreate hello avant de vous attribuez la stratégie de déploiement hello. Vous pouvez ensuite affecter à la stratégie de hello à l’aide de hello de commande suivante :

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Tooset de modèles d’utilisation de coffre de clés
Lorsque vous utilisez un modèle, vous devez tooset hello `enabledForDeployment` propriété trop`true` pour hello ressource du coffre de clés.

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

Pour les autres options que vous pouvez configurer lorsque vous créez un coffre de clés à l’aide de modèles, consultez la rubrique [Création d’un coffre de clés](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
