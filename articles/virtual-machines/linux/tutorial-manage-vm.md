---
title: "aaaCreate et gérer des ordinateurs virtuels Linux avec hello CLI d’Azure | Documents Microsoft"
description: "Didacticiel : créer et gérer des ordinateurs virtuels Linux avec hello CLI d’Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a><span data-ttu-id="82b5b-103">Créer et gérer des ordinateurs virtuels Linux avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="82b5b-103">Create and Manage Linux VMs with hello Azure CLI</span></span>

<span data-ttu-id="82b5b-104">Les machines virtuelles fournissent un environnement informatique entièrement configurable et flexible.</span><span class="sxs-lookup"><span data-stu-id="82b5b-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="82b5b-105">Ce didacticiel traite d’aspects de base du déploiement de machines virtuelles Azure, tels que la sélection d’une taille de machine virtuelle, la sélection d’une image de machine virtuelle et le déploiement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="82b5b-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="82b5b-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="82b5b-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82b5b-107">Créer et connecter tooa machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="82b5b-108">Sélectionner et utiliser des images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-108">Select and use VM images</span></span>
> * <span data-ttu-id="82b5b-109">Afficher et utiliser des tailles de machine virtuelle spécifiques</span><span class="sxs-lookup"><span data-stu-id="82b5b-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="82b5b-110">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-110">Resize a VM</span></span>
> * <span data-ttu-id="82b5b-111">Consulter et comprendre l’état d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="82b5b-112">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="82b5b-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="82b5b-113">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="82b5b-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="82b5b-114">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="82b5b-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="82b5b-115">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="82b5b-115">Create resource group</span></span>

