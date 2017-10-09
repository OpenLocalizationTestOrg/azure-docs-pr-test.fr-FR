---
title: aaaRedeploy ordinateurs virtuels Linux dans Azure | Documents Microsoft
description: "Comment virtuels tooredeploy Linux dans la connexion SSH toomitigate Azure émet."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a><span data-ttu-id="93660-103">Redéployer toonew de machine virtuelle Linux nœud Azure</span><span class="sxs-lookup"><span data-stu-id="93660-103">Redeploy Linux virtual machine toonew Azure node</span></span>
<span data-ttu-id="93660-104">Si vous rencontrez des difficultés de résolution des problèmes de SSH ou accéder à application tooa Linux virtual machine (VM) dans Azure, redéploiement hello machine virtuelle peut aider.</span><span class="sxs-lookup"><span data-stu-id="93660-104">If you face difficulties troubleshooting SSH or application access tooa Linux virtual machine (VM) in Azure, redeploying hello VM may help.</span></span> <span data-ttu-id="93660-105">Lorsque vous redéployez un ordinateur virtuel, il déplace hello VM tooa nouveau nœud au sein de hello infrastructure Azure et donne sur toute sa puissance.</span><span class="sxs-lookup"><span data-stu-id="93660-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="93660-106">Toutes les options de configuration et les ressources associées sont conservées.</span><span class="sxs-lookup"><span data-stu-id="93660-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="93660-107">Cet article vous montre comment tooredeploy une machine virtuelle à l’aide d’Azure CLI ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="93660-107">This article shows you how tooredeploy a VM using Azure CLI or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="93660-108">Une fois que vous redéployez un ordinateur virtuel, disque temporaire de hello est perdu et les adresses IP dynamiques associés à interface réseau virtuelle sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="93660-108">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="93660-109">Vous pouvez redéployer une machine virtuelle à l’aide d’une des options suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="93660-109">You can redeploy a VM using one of hello following options.</span></span> <span data-ttu-id="93660-110">Vous devez uniquement toochoose une option tooredeploy votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="93660-110">You only need toochoose one option tooredeploy your VM:</span></span>

- [<span data-ttu-id="93660-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="93660-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="93660-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="93660-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="93660-113">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="93660-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="93660-114">Utilisez hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="93660-114">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="93660-115">Hello installation dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="93660-115">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="93660-116">Redéployez votre machine virtuelle avec la commande [az vm redeploy](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="93660-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="93660-117">Hello suivant redéploiements ultérieurs d’exemple hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="93660-117">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="93660-118">Utilisez hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="93660-118">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="93660-119">Installer hello [dernière Azure CLI 1.0](../../cli-install-nodejs.md), connectez-vous à tooan compte Azure et vous assurer que vous êtes en mode de gestionnaire de ressources (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="93660-119">Install hello [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in tooan Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="93660-120">Hello suivant redéploiements ultérieurs d’exemple hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="93660-120">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="93660-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93660-121">Next steps</span></span>
<span data-ttu-id="93660-122">Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, vous trouverez une aide spécifique sur [dépannage des connexions SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [détaillée des étapes de dépannage de SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93660-122">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="93660-123">Vous pouvez également lire des informations sur les [problèmes de dépannage des applications](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) si vous ne pouvez pas accéder à une application exécutée sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="93660-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

