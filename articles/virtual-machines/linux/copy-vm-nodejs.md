---
title: aaaCreate une copie de votre VM Linux avec hello Azure CLI 1.0 | Documents Microsoft
description: "Découvrez comment toocreate une copie de votre machine virtuelle Azure Linux hello Azure CLI 1.0 dans le modèle de déploiement du Gestionnaire de ressources hello"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a><span data-ttu-id="bd6e6-103">Créer une copie d’une machine virtuelle de Linux en cours d’exécution sur Azure avec hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bd6e6-103">Create a copy of a Linux virtual machine running on Azure with hello Azure CLI 1.0</span></span>
<span data-ttu-id="bd6e6-104">Cet article vous explique comment une copie de votre machine virtuelle Azure (VM) en cours d’exécution Linux à l’aide de toocreate hello modèle de déploiement de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Resource Manager deployment model.</span></span> <span data-ttu-id="bd6e6-105">Tout d’abord copier sur le système d’exploitation de hello et les données des disques tooa nouveau conteneur, puis configurer les ressources du réseau hello et créer la machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-105">First you copy over hello operating system and data disks tooa new container, then set up hello network resources and create hello new virtual machine.</span></span>

<span data-ttu-id="bd6e6-106">Vous pouvez également [charger et créer une machine virtuelle à partir d’une image de disque personnalisée](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd6e6-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="bd6e6-107">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="bd6e6-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="bd6e6-108">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="bd6e6-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="bd6e6-109">CLI Azure 1.0 – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="bd6e6-109">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="bd6e6-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="bd6e6-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bd6e6-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="bd6e6-111">Before you begin</span></span>
<span data-ttu-id="bd6e6-112">Vérifiez que vous remplissez hello suivant des conditions préalables avant de commencer les étapes hello :</span><span class="sxs-lookup"><span data-stu-id="bd6e6-112">Ensure that you meet hello following prerequisites before you start hello steps:</span></span>

* <span data-ttu-id="bd6e6-113">Vous avez hello [CLI d’Azure](../../cli-install-nodejs.md) téléchargé et installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-113">You have hello [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="bd6e6-114">Vous devez également recueillir quelques informations concernant votre machine virtuelle Linux Azure existante :</span><span class="sxs-lookup"><span data-stu-id="bd6e6-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="bd6e6-115">Informations sur la machine virtuelle source</span><span class="sxs-lookup"><span data-stu-id="bd6e6-115">Source VM information</span></span> | <span data-ttu-id="bd6e6-116">Où tooget il</span><span class="sxs-lookup"><span data-stu-id="bd6e6-116">Where tooget it</span></span> |
| --- | --- |
| <span data-ttu-id="bd6e6-117">Nom de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd6e6-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="bd6e6-118">Nom du groupe ressources</span><span class="sxs-lookup"><span data-stu-id="bd6e6-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="bd6e6-119">Emplacement</span><span class="sxs-lookup"><span data-stu-id="bd6e6-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="bd6e6-120">Nom du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="bd6e6-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="bd6e6-121">Nom du conteneur</span><span class="sxs-lookup"><span data-stu-id="bd6e6-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="bd6e6-122">Nom du fichier VHD de la machine virtuelle source</span><span class="sxs-lookup"><span data-stu-id="bd6e6-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="bd6e6-123">Vous aurez besoin toomake certains choix sur votre nouvelle machine virtuelle :   </span><span class="sxs-lookup"><span data-stu-id="bd6e6-123">You will need toomake some choices about your new VM:    </span></span><br> <span data-ttu-id="bd6e6-124">-Nom du conteneur    </span><span class="sxs-lookup"><span data-stu-id="bd6e6-124">-Container name    </span></span><br> <span data-ttu-id="bd6e6-125">-Nom de la machine virtuelle    </span><span class="sxs-lookup"><span data-stu-id="bd6e6-125">-VM name    </span></span><br> <span data-ttu-id="bd6e6-126">-Taille de la machine virtuelle    </span><span class="sxs-lookup"><span data-stu-id="bd6e6-126">-VM size    </span></span><br> <span data-ttu-id="bd6e6-127">-Nom du réseau virtuel    </span><span class="sxs-lookup"><span data-stu-id="bd6e6-127">-vNet name    </span></span><br> <span data-ttu-id="bd6e6-128">-Nom du sous-réseau    </span><span class="sxs-lookup"><span data-stu-id="bd6e6-128">-SubNet name    </span></span><br> <span data-ttu-id="bd6e6-129">-Nom IP    </span><span class="sxs-lookup"><span data-stu-id="bd6e6-129">-IP Name    </span></span><br> <span data-ttu-id="bd6e6-130">-nom de la carte réseau</span><span class="sxs-lookup"><span data-stu-id="bd6e6-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="bd6e6-131">Se connecter et définir votre abonnement</span><span class="sxs-lookup"><span data-stu-id="bd6e6-131">Login and set your subscription</span></span>
1. <span data-ttu-id="bd6e6-132">Connexion toohello CLI.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-132">Login toohello CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="bd6e6-133">Assurez-vous que vous êtes en mode Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="bd6e6-134">Définir l’abonnement approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-134">Set hello correct subscription.</span></span> <span data-ttu-id="bd6e6-135">Vous pouvez utiliser « liste des comptes azure » toosee tous vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-135">You can use 'azure account list' toosee all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a><span data-ttu-id="bd6e6-136">Arrêter hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd6e6-136">Stop hello VM</span></span>
<span data-ttu-id="bd6e6-137">Arrêt et désallocation de machine virtuelle de la source hello.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-137">Stop and deallocate hello source VM.</span></span> <span data-ttu-id="bd6e6-138">Vous pouvez utiliser « liste d’ordinateur virtuel Windows azure » tooget une liste de toutes les machines virtuelles de hello dans votre abonnement et de leurs noms de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-138">You can use 'azure vm list' tooget a list of all of hello VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a><span data-ttu-id="bd6e6-139">Copiez hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="bd6e6-139">Copy hello VHD</span></span>
<span data-ttu-id="bd6e6-140">Vous pouvez copier hello disque dur virtuel à partir de la destination de toohello hello source de stockage à l’aide de hello `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-140">You can copy hello VHD from hello source storage toohello destination using hello `azure storage blob copy start`.</span></span> <span data-ttu-id="bd6e6-141">Dans cet exemple, nous allons toocopy hello VHD toohello même compte de stockage, mais un autre conteneur.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-141">In this example, we are going toocopy hello VHD toohello same storage account, but a different container.</span></span>

<span data-ttu-id="bd6e6-142">conteneur de tooanother toocopy hello VHD Bonjour même compte de stockage, tapez :</span><span class="sxs-lookup"><span data-stu-id="bd6e6-142">toocopy hello VHD tooanother container in hello same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a><span data-ttu-id="bd6e6-143">La configuration du réseau virtuel de hello pour votre nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd6e6-143">Set up hello virtual network for your new VM</span></span>
<span data-ttu-id="bd6e6-144">Configurez un réseau virtuel et une carte réseau pour votre nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="bd6e6-145">Créer hello nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd6e6-145">Create hello new VM</span></span>
<span data-ttu-id="bd6e6-146">Vous pouvez maintenant créer une machine virtuelle à partir de votre disque virtuel téléchargé [à l’aide d’un modèle de gestionnaire de ressources](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) ou via hello CLI en spécifiant hello URI tooyour copié le disque en tapant :</span><span class="sxs-lookup"><span data-stu-id="bd6e6-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through hello CLI by specifying hello URI tooyour copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="bd6e6-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd6e6-147">Next steps</span></span>
<span data-ttu-id="bd6e6-148">toolearn comment toouse CLI d’Azure toomanage votre nouvelle machine virtuelle, consultez [les commandes CLI d’Azure pour hello Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="bd6e6-148">toolearn how toouse Azure CLI toomanage your new virtual machine, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

