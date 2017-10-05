---
title: Configurer Key Vault pour les machines virtuelles Linux avec Azure CLI 1.0 | Microsoft Docs
description: "Configuration de Key Vault pour une utilisation avec une machine virtuelle Azure Resource Manager au moyen d’Azure CLI 1.0."
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
ms.openlocfilehash: fed612a354d45f34619f2a66bd40d78740c43ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-the-azure-cli-10"></a><span data-ttu-id="87688-103">Configurer Key Vault pour des machines virtuelles dans Azure Resource Manager avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="87688-103">Set up Key Vault for virtual machines in Azure Resource Manager with the Azure CLI 1.0</span></span>
<span data-ttu-id="87688-104">Dans la pile Azure Resource Manager, les secrets/certificats sont modélisés en tant que ressources fournies par le fournisseur de ressources de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="87688-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="87688-105">Pour en savoir plus sur Azure Key Vault, consultez [Qu’est-ce qu’Azure Key Vault ?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="87688-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="87688-106">Pour que Key Vault puisse être utilisé avec des machines virtuelles Azure Resource Manager, la propriété *EnabledForDeployment* doit être définie sur true dans Key Vault.</span><span class="sxs-lookup"><span data-stu-id="87688-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="87688-107">Vous pouvez le faire dans différents clients.</span><span class="sxs-lookup"><span data-stu-id="87688-107">You can do this in various clients.</span></span> <span data-ttu-id="87688-108">Cet article explique comment configurer Key Vault pour une utilisation avec des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="87688-108">This article shows you how to set up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="87688-109">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="87688-109">CLI versions to complete the task</span></span>
<span data-ttu-id="87688-110">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="87688-110">You can complete the task using one of the following CLI versions</span></span>

- <span data-ttu-id="87688-111">[Azure CLI 1.0](#quick-commands) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="87688-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="87688-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="87688-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="use-cli-10-to-set-up-key-vault"></a><span data-ttu-id="87688-113">Utiliser CLI 1.0 pour configurer Key Vault</span><span class="sxs-lookup"><span data-stu-id="87688-113">Use CLI 1.0 to set up Key Vault</span></span>
<span data-ttu-id="87688-114">Pour créer un coffre de clés à l’aide de l’interface de ligne de commande (CLI), consultez la rubrique [Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI)](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="87688-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="87688-115">Pour CLI 1.0, vous devez créer le coffre de clés avant d’attribuer la stratégie de déploiement.</span><span class="sxs-lookup"><span data-stu-id="87688-115">For CLI 1.0, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="87688-116">Vous pouvez ensuite attribuer la stratégie à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="87688-116">You can then assign the policy by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="87688-117">Utilisation de modèles pour configurer Key Vault</span><span class="sxs-lookup"><span data-stu-id="87688-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="87688-118">Quand vous utilisez un modèle, vous devez définir la propriété `enabledForDeployment` sur `true` pour la ressource Key Vault.</span><span class="sxs-lookup"><span data-stu-id="87688-118">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="87688-119">Pour les autres options que vous pouvez configurer lorsque vous créez un coffre de clés à l’aide de modèles, consultez la rubrique [Création d’un coffre de clés](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="87688-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
