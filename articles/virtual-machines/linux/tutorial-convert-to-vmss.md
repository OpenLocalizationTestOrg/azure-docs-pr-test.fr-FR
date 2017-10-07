---
title: "ensemble d’une échelle de tooa de machine virtuelle Azure aaaConvert | Documents Microsoft"
description: "Créez et déployez une échelle de machine virtuelle Linux Azure avec hello CLI d’Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="00f0d-103">Convertir un ensemble d’échelle tooa machine virtuelle Azure existante</span><span class="sxs-lookup"><span data-stu-id="00f0d-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="00f0d-104">Ce didacticiel vous montre comment toouse Azure CLI 2.0 tooconvert définie une échelle de machines virtuelles tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="00f0d-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="00f0d-105">Vous apprendrez également comment tooautomate hello d’ordinateurs virtuels hello dans l’échelle de hello configuré.</span><span class="sxs-lookup"><span data-stu-id="00f0d-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="00f0d-106">Pour plus d’informations sur comment tooinstall CLI Azure 2.0, consultez [prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="00f0d-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="00f0d-107">Pour plus d’informations sur les jeux de mise à l’échelle, consultez [Jeux de mise à l’échelle de machine virtuelle](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00f0d-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="00f0d-108">Étape 1 : hello VM annuler le déploiement</span><span class="sxs-lookup"><span data-stu-id="00f0d-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="00f0d-109">Utiliser SSH tooconnect toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="00f0d-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="00f0d-110">Hello d’annuler le déploiement machine virtuelle à l’aide de fichiers de toodelete de l’agent de machine virtuelle Azure hello et les données.</span><span class="sxs-lookup"><span data-stu-id="00f0d-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="00f0d-111">Pour obtenir une présentation détaillée de l’annulation de l’approvisionnement, consultez [Capture d’une machine virtuelle Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="00f0d-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="00f0d-112">Étape 2 : capturer une image de machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="00f0d-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="00f0d-113">Pour obtenir une présentation détaillée de la capture, consultez [Capture d’une machine virtuelle Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="00f0d-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="00f0d-114">Désallouer hello machine virtuelle avec [az vm désallouer](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="00f0d-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="00f0d-115">Généraliser hello machine virtuelle avec [az vm généraliser](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="00f0d-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="00f0d-116">Créer une image à partir de la ressource d’ordinateur virtuel hello avec [az image création](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="00f0d-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="00f0d-117">Étape 3 : création d’un ensemble d’échelle hello</span><span class="sxs-lookup"><span data-stu-id="00f0d-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="00f0d-118">Obtenir hello **id** d’image de hello.</span><span class="sxs-lookup"><span data-stu-id="00f0d-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="00f0d-119">Créez une machine virtuelle à partir de la ressource d’image à l’aide de la commande [az vmss create](/cli/azure/vmss#create) :</span><span class="sxs-lookup"><span data-stu-id="00f0d-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="00f0d-120">Cette commande joint également un disque de données de 10 Go.</span><span class="sxs-lookup"><span data-stu-id="00f0d-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="00f0d-121">N’oubliez pas que, en fonction de la machine virtuelle de hello taille choisie (nous avons utilisé **Standard_DS1_v2**), nombre de hello de disques de données autorisé est différent.</span><span class="sxs-lookup"><span data-stu-id="00f0d-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="00f0d-122">Pour plus d’informations, consultez hello [tailles de machine virtuelle](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="00f0d-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="00f0d-123">Une fois la mise à l’échelle hello terminée, connectez tooit.</span><span class="sxs-lookup"><span data-stu-id="00f0d-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="00f0d-124">Obtenir la liste d’adresses IP pour les instances de hello pour SSH avec [az mise liste-instance-connexion-info](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="00f0d-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="00f0d-125">Vous pouvez désormais connecter disque de données toohello machine virtuelle instance tooinitialize hello</span><span class="sxs-lookup"><span data-stu-id="00f0d-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="00f0d-126">Étape 4 - disque de données hello Initialize</span><span class="sxs-lookup"><span data-stu-id="00f0d-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="00f0d-127">Lors de la machine virtuelle de toohello connecté, partitionner le disque de hello avec `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="00f0d-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="00f0d-128">Écrire une partition avec hello toohello `mkfs` commande :</span><span class="sxs-lookup"><span data-stu-id="00f0d-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="00f0d-129">Monter le disque de nouveau hello afin qu’il soit accessible dans le système d’exploitation de hello :</span><span class="sxs-lookup"><span data-stu-id="00f0d-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="00f0d-130">disque de Hello peut maintenant être accède via hello datadrive point de montage, ce qui peut être vérifié avec `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="00f0d-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="00f0d-131">Fin de session SSH hello.</span><span class="sxs-lookup"><span data-stu-id="00f0d-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="00f0d-132">Étape 5 : Configuration du pare-feu</span><span class="sxs-lookup"><span data-stu-id="00f0d-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="00f0d-133">Introduire une faille via hello pare-feu toohello serveur Web hébergé par un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="00f0d-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="00f0d-134">Lors de l’ensemble d’échelle hello a été créé, un équilibreur de charge a également été créé et vous l’avez utilisé **SSH** toohello des ordinateurs virtuels individuels.</span><span class="sxs-lookup"><span data-stu-id="00f0d-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="00f0d-135">tooopen un port, vous avez besoin de deux informations que vous pouvez obtenir à l’aide de CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="00f0d-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="00f0d-136">**Pool d’adresses IP frontales**</span><span class="sxs-lookup"><span data-stu-id="00f0d-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="00f0d-137">**Pool d’adresses IP principales**</span><span class="sxs-lookup"><span data-stu-id="00f0d-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="00f0d-138">Avec ces deux noms, vous pouvez ouvrir le port **80**.</span><span class="sxs-lookup"><span data-stu-id="00f0d-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="00f0d-139">Étape 6 : Automatisation de la configuration</span><span class="sxs-lookup"><span data-stu-id="00f0d-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="00f0d-140">disque de données Hello doit toobe configuré sur chaque instance de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="00f0d-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="00f0d-141">Nous pouvons automatiser la configuration de hello de machine virtuelle hello hello **CustomScript** extension.</span><span class="sxs-lookup"><span data-stu-id="00f0d-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="00f0d-142">Commencez par créer un *.sh* script qui inclut des commandes de format de disque hello.</span><span class="sxs-lookup"><span data-stu-id="00f0d-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="00f0d-143">Ensuite, téléchargez ce hello toowhere du fichier script **CustomScript** extension peut y accéder.</span><span class="sxs-lookup"><span data-stu-id="00f0d-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="00f0d-144">Une copie est disponible [ici](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="00f0d-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="00f0d-145">Créer un fichier local nommé **settings.json** et put hello après le bloc JSON qu’elle contient.</span><span class="sxs-lookup"><span data-stu-id="00f0d-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="00f0d-146">Hello `flieUris` toowhere téléchargé vers votre fichier de script doit être affecté à la propriété.</span><span class="sxs-lookup"><span data-stu-id="00f0d-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="00f0d-147">Déployer cette mise à l’échelle tooyour commande définie par hello **CustomScript** extension, référencement hello **settings.json** fichier que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="00f0d-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="00f0d-148">Cette extension s’exécute automatiquement sur toutes les instances actuelles et toutes les instances créées ultérieurement par le biais de la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="00f0d-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="00f0d-149">Étape 7 : Configuration des règles de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="00f0d-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="00f0d-150">Actuellement, les règles de mise à l’échelle automatique ne peuvent pas être définies dans Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="00f0d-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="00f0d-151">Hello d’utilisation [portail Azure](https://portal.azure.com) tooconfigure mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="00f0d-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="00f0d-152">Étape 8 : Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="00f0d-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="00f0d-153">Tout au long du cycle de vie hello de hello ensemble d’échelle, vous devrez peut-être toorun une ou plusieurs tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="00f0d-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="00f0d-154">En outre, vous pouvez toocreate les scripts qui automatisent différentes pour les tâches de cycle de vie, et hello CLI d’Azure fournit un moyen rapide de toodo ces tâches.</span><span class="sxs-lookup"><span data-stu-id="00f0d-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="00f0d-155">Voici quelques tâches courantes.</span><span class="sxs-lookup"><span data-stu-id="00f0d-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="00f0d-156">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="00f0d-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="00f0d-157">Définir le nombre d’instances (mise à l’échelle manuelle)</span><span class="sxs-lookup"><span data-stu-id="00f0d-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="00f0d-158">Supprimer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="00f0d-158">Delete resource group</span></span>

<span data-ttu-id="00f0d-159">La suppression d’un groupe de ressources supprime également toutes les ressources qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="00f0d-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="00f0d-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00f0d-160">Next steps</span></span>
<span data-ttu-id="00f0d-161">toolearn de plus amples informations sur l’échelle de machine virtuelle hello définir des fonctionnalités introduites dans ce didacticiel, consultez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="00f0d-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="00f0d-162">Présentation des groupes de machines virtuelles identiques Azure</span><span class="sxs-lookup"><span data-stu-id="00f0d-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="00f0d-163">Vue d’ensemble d’Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="00f0d-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="00f0d-164">Contrôler le flux de trafic réseau avec les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="00f0d-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)