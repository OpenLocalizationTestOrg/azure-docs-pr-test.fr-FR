---
title: "stockage de fichier Azure sur les machines virtuelles Linux à l’aide de SMB d’aaaMount | Documents Microsoft"
description: "Comment toomount stockage de fichier Azure sur les machines virtuelles Linux à l’aide de SMB avec hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="cd160-103">Monter le stockage de fichiers Azure sur les machines virtuelles Linux à l’aide de SMB</span><span class="sxs-lookup"><span data-stu-id="cd160-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="cd160-104">Cet article vous explique comment tooutilize hello service de stockage Azure sur un VM Linux à l’aide d’un serveur SMB montage avec hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="cd160-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="cd160-105">Stockage de fichiers Azure offre des partages de fichiers dans le cloud hello à l’aide du protocole SMB standard de hello.</span><span class="sxs-lookup"><span data-stu-id="cd160-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="cd160-106">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd160-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="cd160-107">spécifications de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="cd160-107">hello requirements are:</span></span>

- [<span data-ttu-id="cd160-108">un compte Azure</span><span class="sxs-lookup"><span data-stu-id="cd160-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="cd160-109">des fichiers de clés SSH publiques et privées</span><span class="sxs-lookup"><span data-stu-id="cd160-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="cd160-110">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="cd160-110">Quick Commands</span></span>

* <span data-ttu-id="cd160-111">Un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cd160-111">A resource group</span></span>
* <span data-ttu-id="cd160-112">Un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="cd160-112">An Azure virtual network</span></span>
* <span data-ttu-id="cd160-113">Un groupe de sécurité réseau avec une connexion SSH entrante.</span><span class="sxs-lookup"><span data-stu-id="cd160-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="cd160-114">Un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="cd160-114">A subnet</span></span>
* <span data-ttu-id="cd160-115">Un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cd160-115">An Azure storage account</span></span>
* <span data-ttu-id="cd160-116">Des clés de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cd160-116">Azure storage account keys</span></span>
* <span data-ttu-id="cd160-117">Un partage de stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="cd160-117">An Azure File storage share</span></span>
* <span data-ttu-id="cd160-118">Une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="cd160-118">A Linux VM</span></span>

<span data-ttu-id="cd160-119">Remplacez les exemples par vos propres paramètres.</span><span class="sxs-lookup"><span data-stu-id="cd160-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="cd160-120">Créez un répertoire de montage local de hello</span><span class="sxs-lookup"><span data-stu-id="cd160-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="cd160-121">Monter le point de montage hello fichier stockage SMB partage toohello</span><span class="sxs-lookup"><span data-stu-id="cd160-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="cd160-122">Conserver le montage de hello après un redémarrage</span><span class="sxs-lookup"><span data-stu-id="cd160-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="cd160-123">toodo, ajoutez hello suivant ligne toohello `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="cd160-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="cd160-124">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="cd160-124">Detailed walkthrough</span></span>

<span data-ttu-id="cd160-125">Stockage de fichiers offre des partages de fichiers dans le cloud de hello qui utilisent le protocole SMB standard de hello.</span><span class="sxs-lookup"><span data-stu-id="cd160-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="cd160-126">Avec la version la plus récente hello de stockage de fichiers, vous pouvez également monter un partage de fichiers à partir de n’importe quel système d’exploitation qui prend en charge SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="cd160-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="cd160-127">Lorsque vous utilisez un montage SMB sur Linux, vous obtenez sauvegardes tooa robustes et permanente d’archivage emplacement de stockage qui est pris en charge par un contrat SLA.</span><span class="sxs-lookup"><span data-stu-id="cd160-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="cd160-128">Déplacement des fichiers à partir d’un montage SMB tooan machine virtuelle qui est hébergé sur le stockage de fichiers est qu'un excellent moyen toodebug se connecte.</span><span class="sxs-lookup"><span data-stu-id="cd160-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="cd160-129">C’est parce que hello partage SMB même peut être monté localement tooyour Mac, Linux ou Windows station de travail.</span><span class="sxs-lookup"><span data-stu-id="cd160-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="cd160-130">SMB n’est pas la meilleure solution pour Linux de diffusion en continu de hello ou de journaux des applications en temps réel, car hello protocole SMB n’est pas généré toohandle ces droits journalisation lourde.</span><span class="sxs-lookup"><span data-stu-id="cd160-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="cd160-131">Un outil de couche de journalisation unifié et dédié comme Fluentd resprésente un meilleur choix que SMB pour collecter la sortie de journalisation d’applications et Linux.</span><span class="sxs-lookup"><span data-stu-id="cd160-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="cd160-132">Pour cette procédure pas à pas détaillées, nous créer les conditions préalables à hello nécessaires toofirst création du partage de stockage de fichier hello et puis montez via SMB sur un VM Linux.</span><span class="sxs-lookup"><span data-stu-id="cd160-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="cd160-133">Créer un groupe de ressources avec [création de groupe de az](/cli/azure/group#create) partage de fichiers toohold hello.</span><span class="sxs-lookup"><span data-stu-id="cd160-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="cd160-134">toocreate un groupe de ressources nommé `myResourceGroup` Bonjour emplacement de « Ouest des États-Unis », utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cd160-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="cd160-135">Créer un compte Azure storage avec [créer de compte de stockage az](/cli/azure/storage/account#create) toostore hello fichiers réels.</span><span class="sxs-lookup"><span data-stu-id="cd160-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="cd160-136">toocreate un compte de stockage nommé mystorageaccount en utilisant le stockage hello Standard_LRS référence (SKU), hello d’utiliser l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cd160-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="cd160-137">Afficher les clés de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="cd160-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="cd160-138">Lorsque vous créez un compte de stockage, les clés de compte hello sont créés dans les paires afin qu’ils peuvent être pivotées sans aucune interruption de service.</span><span class="sxs-lookup"><span data-stu-id="cd160-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="cd160-139">Lorsque vous basculez toohello deuxième clé de la paire de hello, vous créez une nouvelle paire de clés.</span><span class="sxs-lookup"><span data-stu-id="cd160-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="cd160-140">Nouvelles clés de compte de stockage sont toujours créés par paires, s’assurer que vous disposez toujours au moins un tooswitch prêt clé stockage inutilisés compte à.</span><span class="sxs-lookup"><span data-stu-id="cd160-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="cd160-141">Afficher les clés de compte de stockage hello avec hello [liste de clés de compte de stockage az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="cd160-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="cd160-142">Hello clés de compte de stockage pour hello nommé `mystorageaccount` sont répertoriées dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cd160-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="cd160-143">tooextract une clé unique, utiliser hello `--query` indicateur.</span><span class="sxs-lookup"><span data-stu-id="cd160-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="cd160-144">première clé de hello extrait Hello suivant (`[0]`) :</span><span class="sxs-lookup"><span data-stu-id="cd160-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="cd160-145">Création du partage de stockage de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="cd160-145">Create hello File storage share.</span></span>

    <span data-ttu-id="cd160-146">partage de fichiers de stockage Hello contient hello partage SMB avec [créer de partage de stockage az](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="cd160-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="cd160-147">quota de Hello est toujours exprimée en gigaoctets (Go).</span><span class="sxs-lookup"><span data-stu-id="cd160-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="cd160-148">Passez l’une des clés de hello de hello précédent `az storage account keys list` commande.</span><span class="sxs-lookup"><span data-stu-id="cd160-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="cd160-149">Créer un partage nommé mystorageshare avec un quota de 10 Go à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cd160-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="cd160-150">Créez un répertoire de point de montage.</span><span class="sxs-lookup"><span data-stu-id="cd160-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="cd160-151">Créer un répertoire local dans hello toomount hello Linux fichier système partage SMB.</span><span class="sxs-lookup"><span data-stu-id="cd160-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="cd160-152">Rien écrire ou lire à partir du répertoire de montage local hello est transféré toohello partage SMB qui est hébergé sur le stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="cd160-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="cd160-153">toocreate un répertoire local sur/mnt/mymountdirectory, hello d’utiliser l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cd160-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="cd160-154">Montez le répertoire local du toohello partage SMB hello.</span><span class="sxs-lookup"><span data-stu-id="cd160-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="cd160-155">Fournissez votre propre nom d’utilisateur du compte de stockage et de la clé de compte de stockage pour les informations d’identification de montage hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cd160-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="cd160-156">Hello SMB de montage de redémarrages de persistance.</span><span class="sxs-lookup"><span data-stu-id="cd160-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="cd160-157">Lorsque vous redémarrez hello Linux VM, hello monté partage SMB est démonté lors de l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="cd160-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="cd160-158">hello tooremount partage SMB sur le démarrage, ajouter une ligne de toohello/etc/fstab Linux.</span><span class="sxs-lookup"><span data-stu-id="cd160-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="cd160-159">Linux utilise hello fstab fichier toolist hello systèmes de fichiers qu’il doit toomount pendant le processus de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="cd160-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="cd160-160">Ajouter le partage SMB hello garantit que ce partage de stockage de fichier hello est un système de fichiers monté définitivement pour hello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="cd160-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="cd160-161">Hello fichier stockage SMB partage tooa nouvel ordinateur virtuel est possible d’ajouter lorsque vous utilisez init-cloud.</span><span class="sxs-lookup"><span data-stu-id="cd160-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="cd160-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd160-162">Next steps</span></span>

- [<span data-ttu-id="cd160-163">Lors de la création à l’aide de cloud-init toocustomize un VM Linux</span><span class="sxs-lookup"><span data-stu-id="cd160-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="cd160-164">Ajouter un tooa de disque Linux VM</span><span class="sxs-lookup"><span data-stu-id="cd160-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="cd160-165">Chiffrer les disques sur un VM Linux à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="cd160-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
