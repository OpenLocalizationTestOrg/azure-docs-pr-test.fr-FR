---
title: "aaaCreate un VM Linux à l’aide d’un modèle Azure avec Azure CLI 1.0 | Documents Microsoft"
description: "Créer une VM Linux sur Azure à l’aide de hello Azure CLI 1.0 et un modèle Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="beaef-103">Comment toocreate un VM Linux à l’aide de hello Azure CLI 1.0 un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="beaef-103">How toocreate a Linux VM using hello Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="beaef-104">Cet article vous explique comment tooquickly déployer un ordinateur virtuel de Linux à l’aide de hello Azure CLI 1.0 et un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="beaef-104">This article shows you how tooquickly deploy a Linux Virtual Machine using hello Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="beaef-105">article de Hello nécessite :</span><span class="sxs-lookup"><span data-stu-id="beaef-105">hello article requires:</span></span>

* <span data-ttu-id="beaef-106">un compte Azure ([obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="beaef-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="beaef-107">Hello [Azure CLI 1.0](../../cli-install-nodejs.md) connecté `azure login`.</span><span class="sxs-lookup"><span data-stu-id="beaef-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="beaef-108">Hello CLI d’Azure *doit se trouver dans* mode Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="beaef-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="beaef-109">Vous pouvez rapidement déployer un modèle de Linux VM à l’aide de hello [portail Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="beaef-109">You can also quickly deploy a Linux VM template by using hello [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="beaef-110">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="beaef-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="beaef-111">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="beaef-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="beaef-112">[Azure CLI 1.0](#quick-command-summary) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="beaef-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="beaef-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="beaef-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="beaef-114">Résumé des commandes rapides</span><span class="sxs-lookup"><span data-stu-id="beaef-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="beaef-115">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="beaef-115">Detailed Walkthrough</span></span>
<span data-ttu-id="beaef-116">Les modèles permettent d’ordinateurs virtuels de toocreate sur Azure avec les paramètres que vous souhaitez toocustomize pendant le lancement de hello, des paramètres tels que les noms d’utilisateur et les noms d’hôte.</span><span class="sxs-lookup"><span data-stu-id="beaef-116">Templates allow you toocreate VMs on Azure with settings that you want toocustomize during hello launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="beaef-117">Pour cet article, nous lançons un modèle Azure utilisant une machine virtuelle Ubuntu ainsi qu’un groupe de sécurité réseau (NSG) avec le port 22 ouvert pour SSH.</span><span class="sxs-lookup"><span data-stu-id="beaef-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="beaef-118">Les modèles Azure Resource Manager sont des fichiers JSON qui peuvent être utilisés pour des tâches uniques simples telles que le lancement d’une machine virtuelle Ubuntu tel que réalisé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="beaef-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="beaef-119">Modèles Azure peuvent également être utilisé tooconstruct Azure des configurations complexes des environnements entières comme une pile de déploiement de test, de développement ou de production.</span><span class="sxs-lookup"><span data-stu-id="beaef-119">Azure Templates can also be used tooconstruct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-hello-linux-vm"></a><span data-ttu-id="beaef-120">Créer hello Linux VM</span><span class="sxs-lookup"><span data-stu-id="beaef-120">Create hello Linux VM</span></span>
<span data-ttu-id="beaef-121">Hello suivant exemple de code montre comment toocall `azure group create` toocreate une ressource de groupe et de déployer un VM Linux SSH sécurisé à hello même à l’aide de temps [ce modèle Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="beaef-121">hello following code example shows how toocall `azure group create` toocreate a resource group and deploy an SSH-secured Linux VM at hello same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="beaef-122">N’oubliez pas que dans votre exemple que vous avez besoin des noms de toouse tooyour unique environnement.</span><span class="sxs-lookup"><span data-stu-id="beaef-122">Remember that in your example you need toouse names that are unique tooyour environment.</span></span> <span data-ttu-id="beaef-123">Cet exemple utilise *myResourceGroup* en tant que nom de groupe de ressources hello, et *myVM* en tant que nom d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="beaef-123">This example uses *myResourceGroup* as hello resource group name, and *myVM* as hello VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="beaef-124">sortie de Hello doit ressembler à hello bloc de sortie :</span><span class="sxs-lookup"><span data-stu-id="beaef-124">hello output should look like hello following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="beaef-125">Cet exemple déployé une machine virtuelle à l’aide de hello `--template-uri` paramètre.</span><span class="sxs-lookup"><span data-stu-id="beaef-125">That example deployed a VM using hello `--template-uri` parameter.</span></span>  <span data-ttu-id="beaef-126">Vous pouvez également télécharger ou créer un modèle localement et passer le modèle hello à l’aide de hello `--template-file` paramètre avec un chemin d’accès de fichier de modèle toohello en tant qu’argument.</span><span class="sxs-lookup"><span data-stu-id="beaef-126">You can also download or create a template locally and pass hello template using hello `--template-file` parameter with a path toohello template file as an argument.</span></span> <span data-ttu-id="beaef-127">Hello CLI d’Azure vous invite à entrer les paramètres de hello requis par le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="beaef-127">hello Azure CLI prompts you for hello parameters required by hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="beaef-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="beaef-128">Next steps</span></span>
<span data-ttu-id="beaef-129">Hello de recherche [la galerie de modèles](https://azure.microsoft.com/documentation/templates/) toodiscover le toodeploy d’infrastructures d’application suivant.</span><span class="sxs-lookup"><span data-stu-id="beaef-129">Search hello [templates gallery](https://azure.microsoft.com/documentation/templates/) toodiscover what app frameworks toodeploy next.</span></span>

