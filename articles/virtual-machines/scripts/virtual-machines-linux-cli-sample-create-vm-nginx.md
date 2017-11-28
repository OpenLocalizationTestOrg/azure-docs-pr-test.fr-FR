---
title: "aaaAzure exemple de Script CLI - créer un VM Linux avec NGINX | Documents Microsoft"
description: "Exemple de script Azure CLI - Création d’une machine virtuelle Linux avec NGINX"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="b4cf7-103">Créer une machine virtuelle avec NGINX</span><span class="sxs-lookup"><span data-stu-id="b4cf7-103">Create a VM with NGINX</span></span>

<span data-ttu-id="b4cf7-104">Ce script crée une Machine virtuelle Azure et utilise l’Extension de Script personnalisé Machine virtuelle Azure de hello tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-104">This script creates an Azure Virtual Machine and uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="b4cf7-105">Après avoir exécuté le script de hello, vous pouvez accéder à un site Web de démonstration sur hello adresse IP publique de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b4cf7-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="b4cf7-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a><span data-ttu-id="b4cf7-107">Extension de script personnalisé</span><span class="sxs-lookup"><span data-stu-id="b4cf7-107">Custom Script Extension</span></span>

<span data-ttu-id="b4cf7-108">extension de script personnalisé Hello copie ce script sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-108">hello custom script extension copies this script onto hello virtual machine.</span></span> <span data-ttu-id="b4cf7-109">script de Hello est alors exécutée tooinstall et configurer un serveur de web NGINX.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-109">hello script is then run tooinstall and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="b4cf7-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="b4cf7-110">Clean up deployment</span></span> 

<span data-ttu-id="b4cf7-111">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b4cf7-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="b4cf7-112">Script explanation</span></span>

<span data-ttu-id="b4cf7-113">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-113">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="b4cf7-114">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b4cf7-115">Commande</span><span class="sxs-lookup"><span data-stu-id="b4cf7-115">Command</span></span> | <span data-ttu-id="b4cf7-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="b4cf7-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b4cf7-117">az group create</span><span class="sxs-lookup"><span data-stu-id="b4cf7-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b4cf7-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b4cf7-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="b4cf7-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="b4cf7-120">Crée un ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-120">Creates hello virtual machine.</span></span> <span data-ttu-id="b4cf7-121">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-121">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="b4cf7-122">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="b4cf7-122">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="b4cf7-123">Crée un tooallow de règle de groupe de sécurité réseau le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-123">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="b4cf7-124">Dans cet exemple, le port 80 est ouvert pour le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-124">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="b4cf7-125">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="b4cf7-125">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b4cf7-126">Ajoute et exécute un tooa d’extension de machine virtuelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-126">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="b4cf7-127">Dans cet exemple, extension de script personnalisé hello est utilisé tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-127">In this sample, hello custom script extension is used tooinstall NGINX.</span></span>|
| [<span data-ttu-id="b4cf7-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="b4cf7-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b4cf7-129">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b4cf7-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b4cf7-130">Next steps</span></span>

<span data-ttu-id="b4cf7-131">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4cf7-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b4cf7-132">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4cf7-132">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
