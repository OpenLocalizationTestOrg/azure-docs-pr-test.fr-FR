---
title: "aaaCapture une image d’un VM Linux | Documents Microsoft"
description: "Découvrez comment toocapture une image d’une basés sur Linux Azure virtual machine (VM) créé avec le modèle de déploiement classique hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="1c8c7-103">Comment toocapture une machine virtuelle de Linux classique en tant qu’image</span><span class="sxs-lookup"><span data-stu-id="1c8c7-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1c8c7-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1c8c7-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1c8c7-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="1c8c7-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="1c8c7-107">Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c8c7-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1c8c7-108">Cet article vous explique comment toocapture une classique Azure machine virtuelle (VM) exécutant Linux en tant qu’une image toocreate autres machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="1c8c7-109">Cette image comprend le disque du système d’exploitation hello et des disques de données attachée toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="1c8c7-110">Il n’inclut pas la configuration réseau, vous devez tooconfigure que lorsque vous créez hello autre machine virtuelle à partir de l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="1c8c7-111">Magasins Azure hello image sous **Images**, ainsi que toutes les images que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="1c8c7-112">Pour plus d’informations sur les images, consultez l’article [À propos des images de machine virtuelle dans Azure][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="1c8c7-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1c8c7-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="1c8c7-113">Before you begin</span></span>
<span data-ttu-id="1c8c7-114">Ces étapes supposent que vous avez déjà créé une machine virtuelle de Azure à l’aide du modèle de déploiement classique hello et le système d’exploitation de hello configurés, y compris l’attachement des disques de données.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="1c8c7-115">Si vous avez besoin toocreate une machine virtuelle, lisez [comment tooCreate une Machine virtuelle Linux][How tooCreate a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="1c8c7-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="1c8c7-116">Capture de machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="1c8c7-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="1c8c7-117">[Se connecter toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) à l’aide d’un client SSH de votre choix.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="1c8c7-118">Dans la fenêtre SSH hello, tapez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="1c8c7-119">Hello de sortie à partir de `waagent` peut varier légèrement en fonction de la version de hello de cet utilitaire :</span><span class="sxs-lookup"><span data-stu-id="1c8c7-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="1c8c7-120">Hello précédente commande tente de système de hello tooclean et adapté à la préparation.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="1c8c7-121">Cette opération effectue hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c8c7-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="1c8c7-122">Supprime les clés d’hôte SSH (si Provisioning.RegenerateSshHostKeyPair est « y » dans le fichier de configuration hello)</span><span class="sxs-lookup"><span data-stu-id="1c8c7-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="1c8c7-123">efface la configuration de Nameserver dans /etc/resolv.conf ;</span><span class="sxs-lookup"><span data-stu-id="1c8c7-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="1c8c7-124">Supprime hello `root` mot de passe utilisateur à partir / etc/shadow (si Provisioning.DeleteRootPassword est « y » dans le fichier de configuration hello)</span><span class="sxs-lookup"><span data-stu-id="1c8c7-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="1c8c7-125">supprime les baux du client DHCP mis en cache ;</span><span class="sxs-lookup"><span data-stu-id="1c8c7-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="1c8c7-126">Réinitialise héberge nom toolocalhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="1c8c7-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="1c8c7-127">Supprime hello dernier compte d’utilisateur configuré (obtenu à partir de /var/lib/waagent) **et les données associées**.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="1c8c7-128">Mise hors service supprime les fichiers et données trop « généralisent » hello image.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="1c8c7-129">Uniquement, exécutez cette commande sur une machine virtuelle que vous avez l’intention toocapture comme un nouveau modèle d’image.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="1c8c7-130">Il ne garantit pas cette image hello est effacée de toutes les informations sensibles ou adaptée aux parties toothird de redistribution.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="1c8c7-131">Type **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-131">Type **y** toocontinue.</span></span> <span data-ttu-id="1c8c7-132">Vous pouvez ajouter hello `-force` paramètre tooavoid cette étape de confirmation.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="1c8c7-133">Type **Exit** client SSH de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1c8c7-134">Hello restantes étapes supposent que vous avez déjà [installé hello CLI d’Azure](../../../cli-install-nodejs.md) sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="1c8c7-135">Tous les hello comme suit peut également être effectué dans hello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c8c7-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="1c8c7-136">À partir de votre ordinateur client, ouvrez CLI d’Azure et de connexion tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="1c8c7-137">Pour plus d’informations, consultez [connecter tooan abonnement Azure à partir de hello CLI d’Azure](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="1c8c7-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="1c8c7-138">Bonjour portail Azure, ouvrez une session dans toohello portal.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="1c8c7-139">Assurez-vous que vous êtes en mode de gestion des services :</span><span class="sxs-lookup"><span data-stu-id="1c8c7-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="1c8c7-140">Arrêtez hello machine virtuelle qui est déjà annulé.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="1c8c7-141">Hello exemple suivant arrête hello ordinateur virtuel nommé `myVM`:</span><span class="sxs-lookup"><span data-stu-id="1c8c7-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="1c8c7-142">Si nécessaire, vous pouvez afficher une liste hello tous les ordinateurs virtuels créés dans votre abonnement à l’aide de`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="1c8c7-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="1c8c7-143">Si vous utilisez hello portail Azure, sélectionnez hello machine virtuelle et cliquez sur **arrêter** arrêter hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="1c8c7-144">Lorsque hello machine virtuelle est arrêtée, capturez l’image du hello.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="1c8c7-145">Hello suivant capture de l’exemple hello ordinateur virtuel nommé `myVM` et crée une image généralisée nommée `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="1c8c7-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="1c8c7-146">Hello `-t` sous-commande suppressions hello ordinateur virtuel d’origine.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c8c7-147">Bonjour portail Azure, vous pouvez capturer une image en sélectionnant **Image** à partir du menu du hub hello.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="1c8c7-148">Vous devez hello toosupply informations pour l’image de hello suivantes : nom, groupe de ressources, l’emplacement, le type de système d’exploitation et le chemin d’accès de stockage blob.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="1c8c7-149">Hello nouvelle image est désormais disponible dans la liste de hello d’images qui peuvent être utilisées tooconfigure tout nouvel ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="1c8c7-150">Vous pouvez l’afficher avec la commande hello :</span><span class="sxs-lookup"><span data-stu-id="1c8c7-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="1c8c7-151">Sur hello [portail Azure](http://portal.azure.com), hello nouvelle image apparaît dans hello **images de machine virtuelle (classique)** qui appartient toohello **de calcul** services.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="1c8c7-152">Vous pouvez accéder aux **images de machine virtuelle (classique)** en cliquant sur _davantage de services_ bas hello hello Azure service liste, puis en consultant Bonjour **de calcul** services.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![Capture d’image réussie](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="1c8c7-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1c8c7-154">Next steps</span></span>
<span data-ttu-id="1c8c7-155">image de Hello est prêt toobe utilisé toocreate machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="1c8c7-156">Vous pouvez utiliser la commande CLI d’Azure de hello `azure vm create` et nom de l’image hello approvisionnement vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="1c8c7-157">Pour plus d’informations, consultez [Using hello CLI d’Azure avec le modèle de déploiement classique](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="1c8c7-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="1c8c7-158">Vous pouvez également utiliser hello [portail Azure](http://portal.azure.com) toocreate une machine virtuelle personnalisé à l’aide de hello **Image** (méthode) et en sélectionnant hello de l’image que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="1c8c7-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="1c8c7-159">Pour plus d’informations, consultez [comment tooCreate un ordinateur virtuel personnalisé][How tooCreate a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="1c8c7-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="1c8c7-160">**Consultez également :**[Guide d’utilisateur de l’agent Linux Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1c8c7-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
