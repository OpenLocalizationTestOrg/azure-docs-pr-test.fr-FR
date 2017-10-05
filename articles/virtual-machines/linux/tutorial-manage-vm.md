---
title: "Créer et gérer des machines virtuelles Linux avec Azure CLI | Microsoft Docs"
description: "Didacticiel : créer et gérer des machines virtuelles Linux avec l’interface Azure CLI"
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
ms.openlocfilehash: c163c715eb1438a0d6b0ab53cbb43816ca8dbbb4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-linux-vms-with-the-azure-cli"></a><span data-ttu-id="bd0c0-103">Créer et gérer des machines virtuelles Linux avec l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bd0c0-103">Create and Manage Linux VMs with the Azure CLI</span></span>

<span data-ttu-id="bd0c0-104">Les machines virtuelles fournissent un environnement informatique entièrement configurable et flexible.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="bd0c0-105">Ce didacticiel traite d’aspects de base du déploiement de machines virtuelles Azure, tels que la sélection d’une taille de machine virtuelle, la sélection d’une image de machine virtuelle et le déploiement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="bd0c0-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="bd0c0-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd0c0-107">Créer une machine virtuelle et vous y connecter</span><span class="sxs-lookup"><span data-stu-id="bd0c0-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="bd0c0-108">Sélectionner et utiliser des images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-108">Select and use VM images</span></span>
> * <span data-ttu-id="bd0c0-109">Afficher et utiliser des tailles de machine virtuelle spécifiques</span><span class="sxs-lookup"><span data-stu-id="bd0c0-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="bd0c0-110">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-110">Resize a VM</span></span>
> * <span data-ttu-id="bd0c0-111">Consulter et comprendre l’état d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bd0c0-112">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter l’interface de ligne de commande Azure version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="bd0c0-113">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="bd0c0-114">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bd0c0-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="bd0c0-115">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="bd0c0-115">Create resource group</span></span>

