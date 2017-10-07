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
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a><span data-ttu-id="9aa95-103">Comment tooset configuration coffre de clés pour les ordinateurs virtuels avec hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9aa95-103">How tooset up Key Vault for virtual machines with hello Azure CLI 2.0</span></span>

<span data-ttu-id="9aa95-104">Dans la pile du Gestionnaire de ressources Azure hello, secrets/certificats sont modélisées en tant que ressources qui sont fournies par le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="9aa95-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="9aa95-105">toolearn en savoir plus sur le coffre de clés Azure, consultez [Nouveautés d’Azure Key Vault ?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="9aa95-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="9aa95-106">Dans l’ordre pour toobe de coffre de clés utilisée avec les machines virtuelles du Gestionnaire de ressources Azure, hello *EnabledForDeployment* tootrue doit être définie à la propriété sur le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="9aa95-106">In order for Key Vault toobe used with Azure Resource Manager VMs, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="9aa95-107">Cet article explique comment tooset configuration coffre de clés pour une utilisation avec des machines virtuelles (VM) à l’aide de hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="9aa95-107">This article shows you how tooset up Key Vault for use with Azure virtual machines (VMs) using hello Azure CLI 2.0.</span></span> <span data-ttu-id="9aa95-108">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9aa95-108">You can also perform these steps with hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9aa95-109">tooperform ces étapes, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="9aa95-109">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="9aa95-110">Créer un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="9aa95-110">Create a Key Vault</span></span>
<span data-ttu-id="9aa95-111">Créer un coffre de clés et d’attribuer la stratégie de déploiement hello [az keyvault créer](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="9aa95-111">Create a key vault and assign hello deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="9aa95-112">Hello exemple suivant crée un coffre de clés nommé `myKeyVault` Bonjour `myResourceGroup` groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="9aa95-112">hello following example creates a key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="9aa95-113">Mettre à jour un coffre de clés pour l’utiliser avec des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="9aa95-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="9aa95-114">Définir la stratégie de déploiement de hello sur un coffre de clés existant avec [mise à jour du paramètre keyvault az](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="9aa95-114">Set hello deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="9aa95-115">mises à jour suivantes Hello hello coffre de clés nommé `myKeyVault` Bonjour `myResourceGroup` groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="9aa95-115">hello following updates hello key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="9aa95-116">Tooset de modèles d’utilisation de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="9aa95-116">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="9aa95-117">Lorsque vous utilisez un modèle, vous devez tooset hello `enabledForDeployment` propriété trop`true` pour la ressource du coffre de clés hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9aa95-117">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource as follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9aa95-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9aa95-118">Next steps</span></span>
<span data-ttu-id="9aa95-119">Pour connaître les autres options que vous pouvez configurer lorsque vous créez un coffre de clés à l’aide de modèles, consultez la rubrique [Créer un coffre de clés](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="9aa95-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
