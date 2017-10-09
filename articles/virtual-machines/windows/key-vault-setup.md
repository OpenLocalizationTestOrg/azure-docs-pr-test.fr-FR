---
title: "aaaSet de clé de coffre pour les machines virtuelles Windows dans Azure Resource Manager | Documents Microsoft"
description: "Comment tooset configuration coffre de clés pour une utilisation avec une machine virtuelle Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Configuration de Key Vault pour des machines virtuelles dans Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

Dans la pile du Gestionnaire de ressources Azure, les secrets/certificats sont modélisées en tant que ressources qui sont fournies par le fournisseur de ressources hello de coffre de clés. toolearn en savoir plus sur le coffre de clés, consultez [Nouveautés d’Azure Key Vault ?](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. Dans l’ordre pour toobe de coffre de clés utilisée avec les machines virtuelles Azure Resource Manager, hello **EnabledForDeployment** tootrue doit être définie à la propriété sur le coffre de clés. Vous pouvez le faire dans différents clients.
> 2. les besoins de coffre de clés Hello toobe créé dans hello même abonnement et l’emplacement comme hello d’ordinateur virtuel.
>
>

## <a name="use-powershell-tooset-up-key-vault"></a>Utilisez tooset PowerShell configuration coffre de clés
toocreate un coffre de clés à l’aide de PowerShell, consultez [prise en main d’Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).

Pour de nouveaux coffres de clé, vous pouvez utiliser l’applet de commande PowerShell suivante :

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

Pour des coffres de clé existants, vous pouvez utiliser l’applet de commande PowerShell suivante :

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a>Nous CLI tooset configuration coffre de clés
toocreate un coffre de clés à l’aide d’une interface de ligne hello (CLI), consultez [gérer le coffre de clés à l’aide de CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

Pour l’interface CLI, vous devez coffre de clés toocreate hello avant de vous attribuez la stratégie de déploiement hello. Pour cela, à l’aide de hello de commande suivante :

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
