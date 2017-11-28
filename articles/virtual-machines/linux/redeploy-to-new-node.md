---
title: "Redéploiement des machines virtuelles Linux dans Azure | Microsoft Docs"
description: "Redéploiement des machines virtuelles Linux dans Azure pour atténuer les problèmes de connexion SSH."
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
ms.openlocfilehash: 7a8653a82775e718c38f65f246d997ba61f99d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-linux-virtual-machine-to-new-azure-node"></a><span data-ttu-id="30a9a-103">Redéployer une machine virtuelle vers un nouveau nœud Azure</span><span class="sxs-lookup"><span data-stu-id="30a9a-103">Redeploy Linux virtual machine to new Azure node</span></span>
<span data-ttu-id="30a9a-104">Si vous êtes confronté à des problèmes d’accès SSH ou d’accès des applications à une machine virtuelle Linux dans Azure, vous pouvez tenter de redéployer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30a9a-104">If you face difficulties troubleshooting SSH or application access to a Linux virtual machine (VM) in Azure, redeploying the VM may help.</span></span> <span data-ttu-id="30a9a-105">Lorsque vous redéployez une machine virtuelle, celle-ci est déplacée vers un nouveau nœud au sein de l’infrastructure Azure, puis remise en service.</span><span class="sxs-lookup"><span data-stu-id="30a9a-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="30a9a-106">Toutes les options de configuration et les ressources associées sont conservées.</span><span class="sxs-lookup"><span data-stu-id="30a9a-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="30a9a-107">Cet article vous montre comment redéployer une machine virtuelle à l’aide de l’interface de ligne de commande Azure ou du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="30a9a-107">This article shows you how to redeploy a VM using Azure CLI or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="30a9a-108">Une fois que vous redéployez une machine virtuelle, le disque temporaire est perdu et les adresses IP dynamiques associées à l’interface réseau virtuelle sont mises à jour.</span><span class="sxs-lookup"><span data-stu-id="30a9a-108">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="30a9a-109">Vous pouvez redéployer une machine virtuelle à l’aide d’une des options suivantes.</span><span class="sxs-lookup"><span data-stu-id="30a9a-109">You can redeploy a VM using one of the following options.</span></span> <span data-ttu-id="30a9a-110">Choisissez une seule option pour redéployer votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="30a9a-110">You only need to choose one option to redeploy your VM:</span></span>

- [<span data-ttu-id="30a9a-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="30a9a-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="30a9a-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="30a9a-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="30a9a-113">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="30a9a-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="30a9a-114">Utiliser Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="30a9a-114">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="30a9a-115">Installez la dernière version [d’Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à un compte Azure avec la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="30a9a-115">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="30a9a-116">Redéployez votre machine virtuelle avec la commande [az vm redeploy](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="30a9a-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="30a9a-117">L’exemple suivant permet de redéployer la machine virtuelle *myVM* dans le groupe de ressources *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="30a9a-117">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="30a9a-118">Utilisation de la CLI Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="30a9a-118">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="30a9a-119">Installez la [dernière version d’Azure CLI 1.0](../../cli-install-nodejs.md), connectez-vous à un compte Azure et vérifiez que le mode Resource Manager est activé (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="30a9a-119">Install the [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in to an Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="30a9a-120">L’exemple suivant permet de redéployer la machine virtuelle *myVM* dans le groupe de ressources *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="30a9a-120">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="30a9a-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30a9a-121">Next steps</span></span>
<span data-ttu-id="30a9a-122">Vous pouvez rechercher une aide spécifique sur le [dépannage des connexions SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou sur les [étapes de dépannage détaillées des connexions SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) si vous rencontrez des problèmes de connexion à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30a9a-122">If you are having issues connecting to your VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="30a9a-123">Vous pouvez également lire des informations sur les [problèmes de dépannage des applications](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) si vous ne pouvez pas accéder à une application exécutée sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30a9a-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

