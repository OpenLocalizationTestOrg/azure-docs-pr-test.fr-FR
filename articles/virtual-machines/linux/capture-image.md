---
title: "aaaCapture une image d’un VM Linux dans Azure à l’aide de CLI 2.0 | Documents Microsoft"
description: "Capturer une image d’un toouse de machine virtuelle Azure pour les déploiements de mass à l’aide de hello Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="57e3d-103">Comment toocreate une image d’un ordinateur virtuel ou un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="57e3d-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="57e3d-104">toocreate plusieurs copies d’un ordinateur virtuel (VM) toouse dans Azure, capturer une image de machine virtuelle de hello ou hello du disque dur virtuel du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="57e3d-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="57e3d-105">toocreate une image, vous devez supprimer les informations de compte personnel qui le rend plus sûre toodeploy plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="57e3d-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="57e3d-106">Bonjour vous annuler le déploiement d’un ordinateur virtuel existant comme suit, désallouer et créer une image.</span><span class="sxs-lookup"><span data-stu-id="57e3d-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="57e3d-107">Vous pouvez utiliser cette image de toocreate machines virtuelles sur n’importe quel groupe de ressources au sein de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="57e3d-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="57e3d-108">Si vous souhaitez toocreate une copie de votre VM Linux existante pour la sauvegarde ou de débogage, ou téléchargez un VHD Linux spécialisées à partir d’une machine virtuelle locale, consultez [télécharger et créer un VM Linux à partir de l’image de disque personnalisé](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="57e3d-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="57e3d-109">Vous pouvez également utiliser **GARNITURE** toocreate votre configuration personnalisée.</span><span class="sxs-lookup"><span data-stu-id="57e3d-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="57e3d-110">Pour plus d’informations sur l’utilisation du programme de compression, consultez [comment une machine virtuelle Linux toouse GARNITURE toocreate images dans Azure](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="57e3d-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="57e3d-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="57e3d-111">Before you begin</span></span>
<span data-ttu-id="57e3d-112">Vérifiez que vous remplissez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="57e3d-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="57e3d-113">Vous avez besoin d’une machine virtuelle de Azure créé dans le modèle de déploiement hello Gestionnaire de ressources à l’aide de disques gérés.</span><span class="sxs-lookup"><span data-stu-id="57e3d-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="57e3d-114">Si vous n’avez pas créé un VM Linux, vous pouvez utiliser hello [portal](quick-create-portal.md), hello [CLI d’Azure](quick-create-cli.md), ou [modèles Resource Manager](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="57e3d-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="57e3d-115">Configurer hello machine virtuelle en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="57e3d-115">Configure hello VM as needed.</span></span> <span data-ttu-id="57e3d-116">Par exemple, [ajoutez des disques de données](add-disk.md), appliquez des mises à jour et installez des applications.</span><span class="sxs-lookup"><span data-stu-id="57e3d-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="57e3d-117">Vous devez également toohave hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et être connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="57e3d-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="57e3d-118">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="57e3d-118">Quick commands</span></span>

<span data-ttu-id="57e3d-119">Pour une version simplifiée de cette rubrique, pour les tests, l’évaluation ou en savoir plus sur les machines virtuelles dans Azure, consultez [créer une image personnalisée d’une machine virtuelle de Azure à l’aide de hello CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="57e3d-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="57e3d-120">Étape 1 : Annuler le déploiement hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="57e3d-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="57e3d-121">Vous annulez le déploiement hello machine virtuelle, à l’aide des données de l’agent de machine virtuelle Azure hello et toodelete les fichiers d’ordinateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="57e3d-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="57e3d-122">Hello d’utilisation `waagent` avec hello *-deprovision + utilisateur* paramètre sur votre source de Linux VM.</span><span class="sxs-lookup"><span data-stu-id="57e3d-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="57e3d-123">Pour plus d’informations, consultez hello [guide de l’utilisateur Linux Agent Azure](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="57e3d-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="57e3d-124">Se connecter tooyour VM Linux à l’aide d’un client SSH.</span><span class="sxs-lookup"><span data-stu-id="57e3d-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="57e3d-125">Dans la fenêtre SSH hello, tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="57e3d-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="57e3d-126">Uniquement, exécutez cette commande sur une machine virtuelle que vous avez l’intention de toocapture en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="57e3d-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="57e3d-127">Il ne garantit pas cette image hello est effacée de toutes les informations sensibles ou appropriée pour la redistribution.</span><span class="sxs-lookup"><span data-stu-id="57e3d-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="57e3d-128">Hello *+ utilisateur* paramètre supprime également le dernier compte d’utilisateur configuré hello.</span><span class="sxs-lookup"><span data-stu-id="57e3d-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="57e3d-129">Si vous souhaitez que les informations d’identification de compte tookeep Bonjour machine virtuelle, utilisez simplement *-deprovision* compte d’utilisateur tooleave hello en place.</span><span class="sxs-lookup"><span data-stu-id="57e3d-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="57e3d-130">Type **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="57e3d-130">Type **y** toocontinue.</span></span> <span data-ttu-id="57e3d-131">Vous pouvez ajouter hello **-force** paramètre tooavoid cette étape de confirmation.</span><span class="sxs-lookup"><span data-stu-id="57e3d-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="57e3d-132">Une fois la commande hello terminée, tapez **quitter**.</span><span class="sxs-lookup"><span data-stu-id="57e3d-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="57e3d-133">Cette étape ferme le client SSH de hello.</span><span class="sxs-lookup"><span data-stu-id="57e3d-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="57e3d-134">Étape 2 : Créer une image de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="57e3d-134">Step 2: Create VM image</span></span>
<span data-ttu-id="57e3d-135">Utilisez Bonjour Azure CLI 2.0 toomark Bonjour machine virtuelle comme généralisé et capturer l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="57e3d-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="57e3d-136">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="57e3d-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="57e3d-137">Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="57e3d-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="57e3d-138">Désallouer hello machine virtuelle qui vous a été annulé avec [az vm désallouer](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="57e3d-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="57e3d-139">exemple Hello désalloue hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="57e3d-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="57e3d-140">Hello de marque machine virtuelle comme généralisée avec [az vm généraliser](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="57e3d-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="57e3d-141">Hello suivants exemple marques hello hello VM nommée *myVM* dans le groupe de ressources hello nommé *myResourceGroup* comme généralisé :</span><span class="sxs-lookup"><span data-stu-id="57e3d-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="57e3d-142">Créez une image de la ressource d’ordinateur virtuel hello avec [az image création](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="57e3d-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="57e3d-143">Hello exemple suivant crée une image nommée *myImage* dans le groupe de ressources hello nommé *myResourceGroup* à l’aide de la ressource de machine virtuelle hello nommé *myVM*:</span><span class="sxs-lookup"><span data-stu-id="57e3d-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="57e3d-144">Hello image est créée dans hello même groupe de ressources que votre ordinateur virtuel source.</span><span class="sxs-lookup"><span data-stu-id="57e3d-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="57e3d-145">Vous pouvez créer des machines virtuelles dans n’importe quel groupe de ressources de votre abonnement à partir de cette image.</span><span class="sxs-lookup"><span data-stu-id="57e3d-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="57e3d-146">À partir d’un point de vue de gestion, vous pouvez toocreate un groupe de ressources spécifique pour vos ressources d’ordinateurs virtuels et des images.</span><span class="sxs-lookup"><span data-stu-id="57e3d-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="57e3d-147">Étape 3 : Créer une machine virtuelle à partir de l’image de hello capturée</span><span class="sxs-lookup"><span data-stu-id="57e3d-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="57e3d-148">Créer une machine virtuelle à l’aide d’image hello vous avez créé avec [az vm créer](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="57e3d-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="57e3d-149">Hello exemple suivant crée un ordinateur virtuel nommé *myVMDeployed* à partir de l’image hello nommée *myImage*:</span><span class="sxs-lookup"><span data-stu-id="57e3d-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="57e3d-150">Création de hello machine virtuelle dans un autre groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="57e3d-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="57e3d-151">Vous pouvez créer des machines virtuelles à partir d’une image dans n’importe quel groupe de ressources de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="57e3d-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="57e3d-152">toocreate une machine virtuelle dans un autre groupe de ressources à l’image de hello, spécifiez l’ID tooyour image hello ressource complète.</span><span class="sxs-lookup"><span data-stu-id="57e3d-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="57e3d-153">Utilisez [liste d’images az](/cli/azure/image#list) tooview une liste d’images.</span><span class="sxs-lookup"><span data-stu-id="57e3d-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="57e3d-154">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="57e3d-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="57e3d-155">Hello exemple suivant utilise [az vm créer](/cli/azure/vm#create) toocreate une machine virtuelle dans un autre groupe de ressources à l’image source de hello en spécifiant l’ID de ressource d’image hello :</span><span class="sxs-lookup"><span data-stu-id="57e3d-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="57e3d-156">Étape 4 : Vérifier le déploiement de hello</span><span class="sxs-lookup"><span data-stu-id="57e3d-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="57e3d-157">Maintenant SSH toohello machine virtuelle vous avez créé le déploiement de hello tooverify et commencer à utiliser hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="57e3d-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="57e3d-158">tooconnect via SSH, rechercher l’adresse IP de hello ou nom de domaine complet de votre machine virtuelle avec [afficher de machine virtuelle az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="57e3d-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="57e3d-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57e3d-159">Next steps</span></span>
<span data-ttu-id="57e3d-160">Vous pouvez créer plusieurs machines virtuelles à partir de votre image de machine virtuelle source.</span><span class="sxs-lookup"><span data-stu-id="57e3d-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="57e3d-161">Si vous avez besoin d’image de tooyour toomake des modifications :</span><span class="sxs-lookup"><span data-stu-id="57e3d-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="57e3d-162">Créez une machine virtuelle à partir de votre image.</span><span class="sxs-lookup"><span data-stu-id="57e3d-162">Create a VM from your image.</span></span>
- <span data-ttu-id="57e3d-163">Apportez les mises à jour ou modifications de configuration requises.</span><span class="sxs-lookup"><span data-stu-id="57e3d-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="57e3d-164">Suivez hello les étapes à nouveau toodeprovision, désallouer, généraliser et créer une image.</span><span class="sxs-lookup"><span data-stu-id="57e3d-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="57e3d-165">Utilisez cette nouvelle image pour les déploiements futurs.</span><span class="sxs-lookup"><span data-stu-id="57e3d-165">Use this new image for future deployments.</span></span> <span data-ttu-id="57e3d-166">Si vous le souhaitez, supprimez l’image d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="57e3d-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="57e3d-167">Pour plus d’informations sur la gestion de vos machines virtuelles avec hello CLI, consultez [Azure CLI 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="57e3d-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