<span data-ttu-id="82b5b-116">Créer un groupe de ressources avec hello [création de groupe de az](https://docs.microsoft.com/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="82b5b-116">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="82b5b-117">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="82b5b-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="82b5b-118">Un groupe de ressources doit être créé avant les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="82b5b-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="82b5b-119">Dans cet exemple, un groupe de ressources nommé *myResourceGroupVM* est créé dans hello *eastus* région.</span><span class="sxs-lookup"><span data-stu-id="82b5b-119">In this example, a resource group named *myResourceGroupVM* is created in hello *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="82b5b-120">groupe de ressources Hello est spécifié lors de la création ou la modification d’une machine virtuelle, ce qui peut être vu dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="82b5b-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="82b5b-121">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="82b5b-121">Create virtual machine</span></span>

<span data-ttu-id="82b5b-122">Créer une machine virtuelle avec hello [az vm créer](https://docs.microsoft.com/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="82b5b-122">Create a virtual machine with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="82b5b-123">Lorsque vous créez une machine virtuelle, plusieurs options sont disponibles, comme l’image de système d’exploitation, les informations d’identification d’administration ou le dimensionnement des disques.</span><span class="sxs-lookup"><span data-stu-id="82b5b-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="82b5b-124">Dans cet exemple, une machine virtuelle nommée *myVM* est créée et exécute Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="82b5b-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="82b5b-125">Une fois hello que machine virtuelle a été créé, hello CLI d’Azure génère plus d’informations sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="82b5b-125">Once hello VM has been created, hello Azure CLI outputs information about hello VM.</span></span> <span data-ttu-id="82b5b-126">Prenez note de hello `publicIpAddress`, cette adresse peut être utilisé tooaccess hello virtuels...</span><span class="sxs-lookup"><span data-stu-id="82b5b-126">Take note of hello `publicIpAddress`, this address can be used tooaccess hello virtual machine..</span></span> 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a><span data-ttu-id="82b5b-127">Se connecter tooVM</span><span class="sxs-lookup"><span data-stu-id="82b5b-127">Connect tooVM</span></span>

<span data-ttu-id="82b5b-128">Vous pouvez maintenant vous connecter toohello machine virtuelle à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="82b5b-128">You can now connect toohello VM using SSH.</span></span> <span data-ttu-id="82b5b-129">Remplacez l’exemple d’adresse IP hello avec hello `publicIpAddress` indiqué à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="82b5b-129">Replace hello example IP address with hello `publicIpAddress` noted in hello previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="82b5b-130">Une fois par hello VM, fermer la session SSH de hello.</span><span class="sxs-lookup"><span data-stu-id="82b5b-130">Once finished with hello VM, close hello SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="82b5b-131">Comprendre les images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-131">Understand VM images</span></span>

<span data-ttu-id="82b5b-132">Hello Azure marketplace inclut de nombreuses images qui peuvent être des machines virtuelles de toocreate utilisé.</span><span class="sxs-lookup"><span data-stu-id="82b5b-132">hello Azure marketplace includes many images that can be used toocreate VMs.</span></span> <span data-ttu-id="82b5b-133">Dans les étapes précédentes hello, un ordinateur virtuel a été créé à l’aide d’une image d’Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="82b5b-133">In hello previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="82b5b-134">Dans cette étape, hello que CLI d’Azure est marketplace de hello toosearch utilisé pour une image de CentOS, qui est ensuite utilisé toodeploy une deuxième machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="82b5b-134">In this step, hello Azure CLI is used toosearch hello marketplace for a CentOS image, which is then used toodeploy a second virtual machine.</span></span>  

<span data-ttu-id="82b5b-135">toosee une liste de hello couramment utilisés images, utilisez hello [liste d’images de machine virtuelle de az](/cli/azure/vm/image#list) commande.</span><span class="sxs-lookup"><span data-stu-id="82b5b-135">toosee a list of hello most commonly used images, use hello [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="82b5b-136">sortie de la commande Hello renvoie des images de machine virtuelle plus populaires hello sur Azure.</span><span class="sxs-lookup"><span data-stu-id="82b5b-136">hello command output returns hello most popular VM images on Azure.</span></span>

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

<span data-ttu-id="82b5b-137">Une liste complète peut être affichée en ajoutant hello `--all` argument.</span><span class="sxs-lookup"><span data-stu-id="82b5b-137">A full list can be seen by adding hello `--all` argument.</span></span> <span data-ttu-id="82b5b-138">liste d’images Hello peut également être filtré par `--publisher` ou `–-offer`.</span><span class="sxs-lookup"><span data-stu-id="82b5b-138">hello image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="82b5b-139">Dans cet exemple, la liste de hello est filtré pour toutes les images avec une offre qui correspond à *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="82b5b-139">In this example, hello list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="82b5b-140">Résultat partiel :</span><span class="sxs-lookup"><span data-stu-id="82b5b-140">Partial output:</span></span>

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

<span data-ttu-id="82b5b-141">toodeploy une machine virtuelle à l’aide d’une image spécifique, prenez note de la valeur de hello Bonjour *Urn* colonne.</span><span class="sxs-lookup"><span data-stu-id="82b5b-141">toodeploy a VM using a specific image, take note of hello value in hello *Urn* column.</span></span> <span data-ttu-id="82b5b-142">Lorsque vous spécifiez l’image de hello, numéro de version d’image hello peut être remplacé par « dernier », qui sélectionne la version la plus récente de la distribution de hello hello.</span><span class="sxs-lookup"><span data-stu-id="82b5b-142">When specifying hello image, hello image version number can be replaced with “latest”, which selects hello latest version of hello distribution.</span></span> <span data-ttu-id="82b5b-143">Dans cet exemple, hello `--image` argument est la version la plus récente hello toospecify utilisé d’une image CentOS 6.5.</span><span class="sxs-lookup"><span data-stu-id="82b5b-143">In this example, hello `--image` argument is used toospecify hello latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="82b5b-144">Comprendre les tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-144">Understand VM sizes</span></span>

<span data-ttu-id="82b5b-145">Une taille de machine virtuelle détermine hello des ressources de calcul tels que le processeur et mémoire GPU apportées virtuels toohello disponibles.</span><span class="sxs-lookup"><span data-stu-id="82b5b-145">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="82b5b-146">Machines virtuelles doivent toobe la taille appropriée pour la charge de travail hello attendu.</span><span class="sxs-lookup"><span data-stu-id="82b5b-146">Virtual machines need toobe sized appropriately for hello expected work load.</span></span> <span data-ttu-id="82b5b-147">Si la charge de travail augmente, une machine virtuelle existante peut être redimensionnée.</span><span class="sxs-lookup"><span data-stu-id="82b5b-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="82b5b-148">Tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-148">VM Sizes</span></span>

<span data-ttu-id="82b5b-149">Hello tableau suivant catégorise les tailles en cas d’usage.</span><span class="sxs-lookup"><span data-stu-id="82b5b-149">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="82b5b-150">Type</span><span class="sxs-lookup"><span data-stu-id="82b5b-150">Type</span></span>                     | <span data-ttu-id="82b5b-151">Tailles</span><span class="sxs-lookup"><span data-stu-id="82b5b-151">Sizes</span></span>           |    <span data-ttu-id="82b5b-152">Description</span><span class="sxs-lookup"><span data-stu-id="82b5b-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="82b5b-153">Usage général</span><span class="sxs-lookup"><span data-stu-id="82b5b-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="82b5b-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="82b5b-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="82b5b-155">Ratio processeur/mémoire équilibré.</span><span class="sxs-lookup"><span data-stu-id="82b5b-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="82b5b-156">La solution idéale pour le développement / test et des solutions d’applications et des données toomedium petit.</span><span class="sxs-lookup"><span data-stu-id="82b5b-156">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| [<span data-ttu-id="82b5b-157">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="82b5b-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="82b5b-158">Fs, F</span><span class="sxs-lookup"><span data-stu-id="82b5b-158">Fs, F</span></span>             | <span data-ttu-id="82b5b-159">Ratio processeur/mémoire élevé.</span><span class="sxs-lookup"><span data-stu-id="82b5b-159">High CPU-to-memory.</span></span> <span data-ttu-id="82b5b-160">Convient pour les applications au trafic moyen, les appliances réseau et les processus de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="82b5b-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="82b5b-161">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="82b5b-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="82b5b-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="82b5b-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="82b5b-163">Ratio mémoire/cœur élevé.</span><span class="sxs-lookup"><span data-stu-id="82b5b-163">High memory-to-core.</span></span> <span data-ttu-id="82b5b-164">Idéal pour les bases de données relationnelles, les caches toolarge moyenne et en mémoire analytique.</span><span class="sxs-lookup"><span data-stu-id="82b5b-164">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="82b5b-165">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="82b5b-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="82b5b-166">Ls</span><span class="sxs-lookup"><span data-stu-id="82b5b-166">Ls</span></span>                | <span data-ttu-id="82b5b-167">Débit de disque et E/S élevés.</span><span class="sxs-lookup"><span data-stu-id="82b5b-167">High disk throughput and IO.</span></span> <span data-ttu-id="82b5b-168">Idéale pour les bases de données NoSQL, SQL et Big Data.</span><span class="sxs-lookup"><span data-stu-id="82b5b-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="82b5b-169">GPU</span><span class="sxs-lookup"><span data-stu-id="82b5b-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="82b5b-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="82b5b-170">NV, NC</span></span>            | <span data-ttu-id="82b5b-171">Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.</span><span class="sxs-lookup"><span data-stu-id="82b5b-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="82b5b-172">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="82b5b-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="82b5b-173">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="82b5b-173">H, A8-11</span></span>          | <span data-ttu-id="82b5b-174">Nos machines virtuelles dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA).</span><span class="sxs-lookup"><span data-stu-id="82b5b-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="82b5b-175">Rechercher les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="82b5b-175">Find available VM sizes</span></span>

<span data-ttu-id="82b5b-176">toosee une liste des ordinateurs virtuels des tailles disponibles dans une région particulière, utilisez hello [liste-tailles de machine virtuelle az](/cli/azure/vm#list-sizes) commande.</span><span class="sxs-lookup"><span data-stu-id="82b5b-176">toosee a list of VM sizes available in a particular region, use hello [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="82b5b-177">Résultat partiel :</span><span class="sxs-lookup"><span data-stu-id="82b5b-177">Partial output:</span></span>

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="82b5b-178">Créer une machine virtuelle d’une taille spécifique</span><span class="sxs-lookup"><span data-stu-id="82b5b-178">Create VM with specific size</span></span>

<span data-ttu-id="82b5b-179">Dans le précédent exemple de la création de machine virtuelle hello, une taille n’est spécifié, ce qui aboutit à une taille par défaut.</span><span class="sxs-lookup"><span data-stu-id="82b5b-179">In hello previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="82b5b-180">Une taille de machine virtuelle peut être sélectionnée au moment de la création à l’aide [az vm créer](/cli/azure/vm#create) et hello `--size` argument.</span><span class="sxs-lookup"><span data-stu-id="82b5b-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and hello `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="82b5b-181">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-181">Resize a VM</span></span>

<span data-ttu-id="82b5b-182">Après avoir déployé une machine virtuelle, il peut être redimensionné tooincrease ou diminuer l’allocation de ressources.</span><span class="sxs-lookup"><span data-stu-id="82b5b-182">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="82b5b-183">Avant de redimensionner une machine virtuelle, vérifiez si hello taille souhaitée est disponible sur le cluster Azure hello actuel.</span><span class="sxs-lookup"><span data-stu-id="82b5b-183">Before resizing a VM, check if hello desired size is available on hello current Azure cluster.</span></span> <span data-ttu-id="82b5b-184">Hello [az vm-vm-resize-options de la liste](/cli/azure/vm#list-vm-resize-options) renvoie hello liste des tailles de commande.</span><span class="sxs-lookup"><span data-stu-id="82b5b-184">hello [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns hello list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="82b5b-185">Si hello souhaité de taille n’est disponible, hello machine virtuelle peut être redimensionnée à partir d’un état sous tension, mais il est redémarré au cours de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="82b5b-185">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span> <span data-ttu-id="82b5b-186">Hello d’utilisation [az vm redimensionner]( /cli/azure/vm#resize) commande tooperform hello redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="82b5b-186">Use hello [az vm resize]( /cli/azure/vm#resize) command tooperform hello resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="82b5b-187">Si vous le souhaitez hello taille n’est pas sur le cluster actuel hello, hello VM besoins toobe libérée avant que l’opération de redimensionnement hello peut se produire.</span><span class="sxs-lookup"><span data-stu-id="82b5b-187">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="82b5b-188">Hello d’utilisation [az vm désallouer]( /cli/azure/vm#deallocate) commande toostop et désallouer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="82b5b-188">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span> <span data-ttu-id="82b5b-189">Notez que, quand hello VM est sous tension précédent, toutes les données sur le disque temporaire de hello peuvent être supprimées.</span><span class="sxs-lookup"><span data-stu-id="82b5b-189">Note, when hello VM is powered back on, any data on hello temp disk may be removed.</span></span> <span data-ttu-id="82b5b-190">adresse IP publique de Hello change également, sauf si une adresse IP statique est utilisée.</span><span class="sxs-lookup"><span data-stu-id="82b5b-190">hello public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="82b5b-191">Une fois libérées, hello redimensionnement peut se produire.</span><span class="sxs-lookup"><span data-stu-id="82b5b-191">Once deallocated, hello resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="82b5b-192">Une fois hello redimensionner, hello machine virtuelle peut être démarré.</span><span class="sxs-lookup"><span data-stu-id="82b5b-192">After hello resize, hello VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="82b5b-193">États d’alimentation de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-193">VM power states</span></span>

<span data-ttu-id="82b5b-194">Une machine virtuelle Azure peut présenter différents états d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="82b5b-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="82b5b-195">Cet état représente état actuel de hello Hello machine virtuelle à partir du point de vue hello de hello hyperviseur.</span><span class="sxs-lookup"><span data-stu-id="82b5b-195">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="82b5b-196">États d’alimentation</span><span class="sxs-lookup"><span data-stu-id="82b5b-196">Power states</span></span>

| <span data-ttu-id="82b5b-197">État d’alimentation</span><span class="sxs-lookup"><span data-stu-id="82b5b-197">Power State</span></span> | <span data-ttu-id="82b5b-198">Description</span><span class="sxs-lookup"><span data-stu-id="82b5b-198">Description</span></span>
|----|----|
| <span data-ttu-id="82b5b-199">Starting</span><span class="sxs-lookup"><span data-stu-id="82b5b-199">Starting</span></span> | <span data-ttu-id="82b5b-200">Indique l’ordinateur virtuel de hello est en cours de démarrage.</span><span class="sxs-lookup"><span data-stu-id="82b5b-200">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="82b5b-201">Exécution</span><span class="sxs-lookup"><span data-stu-id="82b5b-201">Running</span></span> | <span data-ttu-id="82b5b-202">Indique que l’ordinateur virtuel hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="82b5b-202">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="82b5b-203">En cours d’arrêt</span><span class="sxs-lookup"><span data-stu-id="82b5b-203">Stopping</span></span> | <span data-ttu-id="82b5b-204">Indique que l’ordinateur virtuel hello est en cours d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="82b5b-204">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="82b5b-205">Arrêté</span><span class="sxs-lookup"><span data-stu-id="82b5b-205">Stopped</span></span> | <span data-ttu-id="82b5b-206">Indique que l’ordinateur virtuel hello est arrêté.</span><span class="sxs-lookup"><span data-stu-id="82b5b-206">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="82b5b-207">Machines virtuelles dans un état de hello arrêté peut toujours occasionner des frais de calcul.</span><span class="sxs-lookup"><span data-stu-id="82b5b-207">Virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="82b5b-208">Libération</span><span class="sxs-lookup"><span data-stu-id="82b5b-208">Deallocating</span></span> | <span data-ttu-id="82b5b-209">Indique que l’ordinateur virtuel hello est désalloué.</span><span class="sxs-lookup"><span data-stu-id="82b5b-209">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="82b5b-210">Libéré</span><span class="sxs-lookup"><span data-stu-id="82b5b-210">Deallocated</span></span> | <span data-ttu-id="82b5b-211">Indique que l’ordinateur virtuel hello est supprimé de l’hyperviseur de hello mais restent disponibles dans le plan de contrôle hello.</span><span class="sxs-lookup"><span data-stu-id="82b5b-211">Indicates that hello virtual machine is removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="82b5b-212">Machines virtuelles dans hello désallouée état n’entraînent aucun frais de calcul.</span><span class="sxs-lookup"><span data-stu-id="82b5b-212">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="82b5b-213">Indique que l’état de l’alimentation de l’ordinateur virtuel de hello hello est inconnu.</span><span class="sxs-lookup"><span data-stu-id="82b5b-213">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="82b5b-214">Rechercher un état d’alimentation</span><span class="sxs-lookup"><span data-stu-id="82b5b-214">Find power state</span></span>

<span data-ttu-id="82b5b-215">état de hello tooretrieve d’un ordinateur virtuel, utilisez hello [az vm obtenir de l’instance](/cli/azure/vm#get-instance-view) commande.</span><span class="sxs-lookup"><span data-stu-id="82b5b-215">tooretrieve hello state of a particular VM, use hello [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="82b5b-216">Être vraiment toospecify un nom valide pour un ordinateur virtuel et le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="82b5b-216">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="82b5b-217">Output:</span><span class="sxs-lookup"><span data-stu-id="82b5b-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="82b5b-218">Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="82b5b-218">Management tasks</span></span>

<span data-ttu-id="82b5b-219">Au cours de hello cycle de vie d’un ordinateur virtuel, vous souhaiterez toorun des tâches de gestion telles que le démarrage, arrêt ou suppression d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="82b5b-219">During hello life-cycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="82b5b-220">En outre, vous souhaiterez toocreate scripts tooautomate répétitives ou complexes des tâches.</span><span class="sxs-lookup"><span data-stu-id="82b5b-220">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="82b5b-221">À l’aide de hello CLI d’Azure, plusieurs tâches de gestion courantes peuvent être exécutées à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="82b5b-221">Using hello Azure CLI, many common management tasks can be run from hello command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="82b5b-222">Obtenir l’adresse IP</span><span class="sxs-lookup"><span data-stu-id="82b5b-222">Get IP address</span></span>

<span data-ttu-id="82b5b-223">Cette commande renvoie hello privés et publics adresses d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="82b5b-223">This command returns hello private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="82b5b-224">Arrêt d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="82b5b-225">Démarrage d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="82b5b-226">Supprimer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="82b5b-226">Delete resource group</span></span>

<span data-ttu-id="82b5b-227">La suppression d’un groupe de ressources supprime également toutes les ressources qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="82b5b-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="82b5b-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82b5b-228">Next steps</span></span>

<span data-ttu-id="82b5b-229">Ce didacticiel vous a montré les tâches de base de création et de gestion de machines virtuelles, notamment :</span><span class="sxs-lookup"><span data-stu-id="82b5b-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82b5b-230">Créer et connecter tooa machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-230">Create and connect tooa VM</span></span>
> * <span data-ttu-id="82b5b-231">Sélectionner et utiliser des images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-231">Select and use VM images</span></span>
> * <span data-ttu-id="82b5b-232">Afficher et utiliser des tailles de machine virtuelle spécifiques</span><span class="sxs-lookup"><span data-stu-id="82b5b-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="82b5b-233">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-233">Resize a VM</span></span>
> * <span data-ttu-id="82b5b-234">Consulter et comprendre l’état d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-234">View and understand VM state</span></span>

<span data-ttu-id="82b5b-235">Avance toohello toolearn de didacticiel suivant sur les disques de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="82b5b-235">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="82b5b-236">Créer et gérer des disques de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="82b5b-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
