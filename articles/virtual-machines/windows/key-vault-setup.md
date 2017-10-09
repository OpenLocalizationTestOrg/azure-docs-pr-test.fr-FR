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
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="43728-103">Configuration de Key Vault pour des machines virtuelles dans Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="43728-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="43728-104">Dans la pile du Gestionnaire de ressources Azure, les secrets/certificats sont modélisées en tant que ressources qui sont fournies par le fournisseur de ressources hello de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="43728-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="43728-105">toolearn en savoir plus sur le coffre de clés, consultez [Nouveautés d’Azure Key Vault ?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="43728-105">toolearn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="43728-106">Dans l’ordre pour toobe de coffre de clés utilisée avec les machines virtuelles Azure Resource Manager, hello **EnabledForDeployment** tootrue doit être définie à la propriété sur le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="43728-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello **EnabledForDeployment** property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="43728-107">Vous pouvez le faire dans différents clients.</span><span class="sxs-lookup"><span data-stu-id="43728-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="43728-108">les besoins de coffre de clés Hello toobe créé dans hello même abonnement et l’emplacement comme hello d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="43728-108">hello Key Vault needs toobe created in hello same subscription and location as hello Virtual Machine.</span></span>
>
>

## <a name="use-powershell-tooset-up-key-vault"></a><span data-ttu-id="43728-109">Utilisez tooset PowerShell configuration coffre de clés</span><span class="sxs-lookup"><span data-stu-id="43728-109">Use PowerShell tooset up Key Vault</span></span>
<span data-ttu-id="43728-110">toocreate un coffre de clés à l’aide de PowerShell, consultez [prise en main d’Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="43728-110">toocreate a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="43728-111">Pour de nouveaux coffres de clé, vous pouvez utiliser l’applet de commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="43728-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="43728-112">Pour des coffres de clé existants, vous pouvez utiliser l’applet de commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="43728-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a><span data-ttu-id="43728-113">Nous CLI tooset configuration coffre de clés</span><span class="sxs-lookup"><span data-stu-id="43728-113">Us CLI tooset up Key Vault</span></span>
<span data-ttu-id="43728-114">toocreate un coffre de clés à l’aide d’une interface de ligne hello (CLI), consultez [gérer le coffre de clés à l’aide de CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="43728-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="43728-115">Pour l’interface CLI, vous devez coffre de clés toocreate hello avant de vous attribuez la stratégie de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="43728-115">For CLI, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="43728-116">Pour cela, à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="43728-116">You can do this by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="43728-117">Tooset de modèles d’utilisation de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="43728-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="43728-118">Lorsque vous utilisez un modèle, vous devez tooset hello `enabledForDeployment` propriété trop`true` pour hello ressource du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="43728-118">While you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="43728-119">Pour les autres options que vous pouvez configurer lorsque vous créez un coffre de clés à l’aide de modèles, consultez la rubrique [Création d’un coffre de clés](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="43728-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
