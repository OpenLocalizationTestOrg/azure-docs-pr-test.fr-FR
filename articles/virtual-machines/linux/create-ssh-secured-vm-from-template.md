---
title: "aaaCreate un VM Linux dans Azure à partir d’un modèle | Documents Microsoft"
description: "Comment toouse hello Azure CLI 2.0 toocreate un VM Linux à partir d’un modèle de gestionnaire de ressources"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="6bcc0-103">Comment toocreate une machine virtuelle Linux modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6bcc0-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="6bcc0-104">Cet article vous explique comment tooquickly déployer un ordinateur virtuel de Linux (VM) avec les modèles Azure Resource Manager et hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="6bcc0-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="6bcc0-105">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6bcc0-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="6bcc0-106">Vue d’ensemble des modèles</span><span class="sxs-lookup"><span data-stu-id="6bcc0-106">Templates overview</span></span>
<span data-ttu-id="6bcc0-107">Les modèles de gestionnaire de ressources Azure sont des fichiers JSON qui définissent l’infrastructure de hello et la configuration de votre solution Azure.</span><span class="sxs-lookup"><span data-stu-id="6bcc0-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="6bcc0-108">Un modèle vous permet de déployer votre solution à plusieurs reprises tout au long de son cycle de vie pour avoir la garantie que vos ressources présentent un état cohérent lors de leur déploiement.</span><span class="sxs-lookup"><span data-stu-id="6bcc0-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="6bcc0-109">toolearn en savoir plus sur le format de hello du modèle de hello et comment vous construisez, consultez [créer votre premier modèle Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="6bcc0-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="6bcc0-110">tooview hello syntaxe JSON pour les types de ressources, consultez [définir des ressources dans les modèles Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="6bcc0-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="6bcc0-111">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="6bcc0-111">Create resource group</span></span>
<span data-ttu-id="6bcc0-112">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="6bcc0-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="6bcc0-113">Un groupe de ressources doit être créé avant les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6bcc0-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="6bcc0-114">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupVM* Bonjour *eastus* région :</span><span class="sxs-lookup"><span data-stu-id="6bcc0-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="6bcc0-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="6bcc0-115">Create virtual machine</span></span>
<span data-ttu-id="6bcc0-116">Hello exemple suivant crée une machine virtuelle à partir de [ce modèle Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="6bcc0-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="6bcc0-117">Fournissez une valeur de hello de votre propre clé publique SSH, telles que du contenu hello de *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="6bcc0-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="6bcc0-118">Si vous devez toocreate une paire de clés SSH, consultez [comment toocreate et utilisez un SSH paire de clés pour les machines virtuelles dans Azure Linux](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="6bcc0-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="6bcc0-119">Dans cet exemple, vous avez spécifié un modèle stocké dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="6bcc0-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="6bcc0-120">Vous pouvez également télécharger ou créer un modèle et spécifiez le chemin d’accès local de hello avec hello même `--template-file` paramètre.</span><span class="sxs-lookup"><span data-stu-id="6bcc0-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="6bcc0-121">tooSSH tooyour machine virtuelle, obtenir l’adresse IP publique de hello avec [az réseau public-ip afficher](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="6bcc0-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="6bcc0-122">Vous pouvez ensuite SSH tooyour VM normalement :</span><span class="sxs-lookup"><span data-stu-id="6bcc0-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="6bcc0-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6bcc0-123">Next steps</span></span>
<span data-ttu-id="6bcc0-124">Dans cet exemple, vous avez créé une machine virtuelle Linux de base.</span><span class="sxs-lookup"><span data-stu-id="6bcc0-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="6bcc0-125">D’autres modèles de gestionnaire de ressources qui incluent des infrastructures d’applications ou de créer des environnements plus complexes, parcourir hello [galerie de modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="6bcc0-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