<span data-ttu-id="bd0c0-116">Créez un groupe de ressources avec la commande [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bd0c0-116">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="bd0c0-117">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="bd0c0-118">Un groupe de ressources doit être créé avant les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="bd0c0-119">Dans cet exemple, un groupe de ressources nommé *myResourceGroupVM* est créé dans la région *eastus*.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-119">In this example, a resource group named *myResourceGroupVM* is created in the *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="bd0c0-120">Le groupe de ressources est spécifié lors de la création ou de la modification d’une machine virtuelle, qui peut être vue dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="bd0c0-121">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="bd0c0-121">Create virtual machine</span></span>

<span data-ttu-id="bd0c0-122">Créez une machine virtuelle avec la commande [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="bd0c0-122">Create a virtual machine with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="bd0c0-123">Lorsque vous créez une machine virtuelle, plusieurs options sont disponibles, comme l’image de système d’exploitation, les informations d’identification d’administration ou le dimensionnement des disques.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="bd0c0-124">Dans cet exemple, une machine virtuelle nommée *myVM* est créée et exécute Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="bd0c0-125">Une fois la machine virtuelle créée, l’interface Azure CLI fournit des informations concernant cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-125">Once the VM has been created, the Azure CLI outputs information about the VM.</span></span> <span data-ttu-id="bd0c0-126">Notez la valeur de `publicIpAddress`, car cette adresse peut être utilisée pour accéder à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-126">Take note of the `publicIpAddress`, this address can be used to access the virtual machine..</span></span> 

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

## <a name="connect-to-vm"></a><span data-ttu-id="bd0c0-127">Se connecter à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-127">Connect to VM</span></span>

<span data-ttu-id="bd0c0-128">Vous pouvez maintenant vous connecter à la machine virtuelle à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-128">You can now connect to the VM using SSH.</span></span> <span data-ttu-id="bd0c0-129">Remplacez l’exemple d’adresse IP par la valeur de `publicIpAddress` notée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-129">Replace the example IP address with the `publicIpAddress` noted in the previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="bd0c0-130">Une fois que vous avez terminé avec la machine virtuelle, fermez la session SSH.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-130">Once finished with the VM, close the SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="bd0c0-131">Comprendre les images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-131">Understand VM images</span></span>

<span data-ttu-id="bd0c0-132">La Place de marché Azure comprend de nombreuses images qui permettent de créer des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-132">The Azure marketplace includes many images that can be used to create VMs.</span></span> <span data-ttu-id="bd0c0-133">Dans les étapes précédentes, une machine virtuelle a été créée à l’aide d’une image Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-133">In the previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="bd0c0-134">Dans cette étape, vous allez utiliser l’interface Azure CLI pour rechercher dans la Place de marché une image CentOS, qui servira ensuite à déployer une deuxième machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-134">In this step, the Azure CLI is used to search the marketplace for a CentOS image, which is then used to deploy a second virtual machine.</span></span>  

<span data-ttu-id="bd0c0-135">Pour afficher une liste des images les plus couramment utilisées, utilisez la commande [az vm image list](/cli/azure/vm/image#list).</span><span class="sxs-lookup"><span data-stu-id="bd0c0-135">To see a list of the most commonly used images, use the [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="bd0c0-136">La commande renvoie les images de machine virtuelle les plus populaires sur Azure.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-136">The command output returns the most popular VM images on Azure.</span></span>

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

<span data-ttu-id="bd0c0-137">Vous pouvez obtenir une liste complète en ajoutant l’argument `--all`.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-137">A full list can be seen by adding the `--all` argument.</span></span> <span data-ttu-id="bd0c0-138">Vous pouvez également utiliser `--publisher` ou `–-offer` pour filtrer la liste d’images.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-138">The image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="bd0c0-139">Dans cet exemple, la liste est filtrée pour toutes les images dont l’offre correspond à *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-139">In this example, the list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="bd0c0-140">Résultat partiel :</span><span class="sxs-lookup"><span data-stu-id="bd0c0-140">Partial output:</span></span>

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

<span data-ttu-id="bd0c0-141">Pour déployer une machine virtuelle en utilisant une image spécifique, notez la valeur de la colonne *Urn*.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-141">To deploy a VM using a specific image, take note of the value in the *Urn* column.</span></span> <span data-ttu-id="bd0c0-142">Lorsque vous spécifiez l’image, le numéro de version de l’image peut être remplacé par la valeur « latest », qui sélectionne la dernière version de la distribution.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-142">When specifying the image, the image version number can be replaced with “latest”, which selects the latest version of the distribution.</span></span> <span data-ttu-id="bd0c0-143">Dans cet exemple, l’argument `--image` est utilisé pour spécifier la version la plus récente d’une image CentOS 6.5.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-143">In this example, the `--image` argument is used to specify the latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="bd0c0-144">Comprendre les tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-144">Understand VM sizes</span></span>

<span data-ttu-id="bd0c0-145">Une taille de machine virtuelle détermine la quantité de ressources de calcul comme le processeur, le processeur graphique (GPU) et la mémoire qui sont mises à la disposition de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-145">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="bd0c0-146">Les machines virtuelles doivent être correctement dimensionnés en fonction de la charge de travail attendue.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-146">Virtual machines need to be sized appropriately for the expected work load.</span></span> <span data-ttu-id="bd0c0-147">Si la charge de travail augmente, une machine virtuelle existante peut être redimensionnée.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="bd0c0-148">Tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-148">VM Sizes</span></span>

<span data-ttu-id="bd0c0-149">Le tableau suivant classe les tailles en fonction des cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-149">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="bd0c0-150">Type</span><span class="sxs-lookup"><span data-stu-id="bd0c0-150">Type</span></span>                     | <span data-ttu-id="bd0c0-151">Tailles</span><span class="sxs-lookup"><span data-stu-id="bd0c0-151">Sizes</span></span>           |    <span data-ttu-id="bd0c0-152">Description</span><span class="sxs-lookup"><span data-stu-id="bd0c0-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="bd0c0-153">Usage général</span><span class="sxs-lookup"><span data-stu-id="bd0c0-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="bd0c0-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="bd0c0-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="bd0c0-155">Ratio processeur/mémoire équilibré.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="bd0c0-156">Idéale pour le développement/test et pour les petites et moyennes applications et solutions de données.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-156">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| [<span data-ttu-id="bd0c0-157">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="bd0c0-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="bd0c0-158">Fs, F</span><span class="sxs-lookup"><span data-stu-id="bd0c0-158">Fs, F</span></span>             | <span data-ttu-id="bd0c0-159">Ratio processeur/mémoire élevé.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-159">High CPU-to-memory.</span></span> <span data-ttu-id="bd0c0-160">Convient pour les applications au trafic moyen, les appliances réseau et les processus de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="bd0c0-161">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="bd0c0-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="bd0c0-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="bd0c0-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="bd0c0-163">Ratio mémoire/cœur élevé.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-163">High memory-to-core.</span></span> <span data-ttu-id="bd0c0-164">Idéale pour les bases de données relationnelles, les caches moyens à grands et l’analytique en mémoire.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-164">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="bd0c0-165">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="bd0c0-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="bd0c0-166">Ls</span><span class="sxs-lookup"><span data-stu-id="bd0c0-166">Ls</span></span>                | <span data-ttu-id="bd0c0-167">Débit de disque et E/S élevés.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-167">High disk throughput and IO.</span></span> <span data-ttu-id="bd0c0-168">Idéale pour les bases de données NoSQL, SQL et Big Data.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="bd0c0-169">GPU</span><span class="sxs-lookup"><span data-stu-id="bd0c0-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="bd0c0-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="bd0c0-170">NV, NC</span></span>            | <span data-ttu-id="bd0c0-171">Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="bd0c0-172">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="bd0c0-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="bd0c0-173">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="bd0c0-173">H, A8-11</span></span>          | <span data-ttu-id="bd0c0-174">Nos machines virtuelles dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA).</span><span class="sxs-lookup"><span data-stu-id="bd0c0-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="bd0c0-175">Rechercher les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="bd0c0-175">Find available VM sizes</span></span>

<span data-ttu-id="bd0c0-176">Pour afficher la liste des tailles de machines virtuelles disponibles dans une région particulière, utilisez la commande [az vm list-sizes](/cli/azure/vm#list-sizes).</span><span class="sxs-lookup"><span data-stu-id="bd0c0-176">To see a list of VM sizes available in a particular region, use the [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="bd0c0-177">Résultat partiel :</span><span class="sxs-lookup"><span data-stu-id="bd0c0-177">Partial output:</span></span>

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

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="bd0c0-178">Créer une machine virtuelle d’une taille spécifique</span><span class="sxs-lookup"><span data-stu-id="bd0c0-178">Create VM with specific size</span></span>

<span data-ttu-id="bd0c0-179">Dans le précédent exemple de création d’une machine virtuelle, aucune taille n’a été spécifiée ; la taille par défaut a donc été appliquée.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-179">In the previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="bd0c0-180">Vous pouvez sélectionner une taille de machine virtuelle au moment de la création à l’aide de la commande [az vm create](/cli/azure/vm#create) et de l’argument `--size`.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and the `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="bd0c0-181">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-181">Resize a VM</span></span>

<span data-ttu-id="bd0c0-182">Après avoir déployé une machine virtuelle, vous pouvez la redimensionner pour augmenter ou diminuer l’allocation des ressources.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-182">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="bd0c0-183">Avant de redimensionner une machine virtuelle, vérifiez si la taille souhaitée est disponible dans le cluster Azure actuel.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-183">Before resizing a VM, check if the desired size is available on the current Azure cluster.</span></span> <span data-ttu-id="bd0c0-184">La commande [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) commande renvoie la liste des tailles disponibles.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-184">The [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns the list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="bd0c0-185">Si la taille souhaitée est disponible, la machine virtuelle peut être redimensionnée à partir d’un état sous tension, mais elle est redémarrée au cours de l’opération.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-185">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span> <span data-ttu-id="bd0c0-186">Utilisez la commande [az vm resize]( /cli/azure/vm#resize) commande pour effectuer le redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-186">Use the [az vm resize]( /cli/azure/vm#resize) command to perform the resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="bd0c0-187">Si la taille souhaitée ne figure pas dans le cluster actuel, la machine virtuelle doit être libérée avant de procéder au redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-187">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="bd0c0-188">Utilisez la commande [az vm deallocate]( /cli/azure/vm#deallocate) pour arrêter la machine virtuelle et la libérer.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-188">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span> <span data-ttu-id="bd0c0-189">Notez que lorsque la machine virtuelle est remise sous tension, toutes les données contenues dans le disque temporaire peuvent être supprimées.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-189">Note, when the VM is powered back on, any data on the temp disk may be removed.</span></span> <span data-ttu-id="bd0c0-190">L’adresse IP publique change également, sauf si une adresse IP statique est utilisée.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-190">The public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="bd0c0-191">Après la libération, le redimensionnement peut être effectué.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-191">Once deallocated, the resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="bd0c0-192">Après le redimensionnement, la machine virtuelle peut être démarrée.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-192">After the resize, the VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="bd0c0-193">États d’alimentation de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-193">VM power states</span></span>

<span data-ttu-id="bd0c0-194">Une machine virtuelle Azure peut présenter différents états d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="bd0c0-195">Cet état représente l’état actuel de la machine virtuelle du point de vue de l’hyperviseur.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-195">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="bd0c0-196">États d’alimentation</span><span class="sxs-lookup"><span data-stu-id="bd0c0-196">Power states</span></span>

| <span data-ttu-id="bd0c0-197">État d’alimentation</span><span class="sxs-lookup"><span data-stu-id="bd0c0-197">Power State</span></span> | <span data-ttu-id="bd0c0-198">Description</span><span class="sxs-lookup"><span data-stu-id="bd0c0-198">Description</span></span>
|----|----|
| <span data-ttu-id="bd0c0-199">Starting</span><span class="sxs-lookup"><span data-stu-id="bd0c0-199">Starting</span></span> | <span data-ttu-id="bd0c0-200">Indique que la machine virtuelle est en cours de démarrage.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-200">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="bd0c0-201">Exécution</span><span class="sxs-lookup"><span data-stu-id="bd0c0-201">Running</span></span> | <span data-ttu-id="bd0c0-202">Indique que la machine virtuelle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-202">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="bd0c0-203">En cours d’arrêt</span><span class="sxs-lookup"><span data-stu-id="bd0c0-203">Stopping</span></span> | <span data-ttu-id="bd0c0-204">Indique que la machine virtuelle est en cours d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-204">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="bd0c0-205">Arrêté</span><span class="sxs-lookup"><span data-stu-id="bd0c0-205">Stopped</span></span> | <span data-ttu-id="bd0c0-206">Indique que la machine virtuelle est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-206">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="bd0c0-207">Les machines virtuelles à l’état arrêté entraînent toujours des frais de calcul.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-207">Virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="bd0c0-208">Libération</span><span class="sxs-lookup"><span data-stu-id="bd0c0-208">Deallocating</span></span> | <span data-ttu-id="bd0c0-209">Indique que la machine virtuelle est en cours de libération.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-209">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="bd0c0-210">Libéré</span><span class="sxs-lookup"><span data-stu-id="bd0c0-210">Deallocated</span></span> | <span data-ttu-id="bd0c0-211">Indique que la machine virtuelle est supprimée de l’hyperviseur, mais reste disponible dans le plan de contrôle.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-211">Indicates that the virtual machine is removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="bd0c0-212">Les machines virtuelles à l’état Libéré n’entraînent pas de frais de calcul.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-212">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="bd0c0-213">Indique que l’état d’alimentation de la machine virtuelle est inconnu.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-213">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="bd0c0-214">Rechercher un état d’alimentation</span><span class="sxs-lookup"><span data-stu-id="bd0c0-214">Find power state</span></span>

<span data-ttu-id="bd0c0-215">Pour récupérer l’état d’une machine virtuelle spécifique, utilisez la commande [az vm get instance-view](/cli/azure/vm#get-instance-view).</span><span class="sxs-lookup"><span data-stu-id="bd0c0-215">To retrieve the state of a particular VM, use the [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="bd0c0-216">Veillez à spécifier le nom valide d’une machine virtuelle et d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-216">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="bd0c0-217">Output:</span><span class="sxs-lookup"><span data-stu-id="bd0c0-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="bd0c0-218">Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="bd0c0-218">Management tasks</span></span>

<span data-ttu-id="bd0c0-219">Pendant le cycle de vie d’une machine virtuelle, vous souhaiterez exécuter des tâches de gestion telles que le démarrage, l’arrêt ou la suppression d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-219">During the life-cycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="bd0c0-220">En outre, vous souhaiterez peut-être créer des scripts pour automatiser les tâches répétitives ou complexes.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-220">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="bd0c0-221">À l’aide de l’interface Azure CLI, de nombreuses tâches courantes de gestion peuvent être exécutées à partir de la ligne de commande ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-221">Using the Azure CLI, many common management tasks can be run from the command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="bd0c0-222">Obtenir l’adresse IP</span><span class="sxs-lookup"><span data-stu-id="bd0c0-222">Get IP address</span></span>

<span data-ttu-id="bd0c0-223">Cette commande renvoie les adresses IP publiques et privées d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-223">This command returns the private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="bd0c0-224">Arrêt d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="bd0c0-225">Démarrage d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="bd0c0-226">Supprimer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="bd0c0-226">Delete resource group</span></span>

<span data-ttu-id="bd0c0-227">La suppression d’un groupe de ressources supprime également toutes les ressources qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="bd0c0-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd0c0-228">Next steps</span></span>

<span data-ttu-id="bd0c0-229">Ce didacticiel vous a montré les tâches de base de création et de gestion de machines virtuelles, notamment :</span><span class="sxs-lookup"><span data-stu-id="bd0c0-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd0c0-230">Créer une machine virtuelle et vous y connecter</span><span class="sxs-lookup"><span data-stu-id="bd0c0-230">Create and connect to a VM</span></span>
> * <span data-ttu-id="bd0c0-231">Sélectionner et utiliser des images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-231">Select and use VM images</span></span>
> * <span data-ttu-id="bd0c0-232">Afficher et utiliser des tailles de machine virtuelle spécifiques</span><span class="sxs-lookup"><span data-stu-id="bd0c0-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="bd0c0-233">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-233">Resize a VM</span></span>
> * <span data-ttu-id="bd0c0-234">Consulter et comprendre l’état d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-234">View and understand VM state</span></span>

<span data-ttu-id="bd0c0-235">Passez au didacticiel suivant pour en savoir plus sur les disques de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bd0c0-235">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="bd0c0-236">Créer et gérer des disques de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bd0c0-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
