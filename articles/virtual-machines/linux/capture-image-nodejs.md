---
title: "Capturer une machine virtuelle Linux Azure à utiliser en tant que modèle | Microsoft Docs"
description: "Apprenez à capturer et à généraliser l’image d’une machine virtuelle Azure sous Linux créée avec le modèle de déploiement Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: b1164fbd816eea5189786850f096438e32f8f802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="883c6-103">Capturer une machine virtuelle Linux exécutée sur Azure</span><span class="sxs-lookup"><span data-stu-id="883c6-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="883c6-104">Suivez les étapes décrites dans cet article pour généraliser et capturer votre machine virtuelle Linux Azure dans le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="883c6-104">Follow the steps in this article to generalize and capture your Azure Linux virtual machine (VM) in the Resource Manager deployment model.</span></span> <span data-ttu-id="883c6-105">Lorsque vous généralisez la machine virtuelle, vous supprimez les informations personnelles de votre compte et vous préparez la machine virtuelle pour l’utiliser en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="883c6-105">When you generalize the VM, you remove personal account information and prepare the VM to be used as an image.</span></span> <span data-ttu-id="883c6-106">Ensuite, vous capturez une image généralisée du disque dur virtuel du système d’exploitation, les disques durs virtuels des disques de données attachés et un [modèle Resource Manager](../../azure-resource-manager/resource-group-overview.md) pour les nouveaux déploiements de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="883c6-106">You then capture a generalized virtual hard disk (VHD) image for the OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="883c6-107">Cet article explique comment capturer une image de machine virtuelle avec Azure CLI 1.0 pour une machine virtuelle utilisant des disques non gérés.</span><span class="sxs-lookup"><span data-stu-id="883c6-107">This article details how to capture a VM image with the Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="883c6-108">Vous pouvez également [capturer une machine virtuelle utilisant Azure Managed Disks à l’aide d’Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="883c6-108">You can also [capture a VM using Azure Managed Disks with the Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="883c6-109">Les disques gérés sont traités par la plateforme Azure et ne nécessitent pas de préparation ou d’emplacement pour les stocker.</span><span class="sxs-lookup"><span data-stu-id="883c6-109">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="883c6-110">Pour plus d’informations, voir la page [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Vue d’ensemble d’Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="883c6-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="883c6-111">Pour créer des machines virtuelles à l’aide de l’image, configurez les ressources réseau de chaque nouvelle machine virtuelle et utilisez le modèle (un fichier JSON ou JavaScript Object Notation) pour déployer à partir des images de disque dur virtuel capturées.</span><span class="sxs-lookup"><span data-stu-id="883c6-111">To create VMs using the image, set up network resources for each new VM, and use the template (a JavaScript Object Notation, or JSON, file) to deploy it from the captured VHD images.</span></span> <span data-ttu-id="883c6-112">De cette façon, vous pouvez répliquer une machine virtuelle avec sa configuration logicielle actuelle, comme vous utilisez des images dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="883c6-112">In this way, you can replicate a VM with its current software configuration, similar to the way you use images in the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="883c6-113">Si vous souhaitez créer une copie de votre machine virtuelle Linux existante avec son état spécialisé pour la sauvegarde ou le débogage, consultez [Créer une copie d’une machine virtuelle Linux sur Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="883c6-113">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="883c6-114">Si vous souhaitez charger un disque dur virtuel Linux à partir d’une machine virtuelle locale, consultez [Chargement et création d’une machine virtuelle à partir d’une image de disque personnalisée](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="883c6-114">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="883c6-115">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="883c6-115">CLI versions to complete the task</span></span>
<span data-ttu-id="883c6-116">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="883c6-116">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="883c6-117">[Azure CLI 1.0](#before-you-begin) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="883c6-117">[Azure CLI 1.0](#before-you-begin) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="883c6-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="883c6-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="883c6-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="883c6-119">Before you begin</span></span>
<span data-ttu-id="883c6-120">Assurez-vous de satisfaire les prérequis suivants :</span><span class="sxs-lookup"><span data-stu-id="883c6-120">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="883c6-121">**Machine virtuelle Azure créée dans le modèle de déploiement Resource Manager** : si vous n’avez pas créé une machine virtuelle Linux, vous pouvez utiliser le [portail](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [l’interface CLI Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou les [modèles Resource Manager](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="883c6-121">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="883c6-122">Configurez la machine virtuelle en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="883c6-122">Configure the VM as needed.</span></span> <span data-ttu-id="883c6-123">Par exemple, [ajoutez des disques de données](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), appliquez des mises à jour et installez des applications.</span><span class="sxs-lookup"><span data-stu-id="883c6-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="883c6-124">**Interface CLI Azure** : installez [l’interface CLI Azure](../../cli-install-nodejs.md) sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="883c6-124">**Azure CLI** - Install the [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-the-azure-linux-agent"></a><span data-ttu-id="883c6-125">Étape 1 : supprimer l’agent Linux Azure</span><span class="sxs-lookup"><span data-stu-id="883c6-125">Step 1: Remove the Azure Linux agent</span></span>
<span data-ttu-id="883c6-126">Commencez par exécuter la commande **waagent** avec le paramètre **deprovision** sur la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="883c6-126">First, run the **waagent** command with the **deprovision** parameter on the Linux VM.</span></span> <span data-ttu-id="883c6-127">Cette commande supprime les fichiers et les données pour préparer la machine virtuelle à la généralisation.</span><span class="sxs-lookup"><span data-stu-id="883c6-127">This command deletes files and data to make the VM ready for generalizing.</span></span> <span data-ttu-id="883c6-128">Pour plus d’informations, consultez le [Guide d’utilisation de l’agent Linux Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="883c6-128">For details, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="883c6-129">Connectez-vous à votre machine virtuelle Linux en utilisant un client SSH.</span><span class="sxs-lookup"><span data-stu-id="883c6-129">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="883c6-130">Dans la fenêtre SSH, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="883c6-130">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="883c6-131">Exécutez uniquement cette commande sur une machine virtuelle que vous souhaitez capturer en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="883c6-131">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="883c6-132">Cela ne garantit pas que l’image est exempte de toute information sensible ou qu’elle convient pour la redistribution.</span><span class="sxs-lookup"><span data-stu-id="883c6-132">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="883c6-133">Tapez **y** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="883c6-133">Type **y** to continue.</span></span> <span data-ttu-id="883c6-134">Vous pouvez ajouter le paramètre **-force** pour éviter cette étape de confirmation.</span><span class="sxs-lookup"><span data-stu-id="883c6-134">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="883c6-135">Une fois la commande terminée, tapez **exit**.</span><span class="sxs-lookup"><span data-stu-id="883c6-135">After the command completes, type **exit**.</span></span> <span data-ttu-id="883c6-136">Cette étape ferme le client SSH.</span><span class="sxs-lookup"><span data-stu-id="883c6-136">This step closes the SSH client.</span></span>

## <a name="step-2-capture-the-vm"></a><span data-ttu-id="883c6-137">Étape 2 : capturer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="883c6-137">Step 2: Capture the VM</span></span>
<span data-ttu-id="883c6-138">Utilisez l’interface CLI Azure pour généraliser et capturer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="883c6-138">Use the Azure CLI to generalize and capture the VM.</span></span> <span data-ttu-id="883c6-139">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="883c6-139">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="883c6-140">Les noms de paramètre sont par exemple **myResourceGroup**, **myVnet** et **myVM**.</span><span class="sxs-lookup"><span data-stu-id="883c6-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="883c6-141">À partir de l’ordinateur local, ouvrez l’interface CLI Azure et [connectez-vous à votre abonnement Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="883c6-141">From your local computer, open the Azure CLI and [login to your Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="883c6-142">Assurez-vous que vous êtes en mode Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="883c6-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="883c6-143">Arrêtez la machine virtuelle dont vous avez déjà annulé l’approvisionnement à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="883c6-143">Shut down the VM that you already deprovisioned by using the following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="883c6-144">Généralisez la machine virtuelle en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="883c6-144">Generalize the VM with the following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="883c6-145">Exécutez maintenant la commande **azure vm capture** qui capture la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="883c6-145">Now run the **azure vm capture** command, which captures the VM.</span></span> <span data-ttu-id="883c6-146">Dans l’exemple suivant, les disques durs virtuels image sont capturés avec des noms commençant par **MyVHDNamePrefix**, et l’option **-t** spécifie un chemin d’accès au modèle **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="883c6-146">In the following example, the image VHDs are captured with names beginning with **MyVHDNamePrefix**, and the **-t** option specifies a path to the template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="883c6-147">Les fichiers d’image de disque dur virtuel sont créés par défaut dans le même compte de stockage utilisé par la machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="883c6-147">The image VHD files get created by default in the same storage account that the original VM used.</span></span> <span data-ttu-id="883c6-148">Utilisez le *même compte de stockage* pour stocker les disques durs virtuels des nouvelles machines virtuelles créées à partir de l’image.</span><span class="sxs-lookup"><span data-stu-id="883c6-148">Use the *same storage account* to store the VHDs for any new VMs you create from the image.</span></span> 

6. <span data-ttu-id="883c6-149">Pour rechercher l’emplacement d’une image capturée, ouvrez le modèle JSON dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="883c6-149">To find the location of a captured image, open the JSON template in a text editor.</span></span> <span data-ttu-id="883c6-150">Dans **storageProfile**, recherchez **l’uri** de **l’image** située dans le conteneur **system**.</span><span class="sxs-lookup"><span data-stu-id="883c6-150">In the **storageProfile**, find the **uri** of the **image** located in the **system** container.</span></span> <span data-ttu-id="883c6-151">Par exemple, l’URI de l’image du disque du système d’exploitation est semblable à `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="883c6-151">For example, the URI of the OS disk image is similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="883c6-152">Étape 3 : créer une machine virtuelle à partir de l’image capturée</span><span class="sxs-lookup"><span data-stu-id="883c6-152">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="883c6-153">Maintenant, utilisez l’image avec un modèle pour créer une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="883c6-153">Now use the image with a template to create a Linux VM.</span></span> <span data-ttu-id="883c6-154">Ces étapes vous montrent comment utiliser l’interface CLI Azure et le modèle de fichier JSON capturé pour créer la machine virtuelle dans un nouveau réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="883c6-154">These steps show you how to use the Azure CLI and the JSON file template you captured to create the VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="883c6-155">Créer des ressources réseau</span><span class="sxs-lookup"><span data-stu-id="883c6-155">Create network resources</span></span>
<span data-ttu-id="883c6-156">Pour utiliser le modèle, vous devez d’abord configurer un réseau virtuel et une carte réseau pour votre nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="883c6-156">To use the template, you first need to set up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="883c6-157">Nous vous recommandons de créer un groupe de ressources pour ces ressources à l’emplacement de stockage de votre image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="883c6-157">We recommend you create a resource group for these resources in the location where your VM image is stored.</span></span> <span data-ttu-id="883c6-158">Exécutez des commandes comme suit en remplaçant les noms de vos ressources et de l’emplacement Azure approprié (« centralus » dans ces commandes) :</span><span class="sxs-lookup"><span data-stu-id="883c6-158">Run commands similar to the following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-the-id-of-the-nic"></a><span data-ttu-id="883c6-159">Obtenir l’ID de la carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="883c6-159">Get the Id of the NIC</span></span>
<span data-ttu-id="883c6-160">Pour déployer une machine virtuelle à l’aide du fichier JSON que vous avez enregistré pendant la capture, vous avez besoin de l’ID de la carte d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="883c6-160">To deploy a VM from the image by using the JSON you saved during capture, you need the Id of the NIC.</span></span> <span data-ttu-id="883c6-161">Obtenez-le en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="883c6-161">Obtain it by running the following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="883c6-162">**L’ID** du résultat ressemble à `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`.</span><span class="sxs-lookup"><span data-stu-id="883c6-162">The **Id** in the output is similar to `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="883c6-163">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="883c6-163">Create a VM</span></span>
<span data-ttu-id="883c6-164">Exécutez maintenant la commande suivante pour créer votre machine virtuelle à partir de l’image de machine virtuelle capturée.</span><span class="sxs-lookup"><span data-stu-id="883c6-164">Now run the following command to create your VM from the captured VM image.</span></span> <span data-ttu-id="883c6-165">Utilisez le paramètre **-f** pour spécifier le chemin d’accès au modèle de fichier JSON enregistré.</span><span class="sxs-lookup"><span data-stu-id="883c6-165">Use the **-f** parameter to specify the path to the template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="883c6-166">Dans la sortie de commande, vous êtes invité à fournir un nouveau nom de machine virtuelle, le nom d’utilisateur administrateur et un mot de passe et l’ID de la carte d’interface réseau que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="883c6-166">In the command output, you are prompted to supply a new VM name, the admin user name and password, and the Id of the NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="883c6-167">L’exemple suivant montre ce que vous voyez en cas de déploiement réussi :</span><span class="sxs-lookup"><span data-stu-id="883c6-167">The following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment to complete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-the-deployment"></a><span data-ttu-id="883c6-168">Vérifier le déploiement</span><span class="sxs-lookup"><span data-stu-id="883c6-168">Verify the deployment</span></span>
<span data-ttu-id="883c6-169">Maintenant, exécutez le SSH sur la machine virtuelle que vous avez créée pour vérifier le déploiement et lancez le déploiement et le démarrage de l’utilisation de la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="883c6-169">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="883c6-170">Pour vous connecter via SSH, recherchez l’adresse IP de la machine virtuelle que vous avez créée en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="883c6-170">To connect via SSH, find the IP address of the VM you created by running the following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="883c6-171">L’adresse IP publique est répertoriée dans la sortie de commande.</span><span class="sxs-lookup"><span data-stu-id="883c6-171">The public IP address is listed in the command output.</span></span> <span data-ttu-id="883c6-172">Par défaut, vous vous connectez à la VM Linux par SSH sur le port 22.</span><span class="sxs-lookup"><span data-stu-id="883c6-172">By default you connect to the Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="883c6-173">Créer des machines virtuelles supplémentaires</span><span class="sxs-lookup"><span data-stu-id="883c6-173">Create additional VMs</span></span>
<span data-ttu-id="883c6-174">Utilisez le modèle et l’image capturée pour déployer des machines virtuelles supplémentaires à l’aide de la procédure de la section précédente.</span><span class="sxs-lookup"><span data-stu-id="883c6-174">Use the captured image and template to deploy additional VMs using the steps in the preceding section.</span></span> <span data-ttu-id="883c6-175">Les autres options de création de machines virtuelles à partir de l’image incluent l’utilisation d’un modèle de démarrage rapide ou l’exécution de la commande **azure vm create**.</span><span class="sxs-lookup"><span data-stu-id="883c6-175">Other options to create VMs from the image include using a quickstart template or running the **azure vm create** command.</span></span>

### <a name="use-the-captured-template"></a><span data-ttu-id="883c6-176">Utiliser le modèle capturé</span><span class="sxs-lookup"><span data-stu-id="883c6-176">Use the captured template</span></span>
<span data-ttu-id="883c6-177">Pour utiliser l’image capturée et le modèle, suivez cette procédure (détaillée dans la section précédente) :</span><span class="sxs-lookup"><span data-stu-id="883c6-177">To use the captured image and template, follow these steps (detailed in the preceding section):</span></span>

* <span data-ttu-id="883c6-178">Assurez-vous que votre image de machine virtuelle se trouve dans le compte de stockage qui héberge le disque dur virtuel de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="883c6-178">Ensure that your VM image is in the same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="883c6-179">Copiez le modèle de fichier JSON et spécifiez un nom unique pour le disque du système d’exploitation du (ou des) disque(s) dur(s) virtuel(s) de la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="883c6-179">Copy the template JSON file and specify a unique name for the OS disk of the new VM's VHD (or VHDs).</span></span> <span data-ttu-id="883c6-180">Par exemple, dans **storageProfile**, sous **vhd**, dans **uri**, spécifiez un nom unique pour le disque dur virtuel **osDisk**, similaire à `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="883c6-180">For example, in the **storageProfile**, under **vhd**, in **uri**, specify a unique name for the **osDisk** VHD, similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="883c6-181">Créez une carte d’interface réseau dans un réseau virtuel identique ou différent.</span><span class="sxs-lookup"><span data-stu-id="883c6-181">Create a NIC in either the same or a different virtual network.</span></span>
* <span data-ttu-id="883c6-182">À l’aide du modèle de fichier JSON modifié, créez un déploiement dans le groupe de ressources dans lequel vous configurez le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="883c6-182">Using the modified template JSON file, create a deployment in the resource group in which you set up the virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="883c6-183">Utilisation d’un modèle de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="883c6-183">Use a quickstart template</span></span>
<span data-ttu-id="883c6-184">Si vous souhaitez que le réseau soit automatiquement configuré lorsque vous créez une machine virtuelle à partir de l’image, vous pouvez spécifier ces ressources dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="883c6-184">If you want the network set up automatically when you create a VM from the image, you can specify those resources in a template.</span></span> <span data-ttu-id="883c6-185">Par exemple, consultez le [modèle 101-vm-from-user-image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="883c6-185">For example, see the [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="883c6-186">Ce modèle crée un ordinateur virtuel à partir de votre image personnalisée et des ressources virtuelles réseau nécessaires, de l’adresse IP publique et des ressources de carte réseau.</span><span class="sxs-lookup"><span data-stu-id="883c6-186">This template creates a VM from your custom image and the necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="883c6-187">Pour une démonstration de l’utilisation du modèle dans le portail Azure, consultez [Comment créer une machine virtuelle à partir d’une image personnalisée à l’aide d’un modèle ARM](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/)(en anglais).</span><span class="sxs-lookup"><span data-stu-id="883c6-187">For a walkthrough of using the template in the Azure portal, see [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-the-azure-vm-create-command"></a><span data-ttu-id="883c6-188">Utilisation de la commande azure vm create</span><span class="sxs-lookup"><span data-stu-id="883c6-188">Use the azure vm create command</span></span>
<span data-ttu-id="883c6-189">En général, il est plus facile d’utiliser un modèle Resource Manager pour créer une machine virtuelle à partir de l’image.</span><span class="sxs-lookup"><span data-stu-id="883c6-189">Usually it's easiest to use a Resource Manager template to create a VM from the image.</span></span> <span data-ttu-id="883c6-190">Toutefois, vous pouvez créer la machine virtuelle de façon *impérative* à l’aide de la commande **azure vm create** avec le paramètre **-Q** (**--image-urn**).</span><span class="sxs-lookup"><span data-stu-id="883c6-190">However, you can create the VM *imperatively* by using the **azure vm create** command with the **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="883c6-191">Si vous utilisez cette méthode, vous devez également transmettre le paramètre **-d** (**--os-disk-vhd**) pour spécifier l’emplacement du fichier .vhd du système d’exploitation pour la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="883c6-191">If you use this method, you also pass the **-d** (**--os-disk-vhd**) parameter to specify the location of the OS .vhd file for the new VM.</span></span> <span data-ttu-id="883c6-192">Ce fichier doit se trouver dans le conteneur de disques durs virtuels du compte de stockage sur lequel se trouve le fichier d’image du disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="883c6-192">This file must be in the vhds container of the storage account where the image VHD file is stored.</span></span> <span data-ttu-id="883c6-193">La commande copie le disque dur virtuel pour la nouvelle machine virtuelle automatiquement sur le conteneur de disques durs virtuels **vhds**.</span><span class="sxs-lookup"><span data-stu-id="883c6-193">The command copies the VHD for the new VM automatically to the **vhds** container.</span></span>

<span data-ttu-id="883c6-194">Avant d’exécuter **azure vm create** avec l’image, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="883c6-194">Before running **azure vm create** with the image, complete the following steps:</span></span>

1. <span data-ttu-id="883c6-195">Créez un groupe de ressources ou identifiez un groupe de ressources existant pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="883c6-195">Create a resource group, or identify an existing resource group for the deployment.</span></span>
2. <span data-ttu-id="883c6-196">Créez une ressource d’adresse IP publique et une ressource de la carte réseau pour la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="883c6-196">Create a public IP address resource and a NIC resource for the new VM.</span></span> <span data-ttu-id="883c6-197">Pour savoir comment créer un réseau virtuel, une adresse IP publique et une carte réseau à l’aide de l’interface CLI, voir plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="883c6-197">For steps to create a virtual network, public IP address, and NIC by using the CLI, see earlier in this article.</span></span> <span data-ttu-id="883c6-198">(**azure vm create** peut également créer une carte d’interface réseau, mais vous devez transmettre des paramètres supplémentaires pour un réseau virtuel et un sous-réseau.)</span><span class="sxs-lookup"><span data-stu-id="883c6-198">(**azure vm create** can also create a NIC, but you need to pass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="883c6-199">Ensuite, exécutez une commande transmettant des URI vers le nouveau fichier de disque dur virtuel de système d’exploitation et l’image existante.</span><span class="sxs-lookup"><span data-stu-id="883c6-199">Then run a command that passes URIs to both the new OS VHD file and the existing image.</span></span> <span data-ttu-id="883c6-200">Dans cet exemple, une machine virtuelle de taille Standard_A1 est créée dans la région Est des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="883c6-200">In this example, a size Standard_A1 VM is created in the East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="883c6-201">Pour obtenir d’autres options de commande supplémentaires, exécutez `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="883c6-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="883c6-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="883c6-202">Next steps</span></span>
<span data-ttu-id="883c6-203">Pour gérer vos machines virtuelles à l’aide de l’interface de ligne de commande, consultez les tâches décrites dans [Déploiement et gestion de machines virtuelles à l’aide des modèles Azure Resource Manager et de l’interface de ligne de commande Azure](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="883c6-203">To manage your VMs with the CLI, see the tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

