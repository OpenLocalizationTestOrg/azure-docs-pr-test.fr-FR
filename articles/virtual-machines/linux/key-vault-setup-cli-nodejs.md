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
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a><span data-ttu-id="3d3a3-103">Configurer le coffre de clés pour les machines virtuelles dans Azure Resource Manager par hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3d3a3-103">Set up Key Vault for virtual machines in Azure Resource Manager with hello Azure CLI 1.0</span></span>
<span data-ttu-id="3d3a3-104">Dans la pile du Gestionnaire de ressources Azure hello, secrets/certificats sont modélisées en tant que ressources qui sont fournies par le fournisseur de ressources hello de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="3d3a3-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="3d3a3-105">toolearn en savoir plus sur le coffre de clés Azure, consultez [Nouveautés d’Azure Key Vault ?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="3d3a3-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="3d3a3-106">Dans l’ordre pour toobe de coffre de clés utilisée avec les machines virtuelles Azure Resource Manager, hello *EnabledForDeployment* tootrue doit être définie à la propriété sur le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="3d3a3-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="3d3a3-107">Vous pouvez le faire dans différents clients.</span><span class="sxs-lookup"><span data-stu-id="3d3a3-107">You can do this in various clients.</span></span> <span data-ttu-id="3d3a3-108">Cet article vous montre comment tooset configuration coffre de clés pour une utilisation avec des Machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="3d3a3-108">This article shows you how tooset up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3d3a3-109">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="3d3a3-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="3d3a3-110">Vous pouvez terminer la tâche hello à l’aide de hello CLI versions suivantes</span><span class="sxs-lookup"><span data-stu-id="3d3a3-110">You can complete hello task using one of hello following CLI versions</span></span>

- <span data-ttu-id="3d3a3-111">[Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="3d3a3-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3d3a3-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="3d3a3-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="use-cli-10-tooset-up-key-vault"></a><span data-ttu-id="3d3a3-113">Utilisez tooset CLI 1.0 Configuration coffre de clés</span><span class="sxs-lookup"><span data-stu-id="3d3a3-113">Use CLI 1.0 tooset up Key Vault</span></span>
<span data-ttu-id="3d3a3-114">toocreate un coffre de clés à l’aide d’une interface de ligne hello (CLI), consultez [gérer le coffre de clés à l’aide de CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="3d3a3-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="3d3a3-115">CLI 1.0, vous disposez de coffre de clés toocreate hello avant de vous attribuez la stratégie de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="3d3a3-115">For CLI 1.0, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="3d3a3-116">Vous pouvez ensuite affecter à la stratégie de hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3d3a3-116">You can then assign hello policy by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="3d3a3-117">Tooset de modèles d’utilisation de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="3d3a3-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="3d3a3-118">Lorsque vous utilisez un modèle, vous devez tooset hello `enabledForDeployment` propriété trop`true` pour hello ressource du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="3d3a3-118">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="3d3a3-119">Pour les autres options que vous pouvez configurer lorsque vous créez un coffre de clés à l’aide de modèles, consultez la rubrique [Création d’un coffre de clés](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="3d3a3-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
