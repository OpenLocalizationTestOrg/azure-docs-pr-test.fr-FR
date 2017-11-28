---
title: "aaaCapture toouse d’une machine virtuelle de Azure Linux en tant que modèle | Documents Microsoft"
description: "Découvrez comment toocapture et généraliser une image d’une basés sur Linux Azure virtual machine (VM) créée avec le modèle de déploiement du Gestionnaire de ressources Azure hello."
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
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="65ad6-103">Capturer une machine virtuelle Linux exécutée sur Azure</span><span class="sxs-lookup"><span data-stu-id="65ad6-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="65ad6-104">Suivez les étapes de hello dans cet article de toogeneralize et capturer votre machine virtuelle de Azure Linux (VM) dans le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="65ad6-104">Follow hello steps in this article toogeneralize and capture your Azure Linux virtual machine (VM) in hello Resource Manager deployment model.</span></span> <span data-ttu-id="65ad6-105">Lorsque vous généralisez hello machine virtuelle, vous supprimez les informations de compte personnelles et préparez hello VM toobe est utilisé en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="65ad6-105">When you generalize hello VM, you remove personal account information and prepare hello VM toobe used as an image.</span></span> <span data-ttu-id="65ad6-106">Vous puis capture un disque dur virtuel (VHD) généralisé l’image pour hello du système d’exploitation, les disques durs virtuels pour les disques de données attaché, et un [modèle Resource Manager](../../azure-resource-manager/resource-group-overview.md) pour les nouveaux déploiements d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="65ad6-106">You then capture a generalized virtual hard disk (VHD) image for hello OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="65ad6-107">Cet article décrit en détail comment l’image avec hello Azure CLI 1.0 toocapture une machine virtuelle pour une machine virtuelle à l’aide de disques non managés.</span><span class="sxs-lookup"><span data-stu-id="65ad6-107">This article details how toocapture a VM image with hello Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="65ad6-108">Vous pouvez également [capturer une machine virtuelle à l’aide de disques de Azure gérés par hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65ad6-108">You can also [capture a VM using Azure Managed Disks with hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="65ad6-109">Disques gérés sont gérés par hello plateforme Azure et ne nécessitent pas de n’importe quel toostore préparation ou emplacement les.</span><span class="sxs-lookup"><span data-stu-id="65ad6-109">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="65ad6-110">Pour plus d’informations, voir la page [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Vue d’ensemble d’Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="65ad6-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="65ad6-111">toocreate machines virtuelles à l’aide de l’image hello, configurer des ressources réseau pour chaque nouvel ordinateur virtuel et utilisez hello toodeploy de modèle (un fichier JavaScript Object Notation ou JSON,) à partir de hello capture des images de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="65ad6-111">toocreate VMs using hello image, set up network resources for each new VM, and use hello template (a JavaScript Object Notation, or JSON, file) toodeploy it from hello captured VHD images.</span></span> <span data-ttu-id="65ad6-112">De cette façon, vous pouvez répliquer une machine virtuelle avec sa configuration logicielle actuel, toohello comme vous utilisez des images Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="65ad6-112">In this way, you can replicate a VM with its current software configuration, similar toohello way you use images in hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="65ad6-113">Si vous souhaitez toocreate une copie de votre VM Linux existant avec son état spécialisé pour la sauvegarde ou de débogage, consultez [créer une copie d’une machine virtuelle de Linux en cours d’exécution sur Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65ad6-113">If you want toocreate a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="65ad6-114">Et si vous souhaitez tooupload un VHD Linux à partir d’une machine virtuelle locale, consultez [télécharger et de créer un VM Linux à partir de l’image de disque personnalisé](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65ad6-114">And if you want tooupload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="65ad6-115">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="65ad6-115">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="65ad6-116">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="65ad6-116">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="65ad6-117">[Azure CLI 1.0](#before-you-begin) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="65ad6-117">[Azure CLI 1.0](#before-you-begin) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="65ad6-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="65ad6-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="65ad6-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="65ad6-119">Before you begin</span></span>
<span data-ttu-id="65ad6-120">Vérifiez que vous remplissez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="65ad6-120">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="65ad6-121">**Machine virtuelle Azure créé dans le modèle de déploiement du Gestionnaire de ressources hello** -si vous n’avez pas créé un VM Linux, vous pouvez utiliser hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [CLI d’Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ou [le Gestionnaire de ressources modèles](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="65ad6-121">**Azure VM created in hello Resource Manager deployment model** - If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="65ad6-122">Configurer hello machine virtuelle en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="65ad6-122">Configure hello VM as needed.</span></span> <span data-ttu-id="65ad6-123">Par exemple, [ajoutez des disques de données](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), appliquez des mises à jour et installez des applications.</span><span class="sxs-lookup"><span data-stu-id="65ad6-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="65ad6-124">**CLI Azure** -installation hello [CLI d’Azure](../../cli-install-nodejs.md) sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="65ad6-124">**Azure CLI** - Install hello [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-hello-azure-linux-agent"></a><span data-ttu-id="65ad6-125">Étape 1 : Supprimer l’agent de hello Azure Linux</span><span class="sxs-lookup"><span data-stu-id="65ad6-125">Step 1: Remove hello Azure Linux agent</span></span>
<span data-ttu-id="65ad6-126">Tout d’abord, exécutez hello **waagent** avec hello **deprovision** paramètre sur hello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="65ad6-126">First, run hello **waagent** command with hello **deprovision** parameter on hello Linux VM.</span></span> <span data-ttu-id="65ad6-127">Cette commande supprime les fichiers et les données toomake hello prêt pour la généralisation des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="65ad6-127">This command deletes files and data toomake hello VM ready for generalizing.</span></span> <span data-ttu-id="65ad6-128">Pour plus d’informations, consultez hello [guide de l’utilisateur Linux Agent Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65ad6-128">For details, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="65ad6-129">Se connecter tooyour VM Linux à l’aide d’un client SSH.</span><span class="sxs-lookup"><span data-stu-id="65ad6-129">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="65ad6-130">Dans la fenêtre SSH hello, tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="65ad6-130">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="65ad6-131">Uniquement, exécutez cette commande sur une machine virtuelle que vous avez l’intention de toocapture en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="65ad6-131">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="65ad6-132">Il ne garantit pas cette image hello est effacée de toutes les informations sensibles ou appropriée pour la redistribution.</span><span class="sxs-lookup"><span data-stu-id="65ad6-132">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="65ad6-133">Type **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="65ad6-133">Type **y** toocontinue.</span></span> <span data-ttu-id="65ad6-134">Vous pouvez ajouter hello **-force** paramètre tooavoid cette étape de confirmation.</span><span class="sxs-lookup"><span data-stu-id="65ad6-134">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="65ad6-135">Une fois la commande hello terminée, tapez **quitter**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-135">After hello command completes, type **exit**.</span></span> <span data-ttu-id="65ad6-136">Cette étape ferme le client SSH de hello.</span><span class="sxs-lookup"><span data-stu-id="65ad6-136">This step closes hello SSH client.</span></span>

## <a name="step-2-capture-hello-vm"></a><span data-ttu-id="65ad6-137">Étape 2 : Capturer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="65ad6-137">Step 2: Capture hello VM</span></span>
<span data-ttu-id="65ad6-138">Utilisez hello CLI d’Azure toogeneralize et capturer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="65ad6-138">Use hello Azure CLI toogeneralize and capture hello VM.</span></span> <span data-ttu-id="65ad6-139">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="65ad6-139">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="65ad6-140">Les noms de paramètre sont par exemple **myResourceGroup**, **myVnet** et **myVM**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="65ad6-141">À partir de votre ordinateur local, ouvrez hello CLI d’Azure et [connexion tooyour abonnement Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="65ad6-141">From your local computer, open hello Azure CLI and [login tooyour Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="65ad6-142">Assurez-vous que vous êtes en mode Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="65ad6-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="65ad6-143">Arrêtez hello machine virtuelle qui vous a déjà été annulé à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="65ad6-143">Shut down hello VM that you already deprovisioned by using hello following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="65ad6-144">Généraliser hello VM par hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="65ad6-144">Generalize hello VM with hello following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="65ad6-145">Exécutez maintenant hello **capture de machine virtuelle azure** commande, qui capture hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="65ad6-145">Now run hello **azure vm capture** command, which captures hello VM.</span></span> <span data-ttu-id="65ad6-146">Dans l’exemple suivant de hello, image hello disques durs virtuels sont capturés avec des noms commençant par **MyVHDNamePrefix**et hello **-t** option spécifie un modèle de toohello de chemin d’accès **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="65ad6-146">In hello following example, hello image VHDs are captured with names beginning with **MyVHDNamePrefix**, and hello **-t** option specifies a path toohello template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="65ad6-147">fichiers de disque dur virtuel d’image Hello obtient créés par défaut dans hello même compte de stockage hello d’ordinateur virtuel d’origine est utilisée.</span><span class="sxs-lookup"><span data-stu-id="65ad6-147">hello image VHD files get created by default in hello same storage account that hello original VM used.</span></span> <span data-ttu-id="65ad6-148">Hello d’utilisation *même compte de stockage* toostore hello disques durs virtuels pour de nouvelles machines virtuelles que vous créez à partir de l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="65ad6-148">Use hello *same storage account* toostore hello VHDs for any new VMs you create from hello image.</span></span> 

6. <span data-ttu-id="65ad6-149">emplacement de hello toofind d’une image capturée, modèle JSON hello ouvert dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="65ad6-149">toofind hello location of a captured image, open hello JSON template in a text editor.</span></span> <span data-ttu-id="65ad6-150">Bonjour **storageProfile**, recherche hello **uri** Hello **image** situé dans hello **système** conteneur.</span><span class="sxs-lookup"><span data-stu-id="65ad6-150">In hello **storageProfile**, find hello **uri** of hello **image** located in hello **system** container.</span></span> <span data-ttu-id="65ad6-151">Par exemple, hello URI d’image de disque hello du système d’exploitation est similaire trop`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="65ad6-151">For example, hello URI of hello OS disk image is similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="65ad6-152">Étape 3 : Créer une machine virtuelle à partir de l’image de hello capturée</span><span class="sxs-lookup"><span data-stu-id="65ad6-152">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="65ad6-153">Maintenant utiliser hello image avec un modèle de toocreate un VM Linux.</span><span class="sxs-lookup"><span data-stu-id="65ad6-153">Now use hello image with a template toocreate a Linux VM.</span></span> <span data-ttu-id="65ad6-154">Ces étapes vous indiquent comment toouse hello CLI d’Azure et hello du modèle de fichier JSON capturés toocreate hello machine virtuelle dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="65ad6-154">These steps show you how toouse hello Azure CLI and hello JSON file template you captured toocreate hello VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="65ad6-155">Créer des ressources réseau</span><span class="sxs-lookup"><span data-stu-id="65ad6-155">Create network resources</span></span>
<span data-ttu-id="65ad6-156">modèle de hello toouse, vous devez tooset un réseau virtuel et une carte réseau pour votre nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="65ad6-156">toouse hello template, you first need tooset up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="65ad6-157">Nous vous recommandons de que vous créez un groupe de ressources pour ces ressources dans un emplacement hello où est stockée votre image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="65ad6-157">We recommend you create a resource group for these resources in hello location where your VM image is stored.</span></span> <span data-ttu-id="65ad6-158">Exécuter des commandes similaires toohello suivant, en remplaçant les noms de vos ressources et un emplacement Azure approprié (« centralus » dans ces commandes) :</span><span class="sxs-lookup"><span data-stu-id="65ad6-158">Run commands similar toohello following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a><span data-ttu-id="65ad6-159">Obtenir hello Id de carte réseau de hello</span><span class="sxs-lookup"><span data-stu-id="65ad6-159">Get hello Id of hello NIC</span></span>
<span data-ttu-id="65ad6-160">toodeploy une machine virtuelle à partir de l’image hello à l’aide de hello JSON que vous avez enregistré lors de la capture, vous devez hello Id Hello carte réseau.</span><span class="sxs-lookup"><span data-stu-id="65ad6-160">toodeploy a VM from hello image by using hello JSON you saved during capture, you need hello Id of hello NIC.</span></span> <span data-ttu-id="65ad6-161">L’obtenir en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="65ad6-161">Obtain it by running hello following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="65ad6-162">Hello **Id** Bonjour sortie est similaire trop`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="65ad6-162">hello **Id** in hello output is similar too`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="65ad6-163">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="65ad6-163">Create a VM</span></span>
<span data-ttu-id="65ad6-164">Maintenant suivante d’exécution hello commande toocreate votre machine virtuelle à partir de hello capturées image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="65ad6-164">Now run hello following command toocreate your VM from hello captured VM image.</span></span> <span data-ttu-id="65ad6-165">Hello d’utilisation **-f** JSON de modèle de toohello de chemin d’accès hello de paramètre toospecify fichier que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="65ad6-165">Use hello **-f** parameter toospecify hello path toohello template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="65ad6-166">Dans la sortie de la commande hello, vous sont demandée toosupply un nouveau nom d’ordinateur virtuel, nom d’utilisateur admin hello et un mot de passe et hello Id Hello carte réseau que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="65ad6-166">In hello command output, you are prompted toosupply a new VM name, hello admin user name and password, and hello Id of hello NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="65ad6-167">Hello suivant l’exemple montre ce que vous voyez pour un déploiement réussi :</span><span class="sxs-lookup"><span data-stu-id="65ad6-167">hello following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
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

### <a name="verify-hello-deployment"></a><span data-ttu-id="65ad6-168">Vérifier le déploiement de hello</span><span class="sxs-lookup"><span data-stu-id="65ad6-168">Verify hello deployment</span></span>
<span data-ttu-id="65ad6-169">Maintenant SSH toohello machine virtuelle vous avez créé le déploiement de hello tooverify et commencer à utiliser hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="65ad6-169">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="65ad6-170">tooconnect via SSH, Rechercher adresse IP hello hello machine virtuelle que vous avez créé en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="65ad6-170">tooconnect via SSH, find hello IP address of hello VM you created by running hello following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="65ad6-171">adresse IP publique de Hello est répertorié dans la sortie de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="65ad6-171">hello public IP address is listed in hello command output.</span></span> <span data-ttu-id="65ad6-172">Par défaut, vous vous connectez toohello VM Linux par SSH sur le port 22.</span><span class="sxs-lookup"><span data-stu-id="65ad6-172">By default you connect toohello Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="65ad6-173">Créer des machines virtuelles supplémentaires</span><span class="sxs-lookup"><span data-stu-id="65ad6-173">Create additional VMs</span></span>
<span data-ttu-id="65ad6-174">Hello d’utilisation capturées toodeploy image et le modèle à l’aide des étapes de hello Bonjour précédant la section des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="65ad6-174">Use hello captured image and template toodeploy additional VMs using hello steps in hello preceding section.</span></span> <span data-ttu-id="65ad6-175">Autres options de toocreate machines virtuelles à partir de l’image de hello inclure à l’aide d’un modèle de démarrage rapide ou en cours d’exécution hello **créer de machine virtuelle azure** commande.</span><span class="sxs-lookup"><span data-stu-id="65ad6-175">Other options toocreate VMs from hello image include using a quickstart template or running hello **azure vm create** command.</span></span>

### <a name="use-hello-captured-template"></a><span data-ttu-id="65ad6-176">Utiliser le modèle capturé hello</span><span class="sxs-lookup"><span data-stu-id="65ad6-176">Use hello captured template</span></span>
<span data-ttu-id="65ad6-177">toouse hello l’image capturée et modèle, suivez ces étapes (détaillés dans la précédente section de hello) :</span><span class="sxs-lookup"><span data-stu-id="65ad6-177">toouse hello captured image and template, follow these steps (detailed in hello preceding section):</span></span>

* <span data-ttu-id="65ad6-178">Assurez-vous que votre image de machine virtuelle est Bonjour même compte de stockage qui héberge votre disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="65ad6-178">Ensure that your VM image is in hello same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="65ad6-179">Copiez le fichier JSON de modèle hello et spécifiez un nom unique pour le disque de système d’exploitation hello de disque dur virtuel hello nouvelle la machine virtuelle (ou les disques durs virtuels).</span><span class="sxs-lookup"><span data-stu-id="65ad6-179">Copy hello template JSON file and specify a unique name for hello OS disk of hello new VM's VHD (or VHDs).</span></span> <span data-ttu-id="65ad6-180">Par exemple, dans hello **storageProfile**, sous **vhd**, dans **uri**, spécifiez un nom unique pour hello **osDisk** disque dur virtuel similaire trop`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="65ad6-180">For example, in hello **storageProfile**, under **vhd**, in **uri**, specify a unique name for hello **osDisk** VHD, similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="65ad6-181">Créez une carte réseau soit Bonjour même ou à un autre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="65ad6-181">Create a NIC in either hello same or a different virtual network.</span></span>
* <span data-ttu-id="65ad6-182">Fichier JSON de modèle hello modifié, créez un déploiement du groupe de ressources hello dans lequel vous configurez un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="65ad6-182">Using hello modified template JSON file, create a deployment in hello resource group in which you set up hello virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="65ad6-183">Utilisation d’un modèle de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="65ad6-183">Use a quickstart template</span></span>
<span data-ttu-id="65ad6-184">Si vous souhaitez réseau hello configuré automatiquement lorsque vous créez une machine virtuelle à partir de l’image de hello, vous pouvez spécifier ces ressources dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="65ad6-184">If you want hello network set up automatically when you create a VM from hello image, you can specify those resources in a template.</span></span> <span data-ttu-id="65ad6-185">Par exemple, consultez hello [101-vm-de-utilisateur-image modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="65ad6-185">For example, see hello [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="65ad6-186">Ce modèle crée une machine virtuelle à partir de votre image personnalisée et hello nécessaire réseau virtuel, adresse IP publique et ressources de la carte réseau.</span><span class="sxs-lookup"><span data-stu-id="65ad6-186">This template creates a VM from your custom image and hello necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="65ad6-187">Pour une procédure pas à pas de l’utilisation du modèle de hello Bonjour portail Azure, consultez [comment toocreate un ordinateur virtuel à partir d’une image personnalisée à l’aide d’un modèle de gestionnaire de ressources](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="65ad6-187">For a walkthrough of using hello template in hello Azure portal, see [How toocreate a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-hello-azure-vm-create-command"></a><span data-ttu-id="65ad6-188">Utilisez hello azure vm Créer commande</span><span class="sxs-lookup"><span data-stu-id="65ad6-188">Use hello azure vm create command</span></span>
<span data-ttu-id="65ad6-189">Il est généralement plus simple toouse un toocreate de modèle de gestionnaire de ressources une machine virtuelle à partir de l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="65ad6-189">Usually it's easiest toouse a Resource Manager template toocreate a VM from hello image.</span></span> <span data-ttu-id="65ad6-190">Toutefois, vous pouvez créer hello VM *impérative* à l’aide de hello **créer de machine virtuelle azure** avec hello **-Q** (**--urn de l’image**) paramètre .</span><span class="sxs-lookup"><span data-stu-id="65ad6-190">However, you can create hello VM *imperatively* by using hello **azure vm create** command with hello **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="65ad6-191">Si vous utilisez cette méthode, vous passez également hello **-d** (**--système d’exploitation-disque-vhd**) emplacement de hello toospecify paramètre du fichier .vhd de hello du système d’exploitation pour hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="65ad6-191">If you use this method, you also pass hello **-d** (**--os-disk-vhd**) parameter toospecify hello location of hello OS .vhd file for hello new VM.</span></span> <span data-ttu-id="65ad6-192">Ce fichier doit être dans le conteneur de disques durs virtuels hello hello du compte de stockage où se trouve le fichier de disque dur virtuel d’image hello.</span><span class="sxs-lookup"><span data-stu-id="65ad6-192">This file must be in hello vhds container of hello storage account where hello image VHD file is stored.</span></span> <span data-ttu-id="65ad6-193">Hello commande copies hello de disque dur virtuel pour hello nouvelle machine virtuelle automatiquement toohello **disques durs virtuels** conteneur.</span><span class="sxs-lookup"><span data-stu-id="65ad6-193">hello command copies hello VHD for hello new VM automatically toohello **vhds** container.</span></span>

<span data-ttu-id="65ad6-194">Avant d’exécuter **créer de machine virtuelle azure** avec l’image hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="65ad6-194">Before running **azure vm create** with hello image, complete hello following steps:</span></span>

1. <span data-ttu-id="65ad6-195">Créer un groupe de ressources, ou identifier un groupe de ressources pour le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="65ad6-195">Create a resource group, or identify an existing resource group for hello deployment.</span></span>
2. <span data-ttu-id="65ad6-196">Créer un public ressource d’adresse IP et une ressource de la carte réseau pour hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="65ad6-196">Create a public IP address resource and a NIC resource for hello new VM.</span></span> <span data-ttu-id="65ad6-197">Pour les étapes toocreate un réseau virtuel, adresse IP publique et les cartes réseau à l’aide de hello CLI, consultez plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="65ad6-197">For steps toocreate a virtual network, public IP address, and NIC by using hello CLI, see earlier in this article.</span></span> <span data-ttu-id="65ad6-198">(**créer de machine virtuelle azure** peut également créer une carte réseau, mais vous devez toopass des paramètres supplémentaires pour un réseau virtuel et le sous-réseau.)</span><span class="sxs-lookup"><span data-stu-id="65ad6-198">(**azure vm create** can also create a NIC, but you need toopass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="65ad6-199">Exécutez ensuite une commande qui transmet des URI le fichier de disque dur virtuel du système d’exploitation de tooboth hello et hello existant d’image.</span><span class="sxs-lookup"><span data-stu-id="65ad6-199">Then run a command that passes URIs tooboth hello new OS VHD file and hello existing image.</span></span> <span data-ttu-id="65ad6-200">Dans cet exemple, une taille Standard_A1 VM est créé dans la région est des États-Unis hello.</span><span class="sxs-lookup"><span data-stu-id="65ad6-200">In this example, a size Standard_A1 VM is created in hello East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="65ad6-201">Pour obtenir d’autres options de commande supplémentaires, exécutez `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="65ad6-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65ad6-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65ad6-202">Next steps</span></span>
<span data-ttu-id="65ad6-203">toomanage vos machines virtuelles avec hello CLI, consultez tâches hello [déployer et gérer des ordinateurs virtuels à l’aide de modèles Azure Resource Manager et hello CLI d’Azure](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="65ad6-203">toomanage your VMs with hello CLI, see hello tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

